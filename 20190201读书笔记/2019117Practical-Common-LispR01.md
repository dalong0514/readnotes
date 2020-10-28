# 2019117Practical-Common-LispR01

## 记忆时间

## 0301. Practical: A Simple Database

Obviously, before you can start building real software in Lisp, you'll have to learn the language. But let's face it--you may be thinking, "'Practical Common Lisp,' isn't that an oxymoron? Why should you be expected to bother learning all the details of a language unless it's actually good for something you care about?" So I'll start by giving you a small example of what you can do with Common Lisp. In this chapter you'll write a simple database for keeping track of CDs. You'll use similar techniques in Chapter 27 when you build a database of MP3s for our streaming MP3 server. In fact, you could think of this as part of the MP3 software project--after all, in order to have a bunch of MP3s to listen to, it might be helpful to be able to keep track of which CDs you have and which ones you need to rip.

In this chapter, I'll cover just enough Lisp as we go along for you to understand how the code works. But I'll gloss over quite a few details. For now you needn't sweat the small stuff--the next several chapters will cover all the Common Lisp constructs used here, and more, in a much more systematic way.

One terminology note: I'll discuss a handful of Lisp operators in this chapter. In Chapter 4, you'll learn that Common Lisp provides three distinct kinds of operators: functions, macros, and special operators. For the purposes of this chapter, you don't really need to know the difference. I will, however, refer to different operators as functions or macros or special operators as appropriate, rather than trying to hide the details behind the word operator. For now you can treat function, macro, and special operator as all more or less equivalent.1

Also, keep in mind that I won't bust out all the most sophisticated Common Lisp techniques for your very first post-"hello, world" program. The point of this chapter isn't that this is how you would write a database in Lisp; rather, the point is for you to get an idea of what programming in Lisp is like and to see how even a relatively simple Lisp program can be quite featureful.

1 Before I proceed, however, it's crucially important that you forget anything you may know about #define-style "macros" as implemented in the C pre-processor. Lisp macros are a totally different beast.

### 3.1 CDs and Records

To keep track of CDs that need to be ripped to MP3s and which CDs should be ripped first, each record in the database will contain the title and artist of the CD, a rating of how much the user likes it, and a flag saying whether it has been ripped. So, to start with, you'll need a way to represent a single database record (in other words, one CD). Common Lisp gives you lots of choices of data structures from a simple four-item list to a user-defined class, using the Common Lisp Object System (CLOS).

For now you can stay at the simple end of the spectrum and use a list. You can make a list with the LIST function, which, appropriately enough, returns a list of its arguments.

```c
CL-USER> (list 1 2 3) 
(1 2 3)
```

You could use a four-item list, mapping a given position in the list to a given field in the record. However, another flavor of list--called a property list, or plist for short--is even more convenient. A plist is a list where every other element, starting with the first, is a symbol that describes what the next element in the list is. I won't get into all the details of exactly what a symbol is right now; basically it's a name. For the symbols that name the fields in the CD database, you can use a particular kind of symbol, called a keyword symbol. A keyword is any name that starts with a colon (:), for instance, :foo. Here's an example of a plist using the keyword symbols :a, :b, and :c as property names:

```c
CL-USER> (list :a 1 :b 2 :c 3) 
(:A 1 :B 2 :C 3)
```

Note that you can create a property list with the same LIST function as you use to create other lists; it's the contents that make it a plist.

The thing that makes plists a convenient way to represent the records in a database is the function GETF, which takes a plist and a symbol and returns the value in the plist following the symbol, making a plist a sort of poor man's hash table. Lisp has real hash tables too, but plists are sufficient for your needs here and can more easily be saved to a file, which will come in handy later.

1『 autolisp 里是没有 getf 函数的。不过感觉它里面的 dotted pairs 就对应于这里的这种数据结构，其 assoc 函数对应于这里的 getf 函数。』

```c
CL-USER> (getf (list :a 1 :b 2 :c 3) :a) 
1 
CL-USER> (getf (list :a 1 :b 2 :c 3) :c) 
3
```

Given all that, you can easily enough write a function make-cd that will take the four fields as arguments and return a plist representing that CD.

```c
(defun make-cd (title artist rating ripped) 
  (list :title title :artist artist :rating rating :ripped ripped)
)
```

The word DEFUN tells us that this form is defining a new function. The name of the function is make-cd. After the name comes the parameter list. This function has four parameters: title, artist, rating, and ripped. Everything after the parameter list is the body of the function. In this case the body is just one form, a call to LIST. When make-cd is called, the arguments passed to the call will be bound to the variables in the parameter list. For instance, to make a record for the CD Roses by Kathy Mattea, you might call make-cd like this:

```c
CL-USER> (make-cd "Roses" "Kathy Mattea" 7 t) 
(:TITLE "Roses" :ARTIST "Kathy Mattea" :RATING 7 :RIPPED T)
```

### 3.2 Filing CDs

A single record, however, does not a database make. You need some larger construct to hold the records. Again, for simplicity's sake, a list seems like a good choice. Also for simplicity you can use a global variable, `*db*`, which you can define with the DEFVAR macro. The asterisks (*) in the name are a Lisp naming convention for global variables. 2

```c
(defvar *db* nil)
```

You can use the PUSH macro to add items to `*db*`. But it's probably a good idea to abstract things a tiny bit, so you should define a function add-record that adds a record to the database.

```c
(defun add-record (cd) (push cd *db*))
```

Now you can use add-record and make-cd together to add CDs to the database.

```c
CL-USER> (add-record (make-cd "Roses" "Kathy Mattea" 7 t)) 
((:TITLE "Roses" :ARTIST "Kathy Mattea" :RATING 7 :RIPPED T)) 

CL-USER> (add-record (make-cd "Fly" "Dixie Chicks" 8 t)) 
((:TITLE "Fly" :ARTIST "Dixie Chicks" :RATING 8 :RIPPED T) 
(:TITLE "Roses" :ARTIST "Kathy Mattea" :RATING 7 :RIPPED T)) 

CL-USER> (add-record (make-cd "Home" "Dixie Chicks" 9 t)) 
((:TITLE "Home" :ARTIST "Dixie Chicks" :RATING 9 :RIPPED T) 
(:TITLE "Fly" :ARTIST "Dixie Chicks" :RATING 8 :RIPPED T) 
(:TITLE "Roses" :ARTIST "Kathy Mattea" :RATING 7 :RIPPED T))
```

The stuff printed by the REPL after each call to add-record is the return value, which is the value returned by the last expression in the function body, the PUSH. And PUSH returns the new value of the variable it's modifying. So what you're actually seeing is the value of the database after the record has been added.

2 Using a global variable also has some drawbacks -- for instance, you can have only one database at a time. In Chapter 27, with more of the language under your belt, you'll be ready to build a more flexible database. You'll also see, in Chapter 6, how even using a global variable is more flexible in Common Lisp than it may be in other languages.

### 3.3 Looking at the Database Contents

You can also see the current value of `*db*` whenever you want by typing `*db*` at the REPL.

```c
CL-USER> *db* 
((:TITLE "Home" :ARTIST "Dixie Chicks" :RATING 9 :RIPPED T) 
(:TITLE "Fly" :ARTIST "Dixie Chicks" :RATING 8 :RIPPED T) 
(:TITLE "Roses" :ARTIST "Kathy Mattea" :RATING 7 :RIPPED T))
```

However, that's not a very satisfying way of looking at the output. You can write a dump-db function that dumps out the database in a more human-readable format, like this:

```
TITLE: Home 
ARTIST: Dixie Chicks 
RATING: 9 
RIPPED: T 

TITLE: Fly 
ARTIST: Dixie 
Chicks RATING: 8 
RIPPED: T 

TITLE: Roses 
ARTIST: Kathy Mattea 
RATING: 7 
RIPPED: T
```

The function looks like this:

```c
(defun dump-db () 
  (dolist (cd *db*) 
    (format t "~{~a:~10t~a~%~}~%" cd))
)
```

This function works by looping over all the elements of `*db* `with the DOLIST macro, binding each element to the variable cd in turn. For each value of cd, you use the FORMAT function to print it.

Admittedly, the FORMAT call is a little cryptic. However, FORMAT isn't particularly more complicated than C or Perl's printf function or Python's string-% operator. In Chapter 18 I'll discuss FORMAT in greater detail. For now we can take this call bit by bit. As you saw in Chapter 2, FORMAT takes at least two arguments, the first being the stream where it sends its output; t is shorthand for the stream `*standard-output*`.

The second argument to FORMAT is a format string that can contain both literal text and directives telling FORMAT things such as how to interpolate the rest of its arguments. Format directives start with ~ (much the way printf's directives start with %). FORMAT understands dozens of directives, each with their own set of options. 3 However, for now I'll just focus on the ones you need to write dump-db.

The ~a directive is the aesthetic directive; it means to consume one argument and output it in a human-readable form. This will render keywords without the leading : and strings without quotation marks. For instance:

```c
CL-USER> (format t "~a" "Dixie Chicks") 
Dixie Chicks 
NIL
```

or:

```c
CL-USER> (format t "~a" :title) 
TITLE 
NIL
```

The ~t directive is for tabulating. The ~10t tells FORMAT to emit enough spaces to move to the tenth column before processing the next ~a. A ~t doesn't consume any arguments.

```c
CL-USER> (format t "~a:~10t~a" :artist "Dixie Chicks") 
ARTIST: Dixie Chicks 
NIL
```

Now things get slightly more complicated. When FORMAT sees ~{ the next argument to be consumed must be a list. FORMAT loops over that list, processing the directives between the ~{ and ~}, consuming as many elements of the list as needed each time through the list. In dump-db, the FORMAT loop will consume one keyword and one value from the list each time through the loop. The ~% directive doesn't consume any arguments but tells FORMAT to emit a newline. Then after the ~} ends the loop, the last ~% tells FORMAT to emit one more newline to put a blank line between each CD.

Technically, you could have also used FORMAT to loop over the database itself, turning our dump-db function into a one-liner.

```c
(defun dump-db () 
  (format t "~{~{~a:~10t~a~%~}~%~}" *db*)
)
```

That's either very cool or very scary depending on your point of view.

3 One of the coolest FORMAT directives is the ~R directive. Ever want to know how to say a really big number in English words? Lisp knows. Evaluate this:

```c
(format nil "~r" 1606938044258990275541962092)
```

and you should get back the following (wrapped for legibility):

```
one octillion six hundred six septillion nine hundred thirty-eight sextillion forty-four quintillion two hundred fifty-eight quadrillion nine hundred ninety trillion two hundred seventy-five billion five hundred forty-one million nine hundred sixty-two thousand ninety-two
```

### 3.4 Improving the User Interaction

While our add-record function works fine for adding records, it's a bit Lispy for the casual user. And if they want to add a bunch of records, it's not very convenient. So you may want to write a function to prompt the user for information about a set of CDs. Right away you know you'll need some way to prompt the user for a piece of information and read it. So let's write that.

```c
(defun prompt-read (prompt) 
  (format *query-io* "~a: " prompt) 
  (force-output *query-io*) 
  (read-line *query-io*)
)
```

You use your old friend FORMAT to emit a prompt. Note that there's no ~% in the format string, so the cursor will stay on the same line. The call to FORCE-OUTPUT is necessary in some implementations to ensure that Lisp doesn't wait for a newline before it prints the prompt.

Then you can read a single line of text with the aptly named READ-LINE function. The variable `*query-io*` is a global variable (which you can tell because of the `*` naming convention for global variables) that contains the input stream connected to the terminal. The return value of prompt-read will be the value of the last form, the call to READ-LINE, which returns the string it read (without the trailing newline.)

You can combine your existing make-cd function with prompt-read to build a function that makes a new CD record from data it gets by prompting for each value in turn.

```c
(defun prompt-for-cd () 
  (make-cd 
    (prompt-read "Title") 
    (prompt-read "Artist") 
    (prompt-read "Rating") 
    (prompt-read "Ripped [y/n]"))
)
```

That's almost right. Except prompt-read returns a string, which, while fine for the Title and Artist fields, isn't so great for the Rating and Ripped fields, which should be a number and a boolean. Depending on how sophisticated a user interface you want, you can go to arbitrary lengths to validate the data the user enters. For now let's lean toward the quick and dirty: you can wrap the prompt-read for the rating in a call to Lisp's PARSE-INTEGER function, like this:

```c
(parse-integer (prompt-read "Rating"))
```

Unfortunately, the default behavior of PARSE-INTEGER is to signal an error if it can't parse an integer out of the string or if there's any non-numeric junk in the string. However, it takes an optional keyword argument :junk-allowed, which tells it to relax a bit.

```c
(parse-integer (prompt-read "Rating") :junk-allowed t)
```

But there's still one problem: if it can't find an integer amidst all the junk, PARSE-INTEGER will return NIL rather than a number. In keeping with the quick-and-dirty approach, you may just want to call that 0 and continue. Lisp's OR macro is just the thing you need here. It's similar to the "short-circuiting" || in Perl, Python, Java, and C; it takes a series of expressions, evaluates them one at a time, and returns the first non-nil value (or NIL if they're all NIL). So you can use the following:

```c
(or (parse-integer (prompt-read "Rating") :junk-allowed t) 0)
```

to get a default value of 0.

1『在 autolisp 里试验过，or 只是一个逻辑或的功能，不能实现这里，前一个语句是 nil 时自动取后一个语句为默认值的功能。比如 `(or nil 0)` 返回的是 `T`。（2020-10-22）』

Fixing the code to prompt for Ripped is quite a bit simpler. You can just use the Common Lisp function Y-OR-N-P.

```c
(y-or-n-p "Ripped [y/n]: ")
```

In fact, this will be the most robust part of prompt-for-cd, as Y-OR-N-P will reprompt the user if they enter something that doesn't start with y, Y, n, or N. Putting those pieces together you get a reasonably robust prompt-for-cd function.

```c
(defun prompt-for-cd () 
  (make-cd 
    (prompt-read "Title") 
    (prompt-read "Artist") 
    (or (parse-integer (prompt-read "Rating") :junk-allowed t) 0) 
    (y-or-n-p "Ripped [y/n]: "))
)
```

Finally, you can finish the "add a bunch of CDs" interface by wrapping prompt-for-cd in a function that loops until the user is done. You can use the simple form of the LOOP macro, which repeatedly executes a body of expressions until it's exited by a call to RETURN. For example:

```c
(defun add-cds () 
  (loop (add-record (prompt-for-cd)) 
    (if (not (y-or-n-p "Another? [y/n]: ")) 
      (return)
    )
  )
)
```

Now you can use add-cds to add some more CDs to the database.

```c
CL-USER> (add-cds) 
Title: Rockin' the Suburbs 
Artist: Ben Folds 
Rating: 6 
Ripped [y/n]: y 
Another? [y/n]: y 
Title: Give Us a Break 
Artist: Limpopo 
Rating: 10 
Ripped [y/n]: y 
Another? [y/n]: y 
Title: Lyle Lovett 
Artist: Lyle Lovett 
Rating: 9 
Ripped [y/n]: y 
Another? [y/n]: n 
NIL
```

### 3.5 Saving and Loading the Database

Having a convenient way to add records to the database is nice. But it's not so nice that the user is going to be very happy if they have to reenter all the records every time they quit and restart Lisp. Luckily, with the data structures you're using to represent the data, it's trivially easy to save the data to a file and reload it later. Here's a save-db function that takes a filename as an argument and saves the current state of the database:

```c
(defun save-db (filename) 
  (with-open-file 
    (out filename 
      :direction :output 
      :if-exists :supersede) 
    (with-standard-io-syntax (print *db* out))
  )
)
```

The WITH-OPEN-FILE macro opens a file, binds the stream to a variable, executes a set of expressions, and then closes the file. It also makes sure the file is closed even if something goes wrong while evaluating the body. The list directly after WITH-OPEN-FILE isn't a function call but rather part of the syntax defined by WITH-OPEN-FILE. It contains the name of the variable that will hold the file stream to which you'll write within the body of WITH-OPEN-FILE, a value that must be a file name, and then some options that control how the file is opened. Here you specify that you're opening the file for writing with :direction :output and that you want to overwrite an existing file of the same name if it exists with :if-exists :supersede.

Once you have the file open, all you have to do is print the contents of the database with (print `*db*` out). Unlike FORMAT, PRINT prints Lisp objects in a form that can be read back in by the Lisp reader. The macro WITH-STANDARD-IO-SYNTAX ensures that certain variables that affect the behavior of PRINT are set to their standard values. You'll use the same macro when you read the data back in to make sure the Lisp reader and printer are operating compatibly.

The argument to save-db should be a string containing the name of the file where the user wants to save the database. The exact form of the string will depend on what operating system they're using. For instance, on a Unix box they should be able to call save-db like this:

```c
CL-USER> (save-db "~/my-cds.db") 
((:TITLE "Lyle Lovett" :ARTIST "Lyle Lovett" :RATING 9 :RIPPED T) 
 (:TITLE "Give Us a Break" :ARTIST "Limpopo" :RATING 10 :RIPPED T) 
 (:TITLE "Rockin' the Suburbs" :ARTIST "Ben Folds" :RATING 6 :RIPPED T) 
 (:TITLE "Home" :ARTIST "Dixie Chicks" :RATING 9 :RIPPED T) 
 (:TITLE "Fly" :ARTIST "Dixie Chicks" :RATING 8 :RIPPED T) 
 (:TITLE "Roses" :ARTIST "Kathy Mattea" :RATING 9 :RIPPED T))
```

On Windows, the filename might be something like "c:/my-cds.db" or "c:\\my-cds.db." 4 You can open this file in any text editor to see what it looks like. You should see something a lot like what the REPL prints if you type `*db*`.

The function to load the database back in is similar.

```c
(defun load-db (filename) 
  (with-open-file (in filename) 
    (with-standard-io-syntax 
      (setf *db* (read in))
    )
  )
)
```

This time you don't need to specify :direction in the options to WITH-OPEN-FILE, since you want the default of :input. And instead of printing, you use the function READ to read from the stream in. This is the same reader used by the REPL and can read any Lisp expression you could type at the REPL prompt. However, in this case, you're just reading and saving the expression, not evaluating it. Again, the WITH-STANDARD-IO-SYNTAX macro ensures that READ is using the same basic syntax that save-db did when it PRINTed the data.

The SETF macro is Common Lisp's main assignment operator. It sets its first argument to the result of evaluating its second argument. So in load-db the `*db*` variable will contain the object read from the file, namely, the list of lists written by save-db. You do need to be careful about one thing--load-db clobbers whatever was in `*db*` before the call. So if you've added records with add-record or add-cds that haven't been saved with save-db, you'll lose them.

### 3.6 Querying the Database

Now that you have a way to save and reload the database to go along with a convenient user interface for adding new records, you soon may have enough records that you won't want to be dumping out the whole database just to look at what's in it. What you need is a way to query the database. You might like, for instance, to be able to write something like this:

```c
(select :artist "Dixie Chicks")
```

and get a list of all the records where the artist is the Dixie Chicks. Again, it turns out that the choice of saving the records in a list will pay off.

The function REMOVE-IF-NOT takes a predicate and a list and returns a list containing only the elements of the original list that match the predicate. In other words, it has removed all the elements that don't match the predicate. However, REMOVE-IF-NOT doesn't really remove anything--it creates a new list, leaving the original list untouched. It's like running grep over a file. The predicate argument can be any function that accepts a single argument and returns a boolean value--NIL for false and anything else for true.

For instance, if you wanted to extract all the even elements from a list of numbers, you could use REMOVE-IF-NOT as follows:

```c
CL-USER> (remove-if-not #'evenp '(1 2 3 4 5 6 7 8 9 10)) 
(2 4 6 8 10)
```

In this case, the predicate is the function EVENP, which returns true if its argument is an even number. The funny notation #' is shorthand for "Get me the function with the following name." Without the #', Lisp would treat evenp as the name of a variable and look up the value of the variable, not the function.

1『原来 common lisp 里，函数名前面加上 `#'` 表示是个函数。感觉类似于 autolisp 里函数名前面的 `'`。（2020-10-22）』

You can also pass REMOVE-IF-NOT an anonymous function. For instance, if EVENP didn't exist, you could write the previous expression as the following:

```c
CL-USER> 
(remove-if-not 
  #'(lambda (x) (= 0 (mod x 2))) 
  '(1 2 3 4 5 6 7 8 9 10)
) 

(2 4 6 8 10)
```

1『有点 autolisp 里 mapcar 函数的味道了，哈哈。测试了下，autolisp 里是没有 mod 函数的。（2020-10-22）』

In this case, the predicate is this anonymous function:

```c
(lambda (x) (= 0 (mod x 2)))
```

which checks that its argument is equal to 0 modulus 2 (in other words, is even). If you wanted to extract only the odd numbers using an anonymous function, you'd write this:

```c
CL-USER> 
(remove-if-not 
  #'(lambda (x) (= 1 (mod x 2))) 
  '(1 2 3 4 5 6 7 8 9 10)
) 

(1 3 5 7 9)
```

Note that lambda isn't the name of the function--it's the indicator you're defining an anonymous function. 5 Other than the lack of a name, however, a LAMBDA expression looks a lot like a DEFUN: the word lambda is followed by a parameter list, which is followed by the body of the function.

To select all the Dixie Chicks' albums in the database using REMOVE-IF-NOT, you need a function that returns true when the artist field of a record is "Dixie Chicks". Remember that we chose the plist representation for the database records because the function GETF can extract named fields from a plist. So assuming cd is the name of a variable holding a single database record, you can use the expression `(getf cd :artist)` to extract the name of the artist. The function EQUAL, when given string arguments, compares them character by character. So `(equal (getf cd :artist) "Dixie Chicks")` will test whether the artist field of a given CD is equal to "Dixie Chicks". All you need to do is wrap that expression in a LAMBDA form to make an anonymous function and pass it to REMOVE-IF-NOT.

```c
CL-USER> 

(remove-if-not 
  #'(lambda (cd) (equal (getf cd :artist) "Dixie Chicks")) 
  *db*
) 
((:TITLE "Home" :ARTIST "Dixie Chicks" :RATING 9 :RIPPED T) 
  (:TITLE "Fly" :ARTIST "Dixie Chicks" :RATING 8 :RIPPED T)
)
```

Now suppose you want to wrap that whole expression in a function that takes the name of the artist as an argument. You can write that like this:

```c
(defun select-by-artist (artist) 
  (remove-if-not 
    #'(lambda (cd) (equal (getf cd :artist) artist)) 
    *db*
  )
)
```

Note how the anonymous function, which contains code that won't run until it's invoked in REMOVE-IF-NOT, can nonetheless refer to the variable artist. In this case the anonymous function doesn't just save you from having to write a regular function--it lets you write a function that derives part of its meaning--the value of artist--from the context in which it's embedded.

1-2-3『

看到这里才意识到 `remove-if-not` 就是用来构造过滤函数的啊，这正式自己之前 PHP 里用的最多的 `array_filter` 函数，试着在 autolisp 的文档里搜了下，发现果然有 `vl-remove-if-not`，有了它的话，自己很多很多的功能开发都可以基于它变得简洁优雅，简直是捡到金子了，哈哈。做一张术语卡片。（2020-10-22）

[vl-remove-if-not (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-53D12042-8DE3-4DAA-83BD-8ABB376ACA97)

Returns all elements of the supplied list that pass the test function.

```c
(vl-remove-if-not predicate-function lst)
```

predicate-function. Type: Subroutine or Symbol. The test function. This can be any function that accepts a single argument and returns T for any user-specified condition. The predicate-function value can take one of the following forms:

```c
A symbol (function name)
'(LAMBDA (A1 A2) ...)
(FUNCTION (LAMBDA (A1 A2) ...))
```

lst. Type: List. A list to be tested.

Return Values. Type: List or nil.

A list containing all elements of lst for which predicate-function returns a non-nil value

```c
(vl-remove-if-not 'vl-symbolp (list pi t 0 "abc"))
(T)
```

自己写了个例子：

```c
(vl-remove-if-not 
  '(lambda (x) (= x 2)) 
  '(1 2 3 4)
)
```

返回元素为 2 的列表 `(2)`。

vl-remove-if (AutoLISP). Returns all elements of the supplied list that fail the test function.

```c
(vl-remove-if 'vl-symbolp (list pi t 0 "abc"))
(3.14159 0 "abc")
```

vl-remove (AutoLISP). Removes elements from a list.

```c
(vl-remove element-to-remove lst)
```

element-to-remove. Type: Integer, Real, String, List, File, Ename (entity name), T, or nil. The value of the element to be removed; may be any LISP data type.

lst. Type: List. Any list.

Return Values. Type: List or nil. The lst with all elements except those equal to element-to-remove.

```c
(vl-remove pi (list pi t 0 "abc"))
(T 0 "abc")
```

vl-member-if-not (AutoLISP). Determines if the predicate is nil for one of the list members.

```c
(vl-member-if-not predicate-function lst)
```

predicate-function. Type: Subroutine or Symbol. The test function. This can be any function that accepts a single argument and returns T for any user-specified condition. The predicate-function value can take one of the following forms:

Return Values. Type: List or nil. A list, starting with the first element that fails the test and containing all elements following this in the original argument. If none of the elements fails the test condition, vl-member-if-not returns nil.

Remarks: The vl-member-if-not function passes each element in lst to the function specified in predicate-function. If the function returns nil, vl-member-if-not returns the rest of the list in the same manner as the member function.

```c
(vl-member-if-not 'atom '(1 "Str" (0 . "line") nil t))
((0 . "line") nil T)
```

1「函数 `vl-member-if-not` 目前没吃透，不过直觉上感觉有大用途。（2020-10-22）」

』

So that's select-by-artist. However, selecting by artist is only one of the kinds of queries you might like to support. You could write several more functions, such as select-by-title, select-by-rating, select-by-title-and-artist, and so on. But they'd all be about the same except for the contents of the anonymous function. You can instead make a more general select function that takes a function as an argument.

```c
(defun select (selector-fn) 
  (remove-if-not selector-fn *db*)
)
```

So what happened to the #'? Well, in this case you don't want REMOVE-IF-NOT to use the function named selector-fn. You want it to use the anonymous function that was passed as an argument to select in the variable selector-fn. Though, the #' comes back in the call to select.

```c
CL-USER> 
(select 
  #'(lambda (cd) (equal (getf cd :artist) "Dixie Chicks"))
) 
((:TITLE "Home" :ARTIST "Dixie Chicks" :RATING 9 :RIPPED T) 
  (:TITLE "Fly" :ARTIST "Dixie Chicks" :RATING 8 :RIPPED T))
```

But that's really quite gross-looking. Luckily, you can wrap up the creation of the anonymous function.

```c
(defun artist-selector (artist) 
  #'(lambda (cd) (equal (getf cd :artist) artist))
)
```

This is a function that returns a function and one that references a variable that--it seems--won't exist after artist-selector returns. 6 It may seem odd now, but it actually works just the way you'd want--if you call artist-selector with an argument of "Dixie Chicks", you get an anonymous function that matches CDs whose :artist field is "Dixie Chicks", and if you call it with "Lyle Lovett", you get a different function that will match against an :artist field of "Lyle Lovett". So now you can rewrite the call to select like this:

```c
CL-USER> 
(select (artist-selector "Dixie Chicks")) 
((:TITLE "Home" :ARTIST "Dixie Chicks" :RATING 9 :RIPPED T) 
  (:TITLE "Fly" :ARTIST "Dixie Chicks" :RATING 8 :RIPPED T))
```

Now you just need some more functions to generate selectors. But just as you don't want to have to write select-by-title, select-by-rating, and so on, because they would all be quite similar, you're not going to want to write a bunch of nearly identical selector-function generators, one for each field. Why not write one general-purpose selector-function generator, a function that, depending on what arguments you pass it, will generate a selector function for different fields or maybe even a combination of fields? You can write such a function, but first you need a crash course in a feature called keyword parameters.

In the functions you've written so far, you've specified a simple list of parameters, which are bound to the corresponding arguments in the call to the function. For instance, the following function:

```c
(defun foo (a b c) 
  (list a b c)
)
```

has three parameters, a, b, and c, and must be called with three arguments. But sometimes you may want to write a function that can be called with varying numbers of arguments. Keyword parameters are one way to achieve this. A version of foo that uses keyword parameters might look like this:

```c
(defun foo (&key a b c) 
  (list a b c)
)
```

The only difference is the &key at the beginning of the argument list. However, the calls to this new foo will look quite different. These are all legal calls with the result to the right of the ==>:

```c
(foo :a 1 :b 2 :c 3) ==> (1 2 3) 
(foo :c 3 :b 2 :a 1) ==> (1 2 3) 
(foo :a 1 :c 3) ==> (1 NIL 3) 
(foo) ==> (NIL NIL NIL)
```

As these examples show, the value of the variables a, b, and c are bound to the values that follow the corresponding keyword. And if a particular keyword isn't present in the call, the corresponding variable is set to NIL. I'm glossing over a bunch of details of how keyword parameters are specified and how they relate to other kinds of parameters, but you need to know one more detail.

Normally if a function is called with no argument for a particular keyword parameter, the parameter will have the value NIL. However, sometimes you'll want to be able to distinguish between a NIL that was explicitly passed as the argument to a keyword parameter and the default value NIL. To allow this, when you specify a keyword parameter you can replace the simple name with a list consisting of the name of the parameter, a default value, and another parameter name, called a supplied-p parameter. The supplied-p parameter will be set to true or false depending on whether an argument was actually passed for that keyword parameter in a particular call to the function. Here's a version of foo that uses this feature:

```c
(defun foo (&key a (b 20) (c 30 c-p)) 
  (list a b c c-p)
)
```

Now the same calls from earlier yield these results:

```c
(foo :a 1 :b 2 :c 3) ==> (1 2 3 T) 
(foo :c 3 :b 2 :a 1) ==> (1 2 3 T) 
(foo :a 1 :c 3) ==> (1 20 3 T) 
(foo) ==> (NIL 20 30 NIL)
```

The general selector-function generator, which you can call where for reasons that will soon become apparent if you're familiar with SQL databases, is a function that takes four keyword parameters corresponding to the fields in our CD records and generates a selector function that selects any CDs that match all the values given to where. For instance, it will let you say things like this:

```c
(select (where :artist "Dixie Chicks"))
```

or this:

```c
(select (where :rating 10 :ripped nil))
```

The function looks like this:

```c
(defun where (&key title artist rating (ripped nil ripped-p)) 
  #'(lambda (cd) 
      (and 
        (if title (equal (getf cd :title) title) t) 
        (if artist (equal (getf cd :artist) artist) t) 
        (if rating (equal (getf cd :rating) rating) t) 
        (if ripped-p (equal (getf cd :ripped) ripped) t)
      )
    )
)
```

This function returns an anonymous function that returns the logical AND of one clause per field in our CD records. Each clause checks if the appropriate argument was passed in and then either compares it to the value in the corresponding field in the CD record or returns t, Lisp's version of truth, if the parameter wasn't passed in. Thus, the selector function will return t only for CDs that match all the arguments passed to where. 7 Note that you need to use a three-item list to specify the keyword parameter ripped because you need to know whether the caller actually passed :ripped nil, meaning, "Select CDs whose ripped field is nil," or whether they left out :ripped altogether, meaning "I don't care what the value of the ripped field is."

4 Windows actually understands forward slashes in filenames even though it normally uses a backslash as the directory separator. This is convenient since otherwise you have to write double backslashes because backslash is the escape character in Lisp strings.

5 The word lambda is used in Lisp because of an early connection to the lambda calculus, a mathematical formalism invented for studying mathematical functions.

6 The technical term for a function that references a variable in its enclosing scope is a closure because the function “closes over” the variable. I’ll discuss closures in more detail in Chapter 6.

7 Note that in Lisp, an IF form, like everything else, is an expression that returns a value. It’s actually more like the ternary operator `(?:)` in Perl, Java, and C in that this is legal in those languages:

```c
some_var = some_boolean ? value1 : value2;
```

while this isn’t:

```
some_var = if (some_boolean) value1; else value2;
```

because in those languages, if is a statement, not an expression.

### 3.7 Updating Existing Records--Another Use for WHERE

Now that you've got nice generalized select and where functions, you're in a good position to write the next feature that every database needs--a way to update particular records. In SQL the update command is used to update a set of records matching a particular where clause. That seems like a good model, especially since you've already got a where-clause generator. In fact, the update function is mostly just the application of a few ideas you've already seen: using a passed-in selector function to choose the records to update and using keyword arguments to specify the values to change. The main new bit is the use of a function MAPCAR that maps over a list, `*db*` in this case, and returns a new list containing the results of calling a function on each item in the original list.

```c
(defun update (selector-fn &key title artist rating (ripped nil ripped-p)) 
  (setf *db* 
    (mapcar 
      #'(lambda (row) 
          (when (funcall selector-fn row) 
            (if title (setf (getf row :title) title)) 
            (if artist (setf (getf row :artist) artist)) 
            (if rating (setf (getf row :rating) rating)) 
            (if ripped-p (setf (getf row :ripped) ripped))
          ) 
          row
        ) 
      *db*
    )
  )
)
```

1『这里明显，函数的参数竟然可以直接传进 mapcar 回调函数里，autolisp 里不知道行不行，可行的话就太好了，待验证。（2020-10-22）』

One other new bit here is the use of SETF on a complex form such as `(getf row :title)`. I'll discuss SETF in greater detail in Chapter 6, but for now you just need to know that it's a general assignment operator that can be used to assign lots of "places" other than just variables. (It's a coincidence that SETF and GETF have such similar names--they don't have any special relationship.) For now it's enough to know that after `(setf (getf row :title) title)`, the plist referenced by row will have the value of the variable title following the property name :title. With this update function if you decide that you really dig the Dixie Chicks and that all their albums should go to 11, you can evaluate the following form:

```c
CL-USER> (update (where :artist "Dixie Chicks") :rating 11) 
NIL
```

And it is so.

```c
CL-USER> (select (where :artist "Dixie Chicks")) 
((:TITLE "Home" :ARTIST "Dixie Chicks" :RATING 11 :RIPPED T) 
  (:TITLE "Fly" :ARTIST "Dixie Chicks" :RATING 11 :RIPPED T))
```

You can even more easily add a function to delete rows from the database.

```c
(defun delete-rows (selector-fn) 
  (setf *db* (remove-if selector-fn *db*))
)
```

The function REMOVE-IF is the complement of REMOVE-IF-NOT; it returns a list with all the elements that do match the predicate removed. Like REMOVE-IF-NOT, it doesn't actually affect the list it's passed but by saving the result back into `*db*`, delete-rows 8 actually changes the contents of the database. 9

8 You need to use the name delete-rows rather than the more obvious delete because there’s already a function in Common Lisp called DELETE. The Lisp package system gives you a way to deal with such naming conflicts, so you could have a function named delete if you wanted. But I’m not ready to explain packages just yet.

9 If you’re worried that this code creates a memory leak, rest assured: Lisp was the language that invented garbage collection (and heap allocation for that matter). The memory used by the old value of `*db*` will be automatically reclaimed, assuming no one else is holding on to a reference to it, which none of this code is.

### 3.8 Removing Duplication and Winning Big

So far all the database code supporting insert, select, update, and delete, not to mention a command-line user interface for adding new records and dumping out the contents, is just a little more than 50 lines. Total. 10

1『看到这里，突然意识到，完全可以把 CAD 图纸直接作为一个本地数据库，直接在 lisp 文件里实现对该数据库的增删改查。（2020-10-22）』

Yet there's still some annoying code duplication. And it turns out you can remove the duplication and make the code more flexible at the same time. The duplication I'm thinking of is in the where function. The body of the where function is a bunch of clauses like this, one per field:

```c
(if title (equal (getf cd :title) title) t)
```

Right now it's not so bad, but like all code duplication it has the same cost: if you want to change how it works, you have to change multiple copies. And if you change the fields in a CD, you'll have to add or remove clauses to where. And update suffers from the same kind of duplication. It's doubly annoying since the whole point of the where function is to dynamically generate a bit of code that checks the values you care about; why should it have to do work at runtime checking whether title was even passed in?

Imagine that you were trying to optimize this code and discovered that it was spending too much time checking whether title and the rest of the keyword parameters to where were even set? 11 If you really wanted to remove all those runtime checks, you could go through a program and find all the places you call where and look at exactly what arguments you're passing. Then you could replace each call to where with an anonymous function that does only the computation necessary. For instance, if you found this snippet of code:

```c
(select (where :title "Give Us a Break" :ripped t))
```

you could change it to this:

```c
(select 
  #'(lambda (cd) 
      (and 
        (equal (getf cd :title) "Give Us a Break") 
        (equal (getf cd :ripped) t)
      )
    )
)
```

Note that the anonymous function is different from the one that where would have returned; you're not trying to save the call to where but rather to provide a more efficient selector function. This anonymous function has clauses only for the fields that you actually care about at this call site, so it doesn't do any extra work the way a function returned by where might.

You can probably imagine going through all your source code and fixing up all the calls to where in this way. But you can probably also imagine that it would be a huge pain. If there were enough of them, and it was important enough, it might even be worthwhile to write some kind of preprocessor that converts where calls to the code you'd write by hand.

The Lisp feature that makes this trivially easy is its macro system. I can't emphasize enough that the Common Lisp macro shares essentially nothing but the name with the text-based macros found in C and C++. Where the C pre-processor operates by textual substitution and understands almost nothing of the structure of C and C++, a Lisp macro is essentially a code generator that gets run for you automatically by the compiler. 12 When a Lisp expression contains a call to a macro, instead of evaluating the arguments and passing them to the function, the Lisp compiler passes the arguments, unevaluated, to the macro code, which returns a new Lisp expression that is then evaluated in place of the original macro call.

1『感觉开始接触到 lisp 特有的模型了，macro code 的相关信息就是一种体现。（2020-10-22）』

I'll start with a simple, and silly, example and then show how you can replace the where function with a where macro. Before I can write this example macro, I need to quickly introduce one new function: REVERSE takes a list as an argument and returns a new list that is its reverse. So `(reverse '(1 2 3))` evaluates to (3 2 1). Now let's create a macro.

```c
(defmacro backwards (expr) (reverse expr))
```

The main syntactic difference between a function and a macro is that you define a macro with DEFMACRO instead of DEFUN. After that a macro definition consists of a name, just like a function, a parameter list, and a body of expressions, both also like a function. However, a macro has a totally different effect. You can use this macro as follows:

```c
CL-USER> (backwards ("hello, world" t format)) 
hello, world 
NIL
```

How did that work? When the REPL started to evaluate the backwards expression, it recognized that backwards is the name of a macro. So it left the expression `("hello, world" t format)` unevaluated, which is good because it isn't a legal Lisp form. It then passed that list to the backwards code. The code in backwards passed the list to REVERSE, which returned the list `(format t "hello, world")`. backwards then passed that value back out to the REPL, which then evaluated it in place of the original expression.

The backwards macro thus defines a new language that's a lot like Lisp--just backward--that you can drop into anytime simply by wrapping a backward Lisp expression in a call to the backwards macro. And, in a compiled Lisp program, that new language is just as efficient as normal Lisp because all the macro code--the code that generates the new expression--runs at compile time. In other words, the compiler will generate exactly the same code whether you write `(backwards ("hello, world" t format))` or `(format t "hello, world")`.

So how does that help with the code duplication in where? Well, you can write a macro that generates exactly the code you need for each particular call to where. Again, the best approach is to build our code bottom up. In the hand-optimized selector function, you had an expression of the following form for each actual field referred to in the original call to where:

1『这里说了 macro 的用途。（2020-10-22）』

```c
(equal (getf cd field) value)
```

So let's write a function that, given the name of a field and a value, returns such an expression. Since an expression is just a list, you might think you could write something like this:

```c
(defun make-comparison-expr (field value) ; wrong 
  (list equal (list getf cd field) value)
)
```

However, there's one trick here: as you know, when Lisp sees a simple name such as field or value other than as the first element of a list, it assumes it's the name of a variable and looks up its value. That's fine for field and value; it's exactly what you want. But it will treat equal, getf, and cd the same way, which isn't what you want. However, you also know how to stop Lisp from evaluating a form: stick a single forward quote (') in front of it. So if you write make-comparison-expr like this, it will do what you want:

```c
(defun make-comparison-expr (field value) 
  (list 'equal (list 'getf 'cd field) value)
)
```

1-2『直觉上这里可以解释自己之前一直有的疑惑，`'` 到底是什么，有什么用处。不过目前上面的信息还看不太懂，也可以 Google 下相关知识。（2020-10-22）』

You can test it out in the REPL.

```c
CL-USER> (make-comparison-expr :rating 10) 
(EQUAL (GETF CD :RATING) 10) 

CL-USER> (make-comparison-expr :title "Give Us a Break") 
(EQUAL (GETF CD :TITLE) "Give Us a Break")
```

It turns out that there's an even better way to do it. What you'd really like is a way to write an expression that's mostly not evaluated and then have some way to pick out a few expressions that you do want evaluated. And, of course, there's just such a mechanism. A back quote (`) before an expression stops evaluation just like a forward quote.

```c
CL-USER> `(1 2 3) 
(1 2 3) 

CL-USER> '(1 2 3) 
(1 2 3)
```

1『感觉它的作用去「消除」自动计算，即消除后面 `()` 函数要自动计算的东西。（2020-10-22）』

However, in a back-quoted expression, any subexpression that's preceded by a comma is evaluated. Notice the effect of the comma in the second expression:

```c
`(1 2 (+ 1 2)) ==> (1 2 (+ 1 2)) 
`(1 2 ,(+ 1 2)) ==> (1 2 3)
```

Using a back quote, you can write make-comparison-expr like this:

```c
(defun make-comparison-expr (field value) 
  `(equal (getf cd ,field) ,value)
)
```

Now if you look back to the hand-optimized selector function, you can see that the body of the function consisted of one comparison expression per field/value pair, all wrapped in an AND expression. Assume for the moment that you'll arrange for the arguments to the where macro to be passed as a single list. You'll need a function that can take the elements of such a list pairwise and collect the results of calling make-comparison-expr on each pair. To implement that function, you can dip into the bag of advanced Lisp tricks and pull out the mighty and powerful LOOP macro.

```c
(defun make-comparisons-list (fields) 
  (loop while fields 
    collecting (make-comparison-expr (pop fields) (pop fields))
  )
)
```

A full discussion of LOOP will have to wait until Chapter 22; for now just note that this LOOP expression does exactly what you need: it loops while there are elements left in the fields list, popping off two at a time, passing them to make-comparison-expr, and collecting the results to be returned at the end of the loop. The POP macro performs the inverse operation of the PUSH macro you used to add records to `*db*`.

Now you just need to wrap up the list returned by make-comparison-list in an AND and an anonymous function, which you can do in the where macro itself. Using a back quote to make a template that you fill in by interpolating the value of make-comparisons-list, it's trivial.

```c
(defmacro where (&rest clauses) 
  `#'(lambda (cd) (and ,@(make-comparisons-list clauses)))
)
```

This macro uses a variant of , (namely, the ,@) before the call to make-comparisons-list. The ,@ "splices" the value of the following expression--which must evaluate to a list--into the enclosing list. You can see the difference between , and ,@ in the following two expressions:

```c
`(and ,(list 1 2 3)) ==> (AND (1 2 3)) 
`(and ,@(list 1 2 3)) ==> (AND 1 2 3)
```

You can also use ,@ to splice into the middle of a list.

```c
`(and ,@(list 1 2 3) 4) ==> (AND 1 2 3 4)
```

The other important feature of the where macro is the use of &rest in the argument list. Like &key, &rest modifies the way arguments are parsed. With a &rest in its parameter list, a function or macro can take an arbitrary number of arguments, which are collected into a single list that becomes the value of the variable whose name follows the &rest. So if you call where like this:

```c
(where :title "Give Us a Break" :ripped t)
```

the variable clauses will contain the list.

```c
(:title "Give Us a Break" :ripped t)
```

2『 `&key` 和 `&rest` 做一张术语卡片。（2020-10-22）』——未完成

This list is passed to make-comparisons-list, which returns a list of comparison expressions. You can see exactly what code a call to where will generate using the function MACROEXPAND-1. If you pass MACROEXPAND-1, a form representing a macro call, it will call the macro code with appropriate arguments and return the expansion. So you can check out the previous where call like this:

```c
CL-USER> 
(macroexpand-1 '(where :title "Give Us a Break" :ripped t)) 
#'(LAMBDA (CD) 
  (AND (EQUAL (GETF CD :TITLE) "Give Us a Break") 
    (EQUAL (GETF CD :RIPPED) T)
  )
) 
T
```

Looks good. Let's try it for real.

```c
CL-USER> (select (where :title "Give Us a Break" :ripped t)) 
((:TITLE "Give Us a Break" :ARTIST "Limpopo" :RATING 10 :RIPPED T))
```

It works. And the where macro with its two helper functions is actually one line shorter than the old where function. And it's more general in that it's no longer tied to the specific fields in our CD records.

10 A friend of mine was once interviewing an engineer for a programming job and asked him a typical interview question: how do you know when a function or method is too big? Well, said the candidate, I don’t like any method to be bigger than my head. You mean you can’t keep all the details in your head? No, I mean I put my head up against my monitor, and the code shouldn’t be bigger than my head.

11 It’s unlikely that the cost of checking whether keyword parameters had been passed would be a detectible drag on performance since checking whether a variable is NIL is going to be pretty cheap. On the other hand, these functions returned by where are going to be right in the middle of the inner loop of any select, update, or delete-rows call, as they have to be called once per entry in the database. Anyway, for illustrative purposes, this will have to do.

12 Macros are also run by the interpreter—however, it’s easier to understand the point of macros when you think about compiled code. As with everything else in this chapter, I’ll cover this in greater detail in future chapters.

### 3.9 Wrapping Up

Now, an interesting thing has happened. You removed duplication and made the code more efficient and more general at the same time. That's often the way it goes with a well-chosen macro. This makes sense because a macro is just another mechanism for creating abstractions--abstraction at the syntactic level, and abstractions are by definition more concise ways of expressing underlying generalities. Now the only code in the mini-database that's specific to CDs and the fields in them is in the make-cd, prompt-for-cd, and add-cd functions. In fact, our new where macro would work with any plist-based database.

However, this is still far from being a complete database. You can probably think of plenty of features to add, such as supporting multiple tables or more elaborate queries. In Chapter 27 we'll build an MP3 database that incorporates some of those features.

The point of this chapter was to give you a quick introduction to just a handful of Lisp's features and show how they're used to write code that's a bit more interesting than "hello, world." In the next chapter we'll begin a more systematic overview of Lisp.

## 0401. Syntax and Semantics

After that whirlwind tour, we'll settle down for a few chapters to take a more systematic look at the features you've used so far. I'll start with an overview of the basic elements of Lisp's syntax and semantics, which means, of course, that I must first address that burning question. . .

### 4.1 What's with All the Parentheses?

Lisp's syntax is quite a bit different from the syntax of languages descended from Algol. The two most immediately obvious characteristics are the extensive use of parentheses and prefix notation. For whatever reason, a lot of folks are put off by this syntax. Lisp's detractors tend to describe the syntax as "weird" and "annoying." Lisp, they say, must stand for Lots of Irritating Superfluous Parentheses. Lisp folks, on the other hand, tend to consider Lisp's syntax one of its great virtues. How is it that what's so off-putting to one group is a source of delight to another?

I can't really make the complete case for Lisp's syntax until I've explained Lisp's macros a bit more thoroughly, but I can start with an historical tidbit that suggests it may be worth keeping an open mind: when John McCarthy first invented Lisp, he intended to implement a more Algol-like syntax, which he called M-expressions. However, he never got around to it. He explained why not in his article "History of Lisp." 1

The project of defining M-expressions precisely and compiling them or at least translating them into S-expressions was neither finalized nor explicitly abandoned. It just receded into the indefinite future, and a new generation of programmers appeared who preferred [S-expressions] to any FORTRAN-like or ALGOL-like notation that could be devised.

In other words, the people who have actually used Lisp over the past 45 years have liked the syntax and have found that it makes the language more powerful. In the next few chapters, you'll begin to see why.

1 [The implementation of LISP](http://www-formal.stanford.edu/jmc/history/lisp/node3.html)

### 4.2 Breaking Open the Black Box

Before we look at the specifics of Lisp's syntax and semantics, it's worth taking a moment to look at how they're defined and how this differs from many other languages.

In most programming languages, the language processor--whether an interpreter or a compiler--operates as a black box: you shove a sequence of characters representing the text of a program into the black box, and it--depending on whether it's an interpreter or a compiler--either executes the behaviors indicated or produces a compiled version of the program that will execute the behaviors when it's run.

Inside the black box, of course, language processors are usually divided into subsystems that are each responsible for one part of the task of translating a program text into behavior or object code. A typical division is to split the processor into three phases, each of which feeds into the next: a lexical analyzer breaks up the stream of characters into tokens and feeds them to a parser that builds a tree representing the expressions in the program, according to the language's grammar. This tree--called an abstract syntax tree--is then fed to an evaluator that either interprets it directly or compiles it into some other language such as machine code. Because the language processor is a black box, the data structures used by the processor, such as the tokens and abstract syntax trees, are of interest only to the language implementer.

In Common Lisp things are sliced up a bit differently, with consequences for both the implementer and for how the language is defined. Instead of a single black box that goes from text to program behavior in one step, Common Lisp defines two black boxes, one that translates text into Lisp objects and another that implements the semantics of the language in terms of those objects. The first box is called the reader, and the second is called the evaluator. 2

Each black box defines one level of syntax. The reader defines how strings of characters can be translated into Lisp objects called s-expressions. 3 Since the s-expression syntax includes syntax for lists of arbitrary objects, including other lists, s-expressions can represent arbitrary tree expressions, much like the abstract syntax tree generated by the parsers for non-Lisp languages.

The evaluator then defines a syntax of Lisp forms that can be built out of s-expressions. Not all s-expressions are legal Lisp forms any more than all sequences of characters are legal s-expressions. For instance, both (foo 1 2) and ("foo" 1 2) are s-expressions, but only the former can be a Lisp form since a list that starts with a string has no meaning as a Lisp form.

This split of the black box has a couple of consequences. One is that you can use s-expressions, as you saw in Chapter 3, as an externalizable data format for data other than source code, using READ to read it and PRINT to print it. 4 The other consequence is that since the semantics of the language are defined in terms of trees of objects rather than strings of characters, it's easier to generate code within the language than it would be if you had to generate code as text. Generating code completely from scratch is only marginally easier--building up lists vs. building up strings is about the same amount of work. The real win, however, is that you can generate code by manipulating existing data. This is the basis for Lisp's macros, which I'll discuss in much more detail in future chapters. For now I'll focus on the two levels of syntax defined by Common Lisp: the syntax of s-expressions understood by the reader and the syntax of Lisp forms understood by the evaluator.

2 Lisp implementers, like implementers of any language, have many ways they can implement an evaluator, ranging from a “pure” interpreter that interprets the objects given to the evaluator directly to a compiler that translates the objects into machine code that it then runs. In the middle are implementations that compile the input into an intermediate form such as bytecodes for a virtual machine and then interprets the bytecodes. Most Common Lisp implementations these days use some form of compilation even when evaluating code at run time.

3 Sometimes the phrase s-expression refers to the textual representation and sometimes to the objects that result from reading the textual representation. Usually either it’s clear from context which is meant or the distinction isn’t that important.

4 Not all Lisp objects can be written out in a way that can be read back in. But anything you can READ can be printed back out “readably” with PRINT.

### 4.3 S-expressions

The basic elements of s-expressions are lists and atoms. Lists are delimited by parentheses and can contain any number of whitespace-separated elements. Atoms are everything else. 5 The elements of lists are themselves s-expressions (in other words, atoms or nested lists). Comments--which aren't, technically speaking, s-expressions--start with a semicolon, extend to the end of a line, and are treated essentially like whitespace.

And that's pretty much it. Since lists are syntactically so trivial, the only remaining syntactic rules you need to know are those governing the form of different kinds of atoms. In this section I'll describe the rules for the most commonly used kinds of atoms: numbers, strings, and names. After that, I'll cover how s-expressions composed of these elements can be evaluated as Lisp forms.

Numbers are fairly straightforward: any sequence of digits--possibly prefaced with a sign (+ or -), containing a decimal point (.) or a solidus (/), or ending with an exponent marker--is read as a number. For example:

```c
123 ; the integer one hundred twenty-three 
3/7 ; the ratio three-sevenths 
1.0 ; the floating-point number one in default precision 
1.0e0 ; another way to write the same floating-point number 
1.0d0 ; the floating-point number one in "double" precision 
1.0e-4 ; the floating-point equivalent to one-ten-thousandth 
+42 ; the integer forty-two 
-42 ; the integer negative forty-two 
-1/4 ; the ratio negative one-quarter 
-2/8 ; another way to write negative one-quarter 
246/2 ; another way to write the integer one hundred twenty-three
```

These different forms represent different kinds of numbers: integers, ratios, and floating point. Lisp also supports complex numbers, which have their own notation and which I'll discuss in Chapter 10.

As some of these examples suggest, you can notate the same number in many ways. But regardless of how you write them, all rationals--integers and ratios--are represented internally in "simplified" form. In other words, the objects that represent -2/8 or 246/2 aren't distinct from the objects that represent -1/4 and 123. Similarly, 1.0 and 1.0e0 are just different ways of writing the same number. On the other hand, 1.0, 1.0d0, and 1 can all denote different objects because the different floating-point representations and integers are different types. We'll save the details about the characteristics of different kinds of numbers for Chapter 10.

Strings literals, as you saw in the previous chapter, are enclosed in double quotes. Within a string a backslash (\) escapes the next character, causing it to be included in the string regardless of what it is. The only two characters that must be escaped within a string are double quotes and the backslash itself. All other characters can be included in a string literal without escaping, regardless of their meaning outside a string. Some example string literals are as follows:

```c
"foo" ; the string containing the characters f, o, and o. 
"fo\o" ; the same string 
"fo\\o" ; the string containing the characters f, o, \, and o. 
"fo\"o" ; the string containing the characters f, o, ", and o.
```

Names used in Lisp programs, such as FORMAT and hello-world, and `*db*` are represented by objects called symbols. The reader knows nothing about how a given name is going to be used--whether it's the name of a variable, a function, or something else. It just reads a sequence of characters and builds an object to represent the name. 6 Almost any character can appear in a name. Whitespace characters can't, though, because the elements of lists are separated by whitespace. Digits can appear in names as long as the name as a whole can't be interpreted as a number. Similarly, names can contain periods, but the reader can't read a name that consists only of periods. Ten characters that serve other syntactic purposes can't appear in names: open and close parentheses, double and single quotes, backtick, comma, colon, semicolon, backslash, and vertical bar. And even those characters can, if you're willing to escape them by preceding the character to be escaped with a backslash or by surrounding the part of the name containing characters that need escaping with vertical bars.

Two important characteristics of the way the reader translates names to symbol objects have to do with how it treats the case of letters in names and how it ensures that the same name is always read as the same symbol. While reading names, the reader converts all unescaped characters in a name to their uppercase equivalents. Thus, the reader will read foo, Foo, and FOO as the same symbol: FOO. However, `\f\o\o` and `|foo|` will both be read as foo, which is a different object than the symbol FOO. This is why when you define a function at the REPL and it prints the name of the function, it's been converted to uppercase. Standard style, these days, is to write code in all lowercase and let the reader change names to uppercase. 7

1『在 lisp 里，变量名都会自动转为大写的。（2020-10-28）』

To ensure that the same textual name is always read as the same symbol, the reader interns symbols--after it has read the name and converted it to all uppercase, the reader looks in a table called a package for an existing symbol with the same name. If it can't find one, it creates a new symbol and adds it to the table. Otherwise, it returns the symbol already in the table. Thus, anywhere the same name appears in any s-expression, the same object will be used to represent it.8

Because names can contain many more characters in Lisp than they can in Algol-derived languages, certain naming conventions are distinct to Lisp, such as the use of hyphenated names like hello-world. Another important convention is that global variables are given names that start and end with `*`. Similarly, constants are given names starting and ending in +. And some programmers will name particularly low-level functions with names that start with `%` or even `%%`. The names defined in the language standard use only the alphabetic characters (A-Z) plus `*, +, -, /, 1, 2, <, =, >,` and &.

1『建议：1）普通变量名采用连字符 `-` 分割单词，但目前自己还是用驼峰形式命名的。2）全局变量前后加上 `*`。3）常量前后加上 `+`。（2020-10-28）』

The syntax for lists, numbers, strings, and symbols can describe a good percentage of Lisp programs. Other rules describe notations for literal vectors, individual characters, and arrays, which I'll cover when I talk about the associated data types in Chapters 10 and 11. For now the key thing to understand is how you can combine numbers, strings, and symbols with parentheses-delimited lists to build s-expressions representing arbitrary trees of objects. Some simple examples look like this:

```c
x ; the symbol X 
() ; the empty list 
(1 2 3) ; a list of three numbers 
("foo" "bar") ; a list of two strings 
(x y z) ; a list of three symbols 
(x 1 "foo") ; a list of a symbol, a number, and a string 
(+ (* 2 3) 4) ; a list of a symbol, a list, and a number.
```

An only slightly more complex example is the following four-item list that contains two symbols, the empty list, and another list, itself containing two symbols and a string:

```c
(defun hello-world () 
  (format t "hello, world")
)
```

5 The empty list, (), which can also be written NIL, is both an atom and a list.

6 In fact, as you’ll see later, names aren’t intrinsically tied to any one kind of thing. You can use the same name, depending on context, to refer to both a variable and a function, not to mention several other possibilities.

7 The case-converting behavior of the reader can, in fact, be customized, but understanding when and how to change it requires a much deeper discussion of the relation between names, symbols, and other program elements than I’m ready to get into just yet.

8 I'll discuss the relation between symbols and packages in more detail in Chapter 21.

### 4.4 S-expressions As Lisp Forms

After the reader has translated a bunch of text into s-expressions, the s-expressions can then be evaluated as Lisp code. Or some of them can--not every s-expressions that the reader can read can necessarily be evaluated as Lisp code. Common Lisp's evaluation rule defines a second level of syntax that determines which s-expressions can be treated as Lisp forms. 9 The syntactic rules at this level are quite simple. Any atom--any nonlist or the empty list--is a legal Lisp form as is any list that has a symbol as its first element. 10

Of course, the interesting thing about Lisp forms isn't their syntax but how they're evaluated. For purposes of discussion, you can think of the evaluator as a function that takes as an argument a syntactically well-formed Lisp form and returns a value, which we can call the value of the form. Of course, when the evaluator is a compiler, this is a bit of a simplification--in that case, the evaluator is given an expression and generates code that will compute the appropriate value when it's run. But this simplification lets me describe the semantics of Common Lisp in terms of how the different kinds of Lisp forms are evaluated by this notional function.

The simplest Lisp forms, atoms, can be divided into two categories: symbols and everything else. A symbol, evaluated as a form, is considered the name of a variable and evaluates to the current value of the variable. 11 I'll discuss in Chapter 6 how variables get their values in the first place. You should also note that certain "variables" are that old oxymoron of programming: "constant variables." For instance, the symbol PI names a constant variable whose value is the best possible floating-point approximation to the mathematical constant pi.

All other atoms--numbers and strings are the kinds you've seen so far--are self-evaluating objects. This means when such an expression is passed to the notional evaluation function, it's simply returned. You saw examples of self-evaluating objects in Chapter 2 when you typed 10 and "hello, world" at the REPL.

It's also possible for symbols to be self-evaluating in the sense that the variables they name can be assigned the value of the symbol itself. Two important constants that are defined this way are T and NIL, the canonical true and false values. I'll discuss their role as booleans in the section "Truth, Falsehood, and Equality."

Another class of self-evaluating symbols are the keyword symbols--symbols whose names start with `:`. When the reader interns such a name, it automatically defines a constant variable with the name and with the symbol as the value.

1-2『这里提到的 symbols whose names start with `:`，目前没看到应用场景，有时间去研究一下。（2020-10-28）』——未完成

Things get more interesting when we consider how lists are evaluated. All legal list forms start with a symbol, but three kinds of list forms are evaluated in three quite different ways. To determine what kind of form a given list is, the evaluator must determine whether the symbol that starts the list is the name of a function, a macro, or a special operator. If the symbol hasn't been defined yet--as may be the case if you're compiling code that contains references to functions that will be defined later--it's assumed to be a function name. 12 I'll refer to the three kinds of forms as function call forms, macro forms, and special forms.

2『三大类 list 的处理方式：函数、宏和操作符。做一张任意卡片。』——已完成

9 Of course, other levels of correctness exist in Lisp, as in other languages. For instance, the s-expression that results from reading `(foo 1 2)` is syntactically well-formed but can be evaluated only if foo is the name of a function or macro.

10 One other rarely used kind of Lisp form is a list whose first element is a lambda form. I’ll discuss this kind of form in Chapter 5.

11 One other possibility exists—it’s possible to define symbol macros that are evaluated slightly differently. We won’t worry about them.

12 In Common Lisp a symbol can name both an operator—function, macro, or special operatorand a variable. This is one of the major differences between Common Lisp and Scheme. The difference is sometimes described as Common Lisp being a Lisp-2 vs. Scheme being a Lisp-1a Lisp-2 has two namespaces, one for operators and one for variables, but a Lisp-1 uses a single namespace. Both choices have advantages, and partisans can debate endlessly which is better.

### 4.5 Function Calls

The evaluation rule for function call forms is simple: evaluate the remaining elements of the list as Lisp forms and pass the resulting values to the named function. This rule obviously places some additional syntactic constraints on a function call form: all the elements of the list after the first must themselves be well-formed Lisp forms. In other words, the basic syntax of a function call form is as follows, where each of the arguments is itself a Lisp form:

```c
(function-name argument*)
```

Thus, the following expression is evaluated by first evaluating 1, then evaluating 2, and then passing the resulting values to the + function, which returns 3:

```c
(+ 1 2)
```

A more complex expression such as the following is evaluated in similar fashion except that evaluating the arguments (+ 1 2) and (- 3 4) entails first evaluating their arguments and applying the appropriate functions to them:

```c
(* (+ 1 2) (- 3 4))
```

Eventually, the values 3 and -1 are passed to the `*` function, which returns -3.

As these examples show, functions are used for many of the things that require special syntax in other languages. This helps keep Lisp's syntax regular.

### 4.6 Special Operators

That said, not all operations can be defined as functions. Because all the arguments to a function are evaluated before the function is called, there's no way to write a function that behaves like the IF operator you used in Chapter 3. To see why, consider this form:

```c
(if x 
  (format t "yes") 
  (format t "no")
)
```

If IF were a function, the evaluator would evaluate the argument expressions from left to right. The symbol x would be evaluated as a variable yielding some value; then `(format t "yes")` would be evaluated as a function call, yielding NIL after printing "yes" to standard output. Then `(format t "no")` would be evaluated, printing "no" and also yielding NIL. Only after all three expressions were evaluated would the resulting values be passed to IF, too late for it to control which of the two FORMAT expressions gets evaluated.

1『这里收获一个知识点：lisp 中调用函数语句的执行顺序，都是先执行（计算）形参列表里的 list 语句，在把结果传递给函数名所指向的函数。（2020-10-28）』

To solve this problem, Common Lisp defines a couple dozen so-called special operators, IF being one, that do things that functions can't do. There are 25 in all, but only a small handful are used directly in day-to-day programming. 13

When the first element of a list is a symbol naming a special operator, the rest of the expressions are evaluated according to the rule for that operator.

The rule for IF is pretty easy: evaluate the first expression. If it evaluates to non-NIL, then evaluate the next expression and return its value. Otherwise, return the value of evaluating the third expression or NIL if the third expression is omitted. In other words, the basic form of an IF expression is as follows:

```c
(if test-form then-form [ else-form ])
```

The test-form will always be evaluated and then one or the other of the then-form or else-form. An even simpler special operator is QUOTE, which takes a single expression as its "argument" and simply returns it, unevaluated. For instance, the following evaluates to the list (+ 1 2), not the value 3:

```c
(quote (+ 1 2))
```

There's nothing special about this list; you can manipulate it just like any list you could create with the LIST function. 14

QUOTE is used commonly enough that a special syntax for it is built into the reader. Instead of writing the following:

```c
(quote (+ 1 2))
```

you can write this:

```c
'(+ 1 2)
```

1-2『特殊符号，撇号 `'` 的含义及使用，做一张术语卡片。下面注释 14 里也提到，用这种形式创建的 list 里，各个元素是只能是常量，不能变的元素，否者就乖乖用 `list` 语句来创建 list 数据类型。（2020-10-28）』——已完成

This syntax is a small extension of the s-expression syntax understood by the reader. From the point of view of the evaluator, both those expressions will look the same: a list whose first element is the symbol QUOTE and whose second element is the list (+ 1 2). 15

In general, the special operators implement features of the language that require some special processing by the evaluator. For instance, several special operators manipulate the environment in which other forms will be evaluated. One of these, which I'll discuss in detail in Chapter 6, is LET, which is used to create new variable bindings. The following form evaluates to 10 because the second x is evaluated in an environment where it's the name of a variable established by the LET with the value 10:

```c
(let ((x 10)) x)
```

The others provide useful, but somewhat esoteric, features. I’ll discuss them as the features they support come up.

13 The others provide useful, but somewhat esoteric, features. I’ll discuss them as the features they support come up.

14 Well, one difference exists—literal objects such as quoted lists, but also including double-quoted strings, literal arrays, and vectors (whose syntax you’ll see later), must not be modified. Consequently, any lists you plan to manipulate you should create with LIST.

15 This syntax is an example of a reader macro. Reader macros modify the syntax the reader uses to translate text into Lisp objects. It is, in fact, possible to define your own reader macros, but that’s a rarely used facility of the language. When most Lispers talk about “extending the syntax” of the language, they’re talking about regular macros, as I'll discuss in a moment.

### 4.7 Macros

While special operators extend the syntax of Common Lisp beyond what can be expressed with just function calls, the set of special operators is fixed by the language standard. Macros, on the other hand, give users of the language a way to extend its syntax. As you saw in Chapter 3, a macro is a function that takes s-expressions as arguments and returns a Lisp form that's then evaluated in place of the macro form. The evaluation of a macro form proceeds in two phases: First, the elements of the macro form are passed, unevaluated, to the macro function. Second, the form returned by the macro function--called its expansion--is evaluated according to the normal evaluation rules.

It's important to keep the two phases of evaluating a macro form clear in your mind. It's easy to lose track when you're typing expressions at the REPL because the two phases happen one after another and the value of the second phase is immediately returned. But when Lisp code is compiled, the two phases happen at completely different times, so it's important to keep clear what's happening when. For instance, when you compile a whole file of source code with the function COMPILE-FILE, all the macro forms in the file are recursively expanded until the code consists of nothing but function call forms and special forms. This macroless code is then compiled into a FASL file that the LOAD function knows how to load. The compiled code, however, isn't executed until the file is loaded. Because macros generate their expansion at compile time, they can do relatively large amounts of work generating their expansion without having to pay for it when the file is loaded or the functions defined in the file are called.

Since the evaluator doesn't evaluate the elements of the macro form before passing them to the macro function, they don't need to be well-formed Lisp forms. Each macro assigns a meaning to the s-expressions in the macro form by virtue of how it uses them to generate its expansion. In other words, each macro defines its own local syntax. For instance, the backwards macro from Chapter 3 defines a syntax in which an expression is a legal backwards form if it's a list that's the reverse of a legal Lisp form.

I'll talk quite a bit more about macros throughout this book. For now the important thing for you to realize is that macros--while syntactically similar to function calls--serve quite a different purpose, providing a hook into the compiler. 16

16 People without experience using Lisp’s macros or, worse yet, bearing the scars of C preprocessorinflicted wounds, tend to get nervous when they realize that macro calls look like regular function calls. This turns out not to be a problem in practice for several reasons. One is that macro forms are usually formatted differently than function calls. For instance, you write the following:

```c
(dolist (x foo) 
  (print x))
```

rather than this:

```c
(dolist (x foo) (print x))
```

or this:

```c
(dolist (x foo) 
            (print x))
```

the way you would if DOLIST was a function. A good Lisp environment will automatically format macro calls correctly, even for user-defined macros. And even if a DOLIST form was written on a single line, there are several clues that it’s a macro. For one, the expression (x foo) is meaningful by itself only if x is the name of a function or macro. Combine that with the later occurrence of x as a variable, and it’s pretty suggestive that DOLIST is a macro that’s creating a binding for a variable named x. Naming conventions also helplooping constructs, which are invariably macros, are frequently given names starting with do.

### 4.8 Truth, Falsehood, and Equality

Two last bits of basic knowledge you need to get under your belt are Common Lisp's notion of truth and falsehood and what it means for two Lisp objects to be "equal." Truth and falsehood are--in this realm--straightforward: the symbol NIL is the only false value, and everything else is true. The symbol T is the canonical true value and can be used when you need to return a non-NIL value and don't have anything else handy. The only tricky thing about NIL is that it's the only object that's both an atom and a list: in addition to falsehood, it's also used to represent the empty list. 17 This equivalence between NIL and the empty list is built into the reader: if the reader sees (), it reads it as the symbol NIL. They're completely interchangeable. And because NIL, as I mentioned previously, is the name of a constant variable with the symbol NIL as its value, the expressions nil, (), 'nil, and '() all evaluate to the same thing--the unquoted forms are evaluated as a reference to the constant variable whose value is the symbol NIL, but in the quoted forms the QUOTE special operator evaluates to the symbol directly. For the same reason, both t and 't will evaluate to the same thing: the symbol T.

1-2『意外的一个收获：nil 既是一个 atom 也是一个 list。所以它能用来表示空列表。nil 做一张术语卡片。』——已完成

Using phrases such as "the same thing" of course begs the question of what it means for two values to be "the same." As you'll see in future chapters, Common Lisp provides a number of type-specific equality predicates: `=` is used to compare numbers, `CHAR=` to compare characters, and so on. In this section I'll discuss the four "generic" equality predicates--functions that can be passed any two Lisp objects and will return true if they're equivalent and false otherwise. They are, in order of discrimination, EQ, EQL, EQUAL, and EQUALP.

EQ tests for "object identity"--two objects are EQ if they're identical. Unfortunately, the object identity of numbers and characters depends on how those data types are implemented in a particular Lisp. Thus, EQ may consider two numbers or two characters with the same value to be equivalent, or it may not. Implementations have enough leeway that the expression `(eq 3 3)` can legally evaluate to either true or false. More to the point, `(eq x x)` can evaluate to either true or false if the value of x happens to be a number or character.

Thus, you should never use EQ to compare values that may be numbers or characters. It may seem to work in a predictable way for certain values in a particular implementation, but you have no guarantee that it will work the same way if you switch implementations. And switching implementations may mean simply upgrading your implementation to a new version--if your Lisp implementer changes how they represent numbers or characters, the behavior of EQ could very well change as well.

Thus, Common Lisp defines EQL to behave like EQ except that it also is guaranteed to consider two objects of the same class representing the same numeric or character value to be equivalent. Thus, (eql 1 1) is guaranteed to be true. And (eql 1 1.0) is guaranteed to be false since the integer value 1 and the floating-point value are instances of different classes.

There are two schools of thought about when to use EQ and when to use EQL: The "use EQ when possible" camp argues you should use EQ when you know you aren't going to be com-paring numbers or characters because (a) it's a way to indicate that you aren't going to be comparing numbers or characters and (b) it will be marginally more efficient since EQ doesn't have to check whether its arguments are numbers or characters.

The "always use EQL" camp says you should never use EQ because (a) the potential gain in clarity is lost because every time someone reading your code--including you--sees an EQ, they have to stop and check whether it's being used correctly (in other words, that it's never going to be called upon to compare numbers or characters) and (b) that the efficiency difference between EQ and EQL is in the noise compared to real performance bottlenecks.

The code in this book is written in the "always use EQL" style. 18

The other two equality predicates, EQUAL and EQUALP, are general in the sense that they can operate on all types of objects, but they're much less fundamental than EQ or EQL. They each define a slightly less discriminating notion of equivalence than EQL, allowing different objects to be considered equivalent. There's nothing special about the particular notions of equivalence these functions implement except that they've been found to be handy by Lisp programmers in the past. If these predicates don't suit your needs, you can always define your own predicate function that compares different types of objects in the way you need.

EQUAL loosens the discrimination of EQL to consider lists equivalent if they have the same structure and contents, recursively, according to EQUAL. EQUAL also considers strings equivalent if they contain the same characters. It also defines a looser definition of equivalence than EQL for bit vectors and pathnames, two data types I'll discuss in future chapters. For all other types, it falls back on EQL.

EQUALP is similar to EQUAL except it's even less discriminating. It considers two strings equivalent if they contain the same characters, ignoring differences in case. It also considers two characters equivalent if they differ only in case. Numbers are equivalent under EQUALP if they represent the same mathematical value. Thus, (equalp 1 1.0) is true. Lists with EQUALP elements are EQUALP; likewise, arrays with EQUALP elements are EQUALP. As with EQUAL, there are a few other data types that I haven't covered yet for which EQUALP can consider two objects equivalent that neither EQL nor EQUAL will. For all other data types, EQUALP falls back on EQL.

17 Using the empty list as false is a reflection of Lisp’s heritage as a list-processing language much as the use of the integer 0 as false in C is a reflection of its heritage as a bit-twiddling language. Not all Lisps handle boolean values the same way. Another of the many subtle differences upon which a good Common Lisp vs. Scheme flame war can rage for days is Scheme’s use of a distinct false value #f, which isn’t the same value as either the symbol nil or the empty list, which are also distinct from each other.

18 Even the language standard is a bit ambivalent about which of EQ or EQL should be preferred. Object identity is defined by EQ, but the standard defines the phrase the same when talking about objects to mean EQL unless another predicate is explicitly mentioned. Thus, if you want to be 100 percent technically correct, you can say that (- 3 2) and (- 4 3) evaluate to “the same” object but not that they evaluate to “identical” objects. This is, admittedly, a bit of an angels-onpinheads kind of issue.

### 4.9 Formatting Lisp Code

While code formatting is, strictly speaking, neither a syntactic nor a semantic matter, proper formatting is important to reading and writing code fluently and idiomatically. The key to formatting Lisp code is to indent it properly. The indentation should reflect the structure of the code so that you don't need to count parentheses to see what goes with what. In general, each new level of nesting gets indented a bit more, and, if line breaks are necessary, items at the same level of nesting are lined up. Thus, a function call that needs to be broken up across multiple lines might be written like this:

```c
(some-function arg-with-a-long-name 
                        another-arg-with-an-even-longer-name)
```

Macro and special forms that implement control constructs are typically indented a little differently: the "body" elements are indented two spaces relative to the opening parenthesis of the form. Thus:

```c
(defun print-list (list) 
  (dolist (i list) 
    (format t "item: ~a~%" i)))
```

However, you don't need to worry too much about these rules because a proper Lisp environment such as SLIME will take care of it for you. In fact, one of the advantages of Lisp's regular syntax is that it's fairly easy for software such as editors to know how to indent it. Since the indentation is supposed to reflect the structure of the code and the structure is marked by parentheses, it's easy to let the editor indent your code for you.

In SLIME, hitting Tab at the beginning of each line will cause it to be indented appropriately, or you can re-indent a whole expression by positioning the cursor on the opening parenthesis and typing C-M-q. Or you can re-indent the whole body of a function from anywhere within it by typing C-c M-q.

Indeed, experienced Lisp programmers tend to rely on their editor handling indenting automatically, not just to make their code look nice but to detect typos: once you get used to how code is supposed to be indented, a misplaced parenthesis will be instantly recognizable by the weird indentation your editor gives you. For example, suppose you were writing a function that was supposed to look like this:

```c
(defun foo () 
  (if (test) 
    (do-one-thing) 
    (do-another-thing)))
```

Now suppose you accidentally left off the closing parenthesis after test. Because you don't bother counting parentheses, you quite likely would have added an extra parenthesis at the end of the DEFUN form, giving you this code:

```c
(defun foo () 
  (if (test 
        (do-one-thing) 
        (do-another-thing))))
```

However, if you had been indenting by hitting Tab at the beginning of each line, you wouldn't have code like that. Instead you'd have this:

```c
(defun foo () 
  (if (test 
        (do-one-thing) 
        (do-another-thing))))
```

Seeing the then and else clauses indented way out under the condition rather than just indented slightly relative to the IF shows you immediately that something is awry.

Another important formatting rule is that closing parentheses are always put on the same line as the last element of the list they're closing. That is, don't write this:

```c
(defun foo () 
  (dotimes (i 10) 
    (format t "~d. hello~%" i) 
  ) 
)
```

1『我个人一直采用上面的代码风格。（2020-10-28）』

but instead write this:

```c
(defun foo () 
  (dotimes (i 10) 
    (format t "~d. hello~%" i)))
```

The string of )))s at the end may seem forbidding, but as long your code is properly indented the parentheses should fade away--no need to give them undue prominence by spreading them across several lines.

Finally, comments should be prefaced with one to four semicolons depending on the scope of the comment as follows:

```
;;;; Four semicolons are used for a file header comment. 
;;; A comment with three semicolons will usually be a paragraph
;;; comment that applies to a large section of code that follows, 

(defun foo (x) 
  (dotimes (i x) 
    ;; Two semicolons indicate this comment applies to the code 
    ;; that follows. Note that this comment is indented the same 
    ;; as the code that follows. 
    (some-function-call) 
    (another i) ; this comment applies to this line only 
    (and-another) ; and this is for this line 
    (baz))
  )
)
```

Now you're ready to start looking in greater detail at the major building blocks of Lisp programs, functions, variables, and macros. Up next: functions.

