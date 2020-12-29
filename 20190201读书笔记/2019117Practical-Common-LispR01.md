# 2019117Practical-Common-LispR01

## 记忆时间

## 0301. Practical: A Simple Database

Obviously, before you can start building real software in Lisp, you'll have to learn the language. But let's face it -- you may be thinking, "'Practical Common Lisp,' isn't that an oxymoron? Why should you be expected to bother learning all the details of a language unless it's actually good for something you care about?" So I'll start by giving you a small example of what you can do with Common Lisp. In this chapter you'll write a simple database for keeping track of CDs. You'll use similar techniques in Chapter 27 when you build a database of MP3s for our streaming MP3 server. In fact, you could think of this as part of the MP3 software project -- after all, in order to have a bunch of MP3s to listen to, it might be helpful to be able to keep track of which CDs you have and which ones you need to rip.

In this chapter, I'll cover just enough Lisp as we go along for you to understand how the code works. But I'll gloss over quite a few details. For now you needn't sweat the small stuff -- the next several chapters will cover all the Common Lisp constructs used here, and more, in a much more systematic way.

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

You could use a four-item list, mapping a given position in the list to a given field in the record. However, another flavor of list -- called a property list, or plist for short -- is even more convenient. A plist is a list where every other element, starting with the first, is a symbol that describes what the next element in the list is. I won't get into all the details of exactly what a symbol is right now; basically it's a name. For the symbols that name the fields in the CD database, you can use a particular kind of symbol, called a keyword symbol. A keyword is any name that starts with a colon (:), for instance, :foo. Here's an example of a plist using the keyword symbols :a, :b, and :c as property names:

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

2 Using a global variable also has some drawbacks  --  for instance, you can have only one database at a time. In Chapter 27, with more of the language under your belt, you'll be ready to build a more flexible database. You'll also see, in Chapter 6, how even using a global variable is more flexible in Common Lisp than it may be in other languages.

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

The second argument to FORMAT is a format string that can contain both literal text and directives telling FORMAT things such as how to interpolate the rest of its arguments. Format directives start with `~` (much the way printf's directives start with %). FORMAT understands dozens of directives, each with their own set of options. 3 However, for now I'll just focus on the ones you need to write dump-db.

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

3『这一小结讲了大量 format 函数的信息，目前因为用不到可以跳过，以后遇到使用场景时再研读。（2020-12-22）』

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

1『在 autolisp 里试验过，or 只是一个逻辑或的功能，不能实现这里，前一个语句是 nil 时自动取后一个语句为默认值的功能。比如 `(or nil 0)` 返回的是 `T`。（2020-10-22）回复：完全可以借鉴这里的思想，自己封装一个函数，赞。（2020-12-29）』

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

The SETF macro is Common Lisp's main assignment operator. It sets its first argument to the result of evaluating its second argument. So in load-db the `*db*` variable will contain the object read from the file, namely, the list of lists written by save-db. You do need to be careful about one thing -- load-db clobbers whatever was in `*db*` before the call. So if you've added records with add-record or add-cds that haven't been saved with save-db, you'll lose them.

### 3.6 Querying the Database

Now that you have a way to save and reload the database to go along with a convenient user interface for adding new records, you soon may have enough records that you won't want to be dumping out the whole database just to look at what's in it. What you need is a way to query the database. You might like, for instance, to be able to write something like this:

```c
(select :artist "Dixie Chicks")
```

and get a list of all the records where the artist is the Dixie Chicks. Again, it turns out that the choice of saving the records in a list will pay off.

The function REMOVE-IF-NOT takes a predicate and a list and returns a list containing only the elements of the original list that match the predicate. In other words, it has removed all the elements that don't match the predicate. However, REMOVE-IF-NOT doesn't really remove anything -- it creates a new list, leaving the original list untouched. It's like running grep over a file. The predicate argument can be any function that accepts a single argument and returns a boolean value -- NIL for false and anything else for true.

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

Note that lambda isn't the name of the function -- it's the indicator you're defining an anonymous function. 5 Other than the lack of a name, however, a LAMBDA expression looks a lot like a DEFUN: the word lambda is followed by a parameter list, which is followed by the body of the function.

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

Note how the anonymous function, which contains code that won't run until it's invoked in REMOVE-IF-NOT, can nonetheless refer to the variable artist. In this case the anonymous function doesn't just save you from having to write a regular function -- it lets you write a function that derives part of its meaning -- the value of artist -- from the context in which it's embedded.

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

This is a function that returns a function and one that references a variable that -- it seems -- won't exist after artist-selector returns. 6 It may seem odd now, but it actually works just the way you'd want -- if you call artist-selector with an argument of "Dixie Chicks", you get an anonymous function that matches CDs whose :artist field is "Dixie Chicks", and if you call it with "Lyle Lovett", you get a different function that will match against an :artist field of "Lyle Lovett". So now you can rewrite the call to select like this:

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

### 3.7 Updating Existing Records -- Another Use for WHERE

Now that you've got nice generalized select and where functions, you're in a good position to write the next feature that every database needs -- a way to update particular records. In SQL the update command is used to update a set of records matching a particular where clause. That seems like a good model, especially since you've already got a where-clause generator. In fact, the update function is mostly just the application of a few ideas you've already seen: using a passed-in selector function to choose the records to update and using keyword arguments to specify the values to change. The main new bit is the use of a function MAPCAR that maps over a list, `*db*` in this case, and returns a new list containing the results of calling a function on each item in the original list.

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

One other new bit here is the use of SETF on a complex form such as `(getf row :title)`. I'll discuss SETF in greater detail in Chapter 6, but for now you just need to know that it's a general assignment operator that can be used to assign lots of "places" other than just variables. (It's a coincidence that SETF and GETF have such similar names -- they don't have any special relationship.) For now it's enough to know that after `(setf (getf row :title) title)`, the plist referenced by row will have the value of the variable title following the property name :title. With this update function if you decide that you really dig the Dixie Chicks and that all their albums should go to 11, you can evaluate the following form:

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

The backwards macro thus defines a new language that's a lot like Lisp -- just backward -- that you can drop into anytime simply by wrapping a backward Lisp expression in a call to the backwards macro. And, in a compiled Lisp program, that new language is just as efficient as normal Lisp because all the macro code -- the code that generates the new expression -- runs at compile time. In other words, the compiler will generate exactly the same code whether you write `(backwards ("hello, world" t format))` or `(format t "hello, world")`.

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

This macro uses a variant of , (namely, the ,@) before the call to make-comparisons-list. The ,@ "splices" the value of the following expression -- which must evaluate to a list -- into the enclosing list. You can see the difference between , and ,@ in the following two expressions:

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

Now, an interesting thing has happened. You removed duplication and made the code more efficient and more general at the same time. That's often the way it goes with a well-chosen macro. This makes sense because a macro is just another mechanism for creating abstractions -- abstraction at the syntactic level, and abstractions are by definition more concise ways of expressing underlying generalities. Now the only code in the mini-database that's specific to CDs and the fields in them is in the make-cd, prompt-for-cd, and add-cd functions. In fact, our new where macro would work with any plist-based database.

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

In most programming languages, the language processor -- whether an interpreter or a compiler -- operates as a black box: you shove a sequence of characters representing the text of a program into the black box, and it -- depending on whether it's an interpreter or a compiler -- either executes the behaviors indicated or produces a compiled version of the program that will execute the behaviors when it's run.

Inside the black box, of course, language processors are usually divided into subsystems that are each responsible for one part of the task of translating a program text into behavior or object code. A typical division is to split the processor into three phases, each of which feeds into the next: a lexical analyzer breaks up the stream of characters into tokens and feeds them to a parser that builds a tree representing the expressions in the program, according to the language's grammar. This tree -- called an abstract syntax tree -- is then fed to an evaluator that either interprets it directly or compiles it into some other language such as machine code. Because the language processor is a black box, the data structures used by the processor, such as the tokens and abstract syntax trees, are of interest only to the language implementer.

In Common Lisp things are sliced up a bit differently, with consequences for both the implementer and for how the language is defined. Instead of a single black box that goes from text to program behavior in one step, Common Lisp defines two black boxes, one that translates text into Lisp objects and another that implements the semantics of the language in terms of those objects. The first box is called the reader, and the second is called the evaluator. 2

Each black box defines one level of syntax. The reader defines how strings of characters can be translated into Lisp objects called s-expressions. 3 Since the s-expression syntax includes syntax for lists of arbitrary objects, including other lists, s-expressions can represent arbitrary tree expressions, much like the abstract syntax tree generated by the parsers for non-Lisp languages.

The evaluator then defines a syntax of Lisp forms that can be built out of s-expressions. Not all s-expressions are legal Lisp forms any more than all sequences of characters are legal s-expressions. For instance, both (foo 1 2) and ("foo" 1 2) are s-expressions, but only the former can be a Lisp form since a list that starts with a string has no meaning as a Lisp form.

This split of the black box has a couple of consequences. One is that you can use s-expressions, as you saw in Chapter 3, as an externalizable data format for data other than source code, using READ to read it and PRINT to print it. 4 The other consequence is that since the semantics of the language are defined in terms of trees of objects rather than strings of characters, it's easier to generate code within the language than it would be if you had to generate code as text. Generating code completely from scratch is only marginally easier -- building up lists vs. building up strings is about the same amount of work. The real win, however, is that you can generate code by manipulating existing data. This is the basis for Lisp's macros, which I'll discuss in much more detail in future chapters. For now I'll focus on the two levels of syntax defined by Common Lisp: the syntax of s-expressions understood by the reader and the syntax of Lisp forms understood by the evaluator.

2 Lisp implementers, like implementers of any language, have many ways they can implement an evaluator, ranging from a “pure” interpreter that interprets the objects given to the evaluator directly to a compiler that translates the objects into machine code that it then runs. In the middle are implementations that compile the input into an intermediate form such as bytecodes for a virtual machine and then interprets the bytecodes. Most Common Lisp implementations these days use some form of compilation even when evaluating code at run time.

3 Sometimes the phrase s-expression refers to the textual representation and sometimes to the objects that result from reading the textual representation. Usually either it’s clear from context which is meant or the distinction isn’t that important.

4 Not all Lisp objects can be written out in a way that can be read back in. But anything you can READ can be printed back out “readably” with PRINT.

### 4.3 S-expressions

The basic elements of s-expressions are lists and atoms. Lists are delimited by parentheses and can contain any number of whitespace-separated elements. Atoms are everything else. 5 The elements of lists are themselves s-expressions (in other words, atoms or nested lists). Comments -- which aren't, technically speaking, s-expressions -- start with a semicolon, extend to the end of a line, and are treated essentially like whitespace.

And that's pretty much it. Since lists are syntactically so trivial, the only remaining syntactic rules you need to know are those governing the form of different kinds of atoms. In this section I'll describe the rules for the most commonly used kinds of atoms: numbers, strings, and names. After that, I'll cover how s-expressions composed of these elements can be evaluated as Lisp forms.

Numbers are fairly straightforward: any sequence of digits -- possibly prefaced with a sign (+ or -), containing a decimal point (.) or a solidus (/), or ending with an exponent marker -- is read as a number. For example:

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

As some of these examples suggest, you can notate the same number in many ways. But regardless of how you write them, all rationals -- integers and ratios -- are represented internally in "simplified" form. In other words, the objects that represent -2/8 or 246/2 aren't distinct from the objects that represent -1/4 and 123. Similarly, 1.0 and 1.0e0 are just different ways of writing the same number. On the other hand, 1.0, 1.0d0, and 1 can all denote different objects because the different floating-point representations and integers are different types. We'll save the details about the characteristics of different kinds of numbers for Chapter 10.

Strings literals, as you saw in the previous chapter, are enclosed in double quotes. Within a string a backslash (\) escapes the next character, causing it to be included in the string regardless of what it is. The only two characters that must be escaped within a string are double quotes and the backslash itself. All other characters can be included in a string literal without escaping, regardless of their meaning outside a string. Some example string literals are as follows:

```c
"foo" ; the string containing the characters f, o, and o. 
"fo\o" ; the same string 
"fo\\o" ; the string containing the characters f, o, \, and o. 
"fo\"o" ; the string containing the characters f, o, ", and o.
```

Names used in Lisp programs, such as FORMAT and hello-world, and `*db*` are represented by objects called symbols. The reader knows nothing about how a given name is going to be used -- whether it's the name of a variable, a function, or something else. It just reads a sequence of characters and builds an object to represent the name. 6 Almost any character can appear in a name. Whitespace characters can't, though, because the elements of lists are separated by whitespace. Digits can appear in names as long as the name as a whole can't be interpreted as a number. Similarly, names can contain periods, but the reader can't read a name that consists only of periods. Ten characters that serve other syntactic purposes can't appear in names: open and close parentheses, double and single quotes, backtick, comma, colon, semicolon, backslash, and vertical bar. And even those characters can, if you're willing to escape them by preceding the character to be escaped with a backslash or by surrounding the part of the name containing characters that need escaping with vertical bars.

Two important characteristics of the way the reader translates names to symbol objects have to do with how it treats the case of letters in names and how it ensures that the same name is always read as the same symbol. While reading names, the reader converts all unescaped characters in a name to their uppercase equivalents. Thus, the reader will read foo, Foo, and FOO as the same symbol: FOO. However, `\f\o\o` and `|foo|` will both be read as foo, which is a different object than the symbol FOO. This is why when you define a function at the REPL and it prints the name of the function, it's been converted to uppercase. Standard style, these days, is to write code in all lowercase and let the reader change names to uppercase. 7

1『在 lisp 里，变量名都会自动转为大写的。（2020-10-28）』

To ensure that the same textual name is always read as the same symbol, the reader interns symbols -- after it has read the name and converted it to all uppercase, the reader looks in a table called a package for an existing symbol with the same name. If it can't find one, it creates a new symbol and adds it to the table. Otherwise, it returns the symbol already in the table. Thus, anywhere the same name appears in any s-expression, the same object will be used to represent it.8

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

After the reader has translated a bunch of text into s-expressions, the s-expressions can then be evaluated as Lisp code. Or some of them can -- not every s-expressions that the reader can read can necessarily be evaluated as Lisp code. Common Lisp's evaluation rule defines a second level of syntax that determines which s-expressions can be treated as Lisp forms. 9 The syntactic rules at this level are quite simple. Any atom -- any nonlist or the empty list -- is a legal Lisp form as is any list that has a symbol as its first element. 10

Of course, the interesting thing about Lisp forms isn't their syntax but how they're evaluated. For purposes of discussion, you can think of the evaluator as a function that takes as an argument a syntactically well-formed Lisp form and returns a value, which we can call the value of the form. Of course, when the evaluator is a compiler, this is a bit of a simplification -- in that case, the evaluator is given an expression and generates code that will compute the appropriate value when it's run. But this simplification lets me describe the semantics of Common Lisp in terms of how the different kinds of Lisp forms are evaluated by this notional function.

The simplest Lisp forms, atoms, can be divided into two categories: symbols and everything else. A symbol, evaluated as a form, is considered the name of a variable and evaluates to the current value of the variable. 11 I'll discuss in Chapter 6 how variables get their values in the first place. You should also note that certain "variables" are that old oxymoron of programming: "constant variables." For instance, the symbol PI names a constant variable whose value is the best possible floating-point approximation to the mathematical constant pi.

All other atoms -- numbers and strings are the kinds you've seen so far -- are self-evaluating objects. This means when such an expression is passed to the notional evaluation function, it's simply returned. You saw examples of self-evaluating objects in Chapter 2 when you typed 10 and "hello, world" at the REPL.

It's also possible for symbols to be self-evaluating in the sense that the variables they name can be assigned the value of the symbol itself. Two important constants that are defined this way are T and NIL, the canonical true and false values. I'll discuss their role as booleans in the section "Truth, Falsehood, and Equality."

Another class of self-evaluating symbols are the keyword symbols -- symbols whose names start with `:`. When the reader interns such a name, it automatically defines a constant variable with the name and with the symbol as the value.

1-2『这里提到的 symbols whose names start with `:`，目前没看到应用场景，有时间去研究一下。（2020-10-28）』——未完成

Things get more interesting when we consider how lists are evaluated. All legal list forms start with a symbol, but three kinds of list forms are evaluated in three quite different ways. To determine what kind of form a given list is, the evaluator must determine whether the symbol that starts the list is the name of a function, a macro, or a special operator. If the symbol hasn't been defined yet -- as may be the case if you're compiling code that contains references to functions that will be defined later -- it's assumed to be a function name. 12 I'll refer to the three kinds of forms as function call forms, macro forms, and special forms.

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

While special operators extend the syntax of Common Lisp beyond what can be expressed with just function calls, the set of special operators is fixed by the language standard. Macros, on the other hand, give users of the language a way to extend its syntax. As you saw in Chapter 3, a macro is a function that takes s-expressions as arguments and returns a Lisp form that's then evaluated in place of the macro form. The evaluation of a macro form proceeds in two phases: First, the elements of the macro form are passed, unevaluated, to the macro function. Second, the form returned by the macro function -- called its expansion -- is evaluated according to the normal evaluation rules.

It's important to keep the two phases of evaluating a macro form clear in your mind. It's easy to lose track when you're typing expressions at the REPL because the two phases happen one after another and the value of the second phase is immediately returned. But when Lisp code is compiled, the two phases happen at completely different times, so it's important to keep clear what's happening when. For instance, when you compile a whole file of source code with the function COMPILE-FILE, all the macro forms in the file are recursively expanded until the code consists of nothing but function call forms and special forms. This macroless code is then compiled into a FASL file that the LOAD function knows how to load. The compiled code, however, isn't executed until the file is loaded. Because macros generate their expansion at compile time, they can do relatively large amounts of work generating their expansion without having to pay for it when the file is loaded or the functions defined in the file are called.

Since the evaluator doesn't evaluate the elements of the macro form before passing them to the macro function, they don't need to be well-formed Lisp forms. Each macro assigns a meaning to the s-expressions in the macro form by virtue of how it uses them to generate its expansion. In other words, each macro defines its own local syntax. For instance, the backwards macro from Chapter 3 defines a syntax in which an expression is a legal backwards form if it's a list that's the reverse of a legal Lisp form.

I'll talk quite a bit more about macros throughout this book. For now the important thing for you to realize is that macros -- while syntactically similar to function calls -- serve quite a different purpose, providing a hook into the compiler. 16

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

Two last bits of basic knowledge you need to get under your belt are Common Lisp's notion of truth and falsehood and what it means for two Lisp objects to be "equal." Truth and falsehood are -- in this realm -- straightforward: the symbol NIL is the only false value, and everything else is true. The symbol T is the canonical true value and can be used when you need to return a non-NIL value and don't have anything else handy. The only tricky thing about NIL is that it's the only object that's both an atom and a list: in addition to falsehood, it's also used to represent the empty list. 17 This equivalence between NIL and the empty list is built into the reader: if the reader sees (), it reads it as the symbol NIL. They're completely interchangeable. And because NIL, as I mentioned previously, is the name of a constant variable with the symbol NIL as its value, the expressions nil, (), 'nil, and '() all evaluate to the same thing -- the unquoted forms are evaluated as a reference to the constant variable whose value is the symbol NIL, but in the quoted forms the QUOTE special operator evaluates to the symbol directly. For the same reason, both t and 't will evaluate to the same thing: the symbol T.

1-2『意外的一个收获：nil 既是一个 atom 也是一个 list。所以它能用来表示空列表。nil 做一张术语卡片。』——已完成

Using phrases such as "the same thing" of course begs the question of what it means for two values to be "the same." As you'll see in future chapters, Common Lisp provides a number of type-specific equality predicates: `=` is used to compare numbers, `CHAR=` to compare characters, and so on. In this section I'll discuss the four "generic" equality predicates -- functions that can be passed any two Lisp objects and will return true if they're equivalent and false otherwise. They are, in order of discrimination, EQ, EQL, EQUAL, and EQUALP.

EQ tests for "object identity" -- two objects are EQ if they're identical. Unfortunately, the object identity of numbers and characters depends on how those data types are implemented in a particular Lisp. Thus, EQ may consider two numbers or two characters with the same value to be equivalent, or it may not. Implementations have enough leeway that the expression `(eq 3 3)` can legally evaluate to either true or false. More to the point, `(eq x x)` can evaluate to either true or false if the value of x happens to be a number or character.

Thus, you should never use EQ to compare values that may be numbers or characters. It may seem to work in a predictable way for certain values in a particular implementation, but you have no guarantee that it will work the same way if you switch implementations. And switching implementations may mean simply upgrading your implementation to a new version -- if your Lisp implementer changes how they represent numbers or characters, the behavior of EQ could very well change as well.

Thus, Common Lisp defines EQL to behave like EQ except that it also is guaranteed to consider two objects of the same class representing the same numeric or character value to be equivalent. Thus, (eql 1 1) is guaranteed to be true. And (eql 1 1.0) is guaranteed to be false since the integer value 1 and the floating-point value are instances of different classes.

There are two schools of thought about when to use EQ and when to use EQL: The "use EQ when possible" camp argues you should use EQ when you know you aren't going to be com-paring numbers or characters because (a) it's a way to indicate that you aren't going to be comparing numbers or characters and (b) it will be marginally more efficient since EQ doesn't have to check whether its arguments are numbers or characters.

The "always use EQL" camp says you should never use EQ because (a) the potential gain in clarity is lost because every time someone reading your code -- including you -- sees an EQ, they have to stop and check whether it's being used correctly (in other words, that it's never going to be called upon to compare numbers or characters) and (b) that the efficiency difference between EQ and EQL is in the noise compared to real performance bottlenecks.

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

The string of )))s at the end may seem forbidding, but as long your code is properly indented the parentheses should fade away -- no need to give them undue prominence by spreading them across several lines.

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

## 0501. Functions

After the rules of syntax and semantics, the three most basic components of all Lisp programs are functions, variables and macros. You used all three while building the database in Chapter 3, but I glossed over a lot of the details of how they work and how to best use them. I'll devote the next few chapters to these three topics, starting with functions, which -- like their counterparts in other languages -- provide the basic mechanism for abstracting, well, functionality.

The bulk of Lisp itself consists of functions. More than three quarters of the names defined in the language standard name functions. All the built-in data types are defined purely in terms of what functions operate on them. Even Lisp's powerful object system is built upon a conceptual extension to functions, generic functions, which I'll cover in Chapter 16.

And, despite the importance of macros to The Lisp Way, in the end all real functionality is provided by functions. Macros run at compile time, so the code they generate -- the code that will actually make up the program after all the macros are expanded -- will consist entirely of calls to functions and special operators. Not to mention, macros themselves are also functions, albeit functions that are used to generate code rather than to perform the actions of the program. 1

1 Despite the importance of functions in Common Lisp, it isn’t really accurate to describe it as a functional language. It’s true some of Common Lisp’s features, such as its list manipulation functions, are designed to be used in a body-form* style and that Lisp has a prominent place in the history of functional programming—McCarthy introduced many ideas that are now considered important in functional programming—but Common Lisp was intentionally designed to support many different styles of programming. In the Lisp family, Scheme is the nearest thing to a “pure” functional language, and even it has several features that disqualify it from absolute purity compared to languages such as Haskell and ML.

### 5.1 Defining New Functions

Normally functions are defined using the DEFUN macro. The basic skeleton of a DEFUN looks like this:

```c
(defun name (parameter*) 
  "Optional documentation string." 
  body-form*
)
```

Any symbol can be used as a function name. 2 Usually function names contain only alphabetic characters and hyphens, but other characters are allowed and are used in certain naming conventions. For instance, functions that convert one kind of value to another sometimes use -> in the name. For example, a function to convert strings to widgets might be called `string->widget`. The most important naming convention is the one mentioned in Chapter 2, which is that you construct compound names with hyphens rather than underscores or inner caps. Thus, frob-widget is better Lisp style than either frob_widget or frobWidget.

A function's parameter list defines the variables that will be used to hold the arguments passed to the function when it's called. 3 If the function takes no arguments, the list is empty, written as (). Different flavors of parameters handle required, optional, multiple, and keyword arguments. I'll discuss the details in the next section.

If a string literal follows the parameter list, it's a documentation string that should describe the purpose of the function. When the function is defined, the documentation string will be associated with the name of the function and can later be obtained using the DOCUMENTATION function. 4

Finally, the body of a DEFUN consists of any number of Lisp expressions. They will be evaluated in order when the function is called and the value of the last expression is returned as the value of the function. Or the RETURN-FROM special operator can be used to return immediately from anywhere in a function, as I'll discuss in a moment.

1『真好，common lisp 就有直接从函数体里返回的函数 `return-from`，目前 autolisp 里没找到，所以没法实现多个函数出口啊。（2020-10-28）』

In Chapter 2 we wrote a hello-world function, which looked like this:

```c
(defun hello-world () 
  (format t "hello, world")
)
```

You can now analyze the parts of this function. Its name is hello-world, its parameter list is empty so it takes no arguments, it has no documentation string, and its body consists of one expression.

```c
(format t "hello, world")
```

The following is a slightly more complex function:

```c
(defun verbose-sum (x y) 
  "Sum any two numbers after printing a message." 
  (format t "Summing ~d and ~d.~%" x y) 
  (+ x y)
)
```

This function is named verbose-sum, takes two arguments that will be bound to the parameters x and y, has a documentation string, and has a body consisting of two expressions. The value returned by the call to + becomes the return value of verbose-sum.

2 Well, almost any symbol. It’s undefined what happens if you use any of the names defined in the language standard as a name for one of your own functions. However, as you’ll see in Chapter 21, the Lisp package system allows you to create names in different namespaces, so this isn’t really an issue.

3 Parameter lists are sometimes also called lambda lists because of the historical relationship between Lisp’s notion of functions and the lambda calculus.

4 For example, the following:

```c
(documentation 'foo 'function)
```

returns the documentation string for the function foo. Note, however, that documentation strings are intended for human consumption, not programmatic access. A Lisp implementation isn’t required to store them and is allowed to discard them at any time, so portable programs shouldn’t depend on their presence. In some implementations an implementation-defined variable needs to be set before it will store documentation strings.

### 5.2 Function Parameter Lists

There's not a lot more to say about function names or documentation strings, and it will take a good portion of the rest of this book to describe all the things you can do in the body of a function, which leaves us with the parameter list.

The basic purpose of a parameter list is, of course, to declare the variables that will receive the arguments passed to the function. When a parameter list is a simple list of variable names -- as in verbose-sum -- the parameters are called required parameters. When a function is called, it must be supplied with one argument for every required parameter. Each parameter is bound to the corresponding argument. If a function is called with too few or too many arguments, Lisp will signal an error.

However, Common Lisp's parameter lists also give you more flexible ways of mapping the arguments in a function call to the function's parameters. In addition to required parameters, a function can have optional parameters. Or a function can have a single parameter that's bound to a list containing any extra arguments. And, finally, arguments can be mapped to parameters using keywords rather than position. Thus, Common Lisp's parameter lists provide a convenient solution to several common coding problems.

### 5.3 Optional Parameters

While many functions, like verbose-sum, need only required parameters, not all functions are quite so simple. Sometimes a function will have a parameter that only certain callers will care about, perhaps because there's a reasonable default value. An example is a function that creates a data structure that can grow as needed. Since the data structure can grow, it doesn't matter -- from a correctness point of view -- what the initial size is. But callers who have a good idea how many items they're going to put into the data structure may be able to improve performance by specifying a specific initial size. Most callers, though, would probably rather let the code that implements the data structure pick a good general-purpose value. In Common Lisp you can accommodate both kinds of callers by using an optional parameter; callers who don't care will get a reasonable default, and other callers can provide a specific value. 5

To define a function with optional parameters, after the names of any required parameters, place the symbol `&optional` followed by the names of the optional parameters. A simple example looks like this:

```c
(defun foo (a b &optional c d) 
  (list a b c d)
)
```

When the function is called, arguments are first bound to the required parameters. After all the required parameters have been given values, if there are any arguments left, their values are assigned to the optional parameters. If the arguments run out before the optional parameters do, the remaining optional parameters are bound to the value NIL. Thus, the function defined previously gives the following results:

```c
(foo 1 2) ==> (1 2 NIL NIL) 
(foo 1 2 3) ==> (1 2 3 NIL) 
(foo 1 2 3 4) ==> (1 2 3 4)
```

Lisp will still check that an appropriate number of arguments are passed to the function -- in this case between two and four, inclusive -- and will signal an error if the function is called with too few or too many.

Of course, you'll often want a different default value than NIL. You can specify the default value by replacing the parameter name with a list containing a name and an expression. The expression will be evaluated only if the caller doesn't pass enough arguments to provide a value for the optional parameter. The common case is simply to provide a value as the expression.

```c
(defun foo (a &optional (b 10)) 
  (list a b)
)
```

1『默认值都能实现，赞！（2020-10-28）』

This function requires one argument that will be bound to the parameter a. The second parameter, b, will take either the value of the second argument, if there is one, or 10.

```c
(foo 1 2) ==> (1 2) 
(foo 1) ==> (1 10)
```

Sometimes, however, you may need more flexibility in choosing the default value. You may want to compute a default value based on other parameters. And you can -- the default-value expression can refer to parameters that occur earlier in the parameter list. If you were writing a function that returned some sort of representation of a rectangle and you wanted to make it especially convenient to make squares, you might use an argument list like this:

```c
(defun make-rectangle (width &optional (height width)) ...)
```

which would cause the height parameter to take the same value as the width parameter unless explicitly specified.

Occasionally, it's useful to know whether the value of an optional argument was supplied by the caller or is the default value. Rather than writing code to check whether the value of the parameter is the default (which doesn't work anyway, if the caller happens to explicitly pass the default value), you can add another variable name to the parameter specifier after the default-value expression. This variable will be bound to true if the caller actually supplied an argument for this parameter and NIL otherwise. By convention, these variables are usually named the same as the actual parameter with a "-supplied-p" on the end. For example:

```c
(defun foo (a b &optional (c 3 c-supplied-p)) 
  (list a b c c-supplied-p)
)
```

This gives results like this:

```c
(foo 1 2) ==> (1 2 3 NIL) 
(foo 1 2 3) ==> (1 2 3 T) 
(foo 1 2 4) ==> (1 2 4 T)
```

5 In languages that don’t support optional parameters directly, programmers typically find ways to simulate them. One technique is to use distinguished “no-value” values that the caller can pass to indicate they want the default value of a given parameter. In C, for example, it’s common to use NULL as such a distinguished value. However, such a protocol between the function and its callers is ad hoc—in some functions or for some arguments NULL may be the distinguished value while in other functions or for other arguments the magic value may be -1 or some #defined constant. In languages such as Java that support overloading a single method name with multiple definitions, optional parameters can also be simulated by providing methods with the same name but different numbers of arguments and having the methods with fewer arguments call the “real” method with default values for the missing arguments.

1『上面教你如何来模拟可选形参，在 autolisp 那边试验过，同样的函数名不同个数的形参，系统会自动根据参数个数正确的匹配到对应的函数调用，当时就想利用这个特点来模拟函数的多态行为。（2020-10-28）』

### 5.4 Rest Parameters

Optional parameters are just the thing when you have discrete parameters for which the caller may or may not want to provide values. But some functions need to take a variable number of arguments. Several of the built-in functions you've seen already work this way. FORMAT has two required arguments, the stream and the control string. But after that it needs a variable number of arguments depending on how many values need to be interpolated into the control string. The + function also takes a variable number of arguments -- there's no particular reason to limit it to summing just two numbers; it will sum any number of values. (It even works with zero arguments, returning 0, the identity under addition.) The following are all legal calls of those two functions:

```c
(format t "hello, world") 
(format t "hello, ~a" name) 
(format t "x: ~d y: ~d" x y) 
(+) 
(+ 1) 
(+ 1 2) 
(+ 1 2 3)
```

Obviously, you could write functions taking a variable number of arguments by simply giving them a lot of optional parameters. But that would be incredibly painful -- just writing the parameter list would be bad enough, and that doesn't get into dealing with all the parameters in the body of the function. To do it properly, you'd have to have as many optional parameters as the number of arguments that can legally be passed in a function call. This number is implementation dependent but guaranteed to be at least 50. And in current implementations it ranges from 4,096 to 536,870,911.6 Blech. That kind of mind-bending tedium is definitely not The Lisp Way.

Instead, Lisp lets you include a catchall parameter after the symbol &rest. If a function includes a &rest parameter, any arguments remaining after values have been doled out to all the required and optional parameters are gathered up into a list that becomes the value of the &rest parameter. Thus, the parameter lists for FORMAT and + probably look something like this:

```c
(defun format (stream string &rest values) ...) 
(defun + (&rest numbers) ...)
```

6 The constant CALL-ARGUMENTS-LIMIT tells you the implementation-specific value.

### 5.5 Keyword Parameters

Optional and rest parameters give you quite a bit of flexibility, but neither is going to help you out much in the following situation: Suppose you have a function that takes four optional parameters. Now suppose that most of the places the function is called, the caller wants to provide a value for only one of the four parameters and, further, that the callers are evenly divided as to which parameter they will use.

The callers who want to provide a value for the first parameter are fine -- they just pass the one optional argument and leave off the rest. But all the other callers have to pass some value for between one and three arguments they don't care about. Isn't that exactly the problem optional parameters were designed to solve?

Of course it is. The problem is that optional parameters are still positional -- if the caller wants to pass an explicit value for the fourth optional parameter, it turns the first three optional parameters into required parameters for that caller. Luckily, another parameter flavor, keyword parameters, allow the caller to specify which values go with which parameters.

To give a function keyword parameters, after any required, &optional, and &rest parameters you include the symbol &key and then any number of keyword parameter specifiers, which work like optional parameter specifiers. Here's a function that has only keyword parameters:

```c
(defun foo (&key a b c) 
  (list a b c)
)
```

When this function is called, each keyword parameters is bound to the value immediately following a keyword of the same name. Recall from Chapter 4 that keywords are names that start with a colon and that they're automatically defined as self-evaluating constants.

If a given keyword doesn't appear in the argument list, then the corresponding parameter is assigned its default value, just like an optional parameter. Because the keyword arguments are labeled, they can be passed in any order as long as they follow any required arguments. For instance, foo can be invoked as follows:

```c
(foo) ==> (NIL NIL NIL) 
(foo :a 1) ==> (1 NIL NIL) 
(foo :b 1) ==> (NIL 1 NIL) 
(foo :c 1) ==> (NIL NIL 1) 
(foo :a 1 :c 3) ==> (1 NIL 3) 
(foo :a 1 :b 2 :c 3) ==> (1 2 3) 
(foo :a 1 :c 3 :b 2) ==> (1 2 3)
```

As with optional parameters, keyword parameters can provide a default value form and the name of a supplied-p variable. In both keyword and optional parameters, the default value form can refer to parameters that appear earlier in the parameter list.

```c
(defun foo (&key (a 0) (b 0 b-supplied-p) (c (+ a b))) 
  (list a b c b-supplied-p)
) 

(foo :a 1) ==> (1 0 1 NIL) 
(foo :b 1) ==> (0 1 1 T) 
(foo :b 1 :c 4) ==> (0 1 4 T) 
(foo :a 2 :b 1 :c 4) ==> (2 1 4 T)
```

Also, if for some reason you want the keyword the caller uses to specify the parameter to be different from the name of the actual parameter, you can replace the parameter name with another list containing the keyword to use when calling the function and the name to be used for the parameter. The following definition of foo:

```c
(defun foo (&key ((:apple a)) ((:box b) 0) ((:charlie c) 0 c-supplied-p)) 
  (list a b c c-supplied-p)
)
```

lets the caller call it like this:

```c
(foo :apple 10 :box 20 :charlie 30) ==> (10 20 30 T)
```

This style is mostly useful if you want to completely decouple the public API of the function from the internal details, usually because you want to use short variable names internally but descriptive keywords in the API. It's not, however, very frequently used.

2『经验证 autolisp 里没法实现 key 的形参。（2020-10-28）』

### 5.6 Mixing Different Parameter Types

It's possible, but rare, to use all four flavors of parameters in a single function. Whenever more than one flavor of parameter is used, they must be declared in the order I've discussed them: first the names of the required parameters, then the optional parameters, then the rest parameter, and finally the keyword parameters. Typically, however, in functions that use multiple flavors of parameters, you'll combine required parameters with one other flavor or possibly combine &optional and &rest parameters. The other two combinations, either &optional or &rest parameters combined with &key parameters, can lead to somewhat surprising behavior.

Combining &optional and &key parameters yields surprising enough results that you should probably avoid it altogether. The problem is that if a caller doesn't supply values for all the optional parameters, then those parameters will eat up the keywords and values intended for the keyword parameters. For instance, this function unwisely mixes &optional and &key parameters:

```c
(defun foo (x &optional y &key z) 
  (list x y z)
)
```

If called like this, it works fine:

```c
(foo 1 2 :z 3) ==> (1 2 3)
```

And this is also fine:

```c
(foo 1) ==> (1 nil nil)
```

But this will signal an error:

```c
(foo 1 :z 3) ==> ERROR
```

This is because the keyword :z is taken as a value to fill the optional y parameter, leaving only the argument 3 to be processed. At that point, Lisp will be expecting either a keyword/value pair or nothing and will complain. Perhaps even worse, if the function had had two &optional parameters, this last call would have resulted in the values :z and 3 being bound to the two &optional parameters and the &key parameter z getting the default value NIL with no indication that anything was amiss.

In general, if you find yourself writing a function that uses both &optional and &key parameters, you should probably just change it to use all &key parameters -- they're more flexible, and you can always add new keyword parameters without disturbing existing callers of the function. You can also remove keyword parameters, as long as no one is using them. 7 In general, using keyword parameters helps make code much easier to maintain and evolve -- if you need to add some new behavior to a function that requires new parameters, you can add keyword parameters without having to touch, or even recompile, any existing code that calls the function.

You can safely combine &rest and &key parameters, but the behavior may be a bit surprising initially. Normally the presence of either &rest or &key in a parameter list causes all the values remaining after the required and &optional parameters have been filled in to be processed in a particular way -- either gathered into a list for a &rest parameter or assigned to the appropriate &key parameters based on the keywords. If both &rest and &key appear in a parameter list, then both things happen -- all the remaining values, which include the keywords themselves, are gathered into a list that's bound to the &rest parameter, and the appropriate values are also bound to the &key parameters. So, given this function:

```c
(defun foo (&rest rest &key a b c) 
  (list rest a b c)
)
```

you get this result:

```c
(foo :a 1 :b 2 :c 3) ==> ((:A 1 :B 2 :C 3) 1 2 3)
```

7 Four standard functions take both &optional and &key arguments—READ-FROM-STRING, PARSE-NAMESTRING, WRITE-LINE, and WRITE-STRING. They were left that way during standardization for backward compatibility with earlier Lisp dialects. READ-FROM-STRING tends to be the one that catches new Lisp programmers most frequently—a call such as (read-from-string s :start 10) seems to ignore the :start keyword argument, reading from index 0 instead of 10. That’s because READ-FROM-STRING also has two &optional parameters that swallowed up the arguments :start and 10.

### 5.7 Function Return Values

All the functions you've written so far have used the default behavior of returning the value of the last expression evaluated as their own return value. This is the most common way to return a value from a function.

However, sometimes it's convenient to be able to return from the middle of a function such as when you want to break out of nested control constructs. In such cases you can use the RETURN-FROM special operator to immediately return any value from the function.

You'll see in Chapter 20 that RETURN-FROM is actually not tied to functions at all; it's used to return from a block of code defined with the BLOCK special operator. However, DEFUN automatically wraps the whole function body in a block with the same name as the function. So, evaluating a RETURN-FROM with the name of the function and the value you want to return will cause the function to immediately exit with that value. RETURN-FROM is a special operator whose first "argument" is the name of the block from which to return. This name isn't evaluated and thus isn't quoted.

The following function uses nested loops to find the first pair of numbers, each less than 10, whose product is greater than the argument, and it uses RETURN-FROM to return the pair as soon as it finds it:

```c
(defun foo (n) 
  (dotimes (i 10) 
    (dotimes (j 10) 
      (when (> (* i j) n) 
        (return-from foo (list i j))
      )
    )
  )
)
```

Admittedly, having to specify the name of the function you're returning from is a bit of a pain -- for one thing, if you change the function's name, you'll need to change the name used in the RETURN-FROM as well. 8 But it's also the case that explicit RETURN-FROMs are used much less frequently in Lisp than return statements in C-derived languages, because all Lisp expressions, including control constructs such as loops and conditionals, evaluate to a value. So it's not much of a problem in practice.

8 Another macro, RETURN, doesn’t require a name. However, you can’t use it instead of RETURN-FROM to avoid having to specify the function name; it’s syntactic sugar for returning from a block named NIL. I’ll cover it, along with the details of BLOCK and RETURN-FROM, in Chapter 20.

### 5.8 Functions As Data, a.k.a. Higher-Order Functions

While the main way you use functions is to call them by name, a number of situations exist where it's useful to be able treat functions as data. For instance, if you can pass one function as an argument to another, you can write a general-purpose sorting function while allowing the caller to provide a function that's responsible for comparing any two elements. Then the same underlying algorithm can be used with many different comparison functions. Similarly, callbacks and hooks depend on being able to store references to code in order to run it later. Since functions are already the standard way to abstract bits of code, it makes sense to allow functions to be treated as data. 9

1-2『编程语言里，能把函数当作数据，个人感觉太有必要了，将函数作为参数传进另一个函数，构建复杂的模型。函数作为数据，做一张主题卡。（2020-10-28）』——已完成

In Lisp, functions are just another kind of object. When you define a function with DEFUN, you're really doing two things: creating a new function object and giving it a name. It's also possible, as you saw in Chapter 3, to use LAMBDA expressions to create a function without giving it a name. The actual representation of a function object, whether named or anonymous, is opaque -- in a native-compiling Lisp, it probably consists mostly of machine code. The only things you need to know are how to get hold of it and how to invoke it once you've got it.

The special operator FUNCTION provides the mechanism for getting at a function object. It takes a single argument and returns the function with that name. The name isn't quoted. Thus, if you've defined a function foo, like so:

```c
CL-USER> (defun foo (x) (* 2 x)) 
FOO
```

you can get the function object like this: 10

```c
CL-USER> (function foo) 
#<Interpreted Function FOO>
```

In fact, you've already used FUNCTION, but it was in disguise. The syntax #', which you used in Chapter 3, is syntactic sugar for FUNCTION, just the way ' is syntactic sugar for QUOTE. 11 Thus, you can also get the function object for foo like this:

```c
CL-USER> #'foo 
#<Interpreted Function FOO>
```

1-2『经验证，`#'` 在 autolisp 里无效。（2020-10-28）』

Once you've got the function object, there's really only one thing you can do with it -- invoke it. Common Lisp provides two functions for invoking a function through a function object: FUNCALL and APPLY. 12 They differ only in how they obtain the arguments to pass to the function.

FUNCALL is the one to use when you know the number of arguments you're going to pass to the function at the time you write the code. The first argument to FUNCALL is the function object to be invoked, and the rest of the arguments are passed onto that function. Thus, the following two expressions are equivalent:

```c
(foo 1 2 3) === (funcall #'foo 1 2 3)
```

However, there's little point in using FUNCALL to call a function whose name you know when you write the code. In fact, the previous two expressions will quite likely compile to exactly the same machine instructions.

The following function demonstrates a more apt use of FUNCALL. It accepts a function object as an argument and plots a simple ASCII-art histogram of the values returned by the argument function when it's invoked on the values from min to max, stepping by step.

```c
(defun plot (fn min max step) 
  (loop for i from min to max by step do 
    (loop repeat (funcall fn i) do (format t "*")) 
    (format t "~%")
  )
)
```

The FUNCALL expression computes the value of the function for each value of i. The inner LOOP uses that computed value to determine how many times to print an asterisk to standard output.

Note that you don't use FUNCTION or #' to get the function value of fn; you want it to be interpreted as a variable because it's the variable's value that will be the function object. You can call plot with any function that takes a single numeric argument, such as the built-in function EXP that returns the value of e raised to the power of its argument.

```c
CL-USER> (plot #'exp 0 4 1/2) 
*
*
**
****
*******
NIL
```

FUNCALL, however, doesn't do you any good when the argument list is known only at runtime. For instance, to stick with the plot function for another moment, suppose you've obtained a list containing a function object, a minimum and maximum value, and a step value. In other words, the list contains the values you want to pass as arguments to plot. Suppose this list is in the variable plot-data. You could invoke plot on the values in that list like this:

```c
(plot 
  (first plot-data) 
  (second plot-data) 
  (third plot-data) 
  (fourth plot-data)
)
```

This works fine, but it's pretty annoying to have to explicitly unpack the arguments just so you can pass them to plot.

That's where APPLY comes in. Like FUNCALL, the first argument to APPLY is a function object. But after the function object, instead of individual arguments, it expects a list. It then applies the function to the values in the list. This allows you to write the following instead:

```c
(apply #'plot plot-data)
```

As a further convenience, APPLY can also accept "loose" arguments as long as the last argument is a list. Thus, if plot-data contained just the min, max, and step values, you could still use APPLY like this to plot the EXP function over that range:

```c
(apply #'plot #'exp plot-data)
```

APPLY doesn't care about whether the function being applied takes &optional, &rest, or &key arguments -- the argument list produced by combining any loose arguments with the final list must be a legal argument list for the function with enough arguments for all the required parameters and only appropriate keyword parameters.

9 Lisp, of course, isn’t the only language to treat functions as data. C uses function pointers, Perl uses subroutine references, Python uses a scheme similar to Lisp, and C# introduces delegates, essentially typed function pointers, as an improvement over Java’s rather clunky reflection and anonymous class mechanisms.

10 The exact printed representation of a function object will differ from implementation to implementation.

11 The best way to think of FUNCTION is as a special kind of quotation. QUOTEing a symbol prevents it from being evaluated at all, resulting in the symbol itself rather than the value of the variable named by that symbol. FUNCTION also circumvents the normal evaluation rule but, instead of preventing the symbol from being evaluated at all, causes it to be evaluated as the name of a function, just the way it would if it were used as the function name in a function call expression.

12 There’s actually a third, the special operator MULTIPLE-VALUE-CALL, but I’ll save that for when I discuss expressions that return multiple values in Chapter 20.

### 5.9 Anonymous Functions

Once you start writing, or even simply using, functions that accept other functions as arguments, you're bound to discover that sometimes it's annoying to have to define and name a whole separate function that's used in only one place, especially when you never call it by name.

When it seems like overkill to define a new function with DEFUN, you can create an "anonymous" function using a LAMBDA expression. As discussed in Chapter 3, a LAMBDA expression looks like this:

```c
(lambda (parameters) body)
```

One way to think of LAMBDA expressions is as a special kind of function name where the name itself directly describes what the function does. This explains why you can use a LAMBDA expression in the place of a function name with #'.

```c
(funcall #'(lambda (x y) (+ x y)) 2 3) ==> 5
```

You can even use a LAMBDA expression as the "name" of a function in a function call expression. If you wanted, you could write the previous FUNCALL expression more concisely.

```c
((lambda (x y) (+ x y)) 2 3) ==> 5
```

But this is almost never done; it's merely worth noting that it's legal in order to emphasize that LAMBDA expressions can be used anywhere a normal function name can be.13

Anonymous functions can be useful when you need to pass a function as an argument to another function and the function you need to pass is simple enough to express inline. For instance, suppose you wanted to plot the function 2x. You could define the following function:

```c
(defun double (x) (* 2 x))
```

which you could then pass to plot.

```c
CL-USER> (plot #'double 0 10 1) 
** 
**** 
****** 
******** 
********** 
************ 
************** 
**************** 
****************** 
******************** 
NIL
```

But it's easier, and arguably clearer, to write this:

```c
CL-USER> (plot #'(lambda (x) (* 2 x)) 0 10 1) 
** 
**** 
****** 
******** 
********** 
************ 
************** 
**************** 
****************** 
******************** 
NIL
```

The other important use of LAMBDA expressions is in making closures, functions that capture part of the environment where they're created. You used closures a bit in Chapter 3, but the details of how closures work and what they're used for is really more about how variables work than functions, so I'll save that discussion for the next chapter.

## 0601. Variables

The next basic building block we need to look at are variables. Common Lisp supports two kinds of variables: lexical and dynamic. 1 These two types correspond roughly to "local" and "global" variables in other languages. However, the correspondence is only approximate. On one hand, some languages' "local" variables are in fact much like Common Lisp's dynamic variables. 2 And on the other, some languages' local variables are lexically scoped without providing all the capabilities provided by Common Lisp's lexical variables. In particular, not all languages that provide lexically scoped variables support closures.

To make matters a bit more confusing, many of the forms that deal with variables can be used with both lexical and dynamic variables. So I'll start by discussing a few aspects of Lisp's variables that apply to both kinds and then cover the specific characteristics of lexical and dynamic variables. Then I'll discuss Common Lisp's general-purpose assignment operator, SETF, which is used to assign new values to variables and just about every other place that can hold a value.

1『晕死，这里才突然意识到，command lisp 里的 `setf` 如同 autolisp 里的 `setq`。（2020-11-03）』

1 Dynamic variables are also sometimes called special variables for reasons you’ll see later in this chapter. It’s important to be aware of this synonym, as some folks (and Lisp implementations) use one term while others use the other.

2 Early Lisps tended to use dynamic variables for local variables, at least when interpreted. Elisp, the Lisp dialect used in Emacs, is a bit of a throwback in this respect, continuing to support only dynamic variables. Other languages have recapitulated this transition from dynamic to lexical variables—Perl’s local variables, for instance, are dynamic while its my variables, introduced in Perl 5, are lexical. Python never had true dynamic variables but only introduced true lexical scoping in version 2.2. (Python’s lexical variables are still somewhat limited compared to Lisp’s because of the conflation of assignment and binding in the language’s syntax.)

### 6.1 Variable Basics

As in other languages, in Common Lisp variables are named places that can hold a value. However, in Common Lisp, variables aren't typed the way they are in languages such as Java or C++. That is, you don't need to declare the type of object that each variable can hold. Instead, a variable can hold values of any type and the values carry type information that can be used to check types at runtime. Thus, Common Lisp is dynamically typed -- type errors are detected dynamically. For instance, if you pass something other than a number to the + function, Common Lisp will signal a type error. On the other hand, Common Lisp is a strongly typed language in the sense that all type errors will be detected -- there's no way to treat an object as an instance of a class that it's not. 3

1-2『这里又见「动态语言」的概念，做一张术语卡片。』——已完成

All values in Common Lisp are, conceptually at least, references to objects. 4 Consequently, assigning a variable a new value changes what object the variable refers to but has no effect on the previously referenced object. However, if a variable holds a reference to a mutable object, you can use that reference to modify the object, and the modification will be visible to any code that has a reference to the same object.

One way to introduce new variables you've already used is to define function parameters. As you saw in the previous chapter, when you define a function with DEFUN, the parameter list defines the variables that will hold the function's arguments when it's called. For example, this function defines three variables -- x, y, and z -- to hold its arguments.

```c
(defun foo (x y z) 
  (+ x y z)
)
```

Each time a function is called, Lisp creates new bindings to hold the arguments passed by the function's caller. A binding is the runtime manifestation of a variable. A single variable -- the thing you can point to in the program's source code -- can have many different bindings during a run of the program. A single variable can even have multiple bindings at the same time; parameters to a recursive function, for example, are rebound for each call to the function.

As with all Common Lisp variables, function parameters hold object references. 5 Thus, you can assign a new value to a function parameter within the body of the function, and it will not affect the bindings created for another call to the same function. But if the object passed to a function is mutable and you change it in the function, the changes will be visible to the caller since both the caller and the callee will be referencing the same object.

1『看到这里提到的「可变」，渐渐对「不可变性」有那么一点点感觉了。（2020-11-03）』

Another form that introduces new variables is the LET special operator. The skeleton of a LET form looks like this:

```c
(let (variable*) 
  body-form*
)
```

where each variable is a variable initialization form. Each initialization form is either a list containing a variable name and an initial value form or -- as a shorthand for initializing the variable to NIL -- a plain variable name. The following LET form, for example, binds the three variables x, y, and z with initial values 10, 20, and NIL:

```c
(let ((x 10) (y 20) z) 
  ...
)
```

When the LET form is evaluated, all the initial value forms are first evaluated. Then new bindings are created and initialized to the appropriate initial values before the body forms are executed. Within the body of the LET, the variable names refer to the newly created bindings. After the LET, the names refer to whatever, if anything, they referred to before the LET.

The value of the last expression in the body is returned as the value of the LET expression. Like function parameters, variables introduced with LET are rebound each time the LET is entered. 6

The scope of function parameters and LET variables -- the area of the program where the variable name can be used to refer to the variable's binding -- is delimited by the form that introduces the variable. This form -- the function definition or the LET -- is called the binding form. As you'll see in a bit, the two types of variables -- lexical and dynamic -- use two slightly different scoping mechanisms, but in both cases the scope is delimited by the binding form.

If you nest binding forms that introduce variables with the same name, then the bindings of the innermost variable shadows the outer bindings. For instance, when the following function is called, a binding is created for the parameter x to hold the function's argument. Then the first LET creates a new binding with the initial value 2, and the inner LET creates yet another binding, this one with the initial value 3. The bars on the right mark the scope of each binding.

```c
(defun foo (x) ; x is argument
  (format t "Parameter: ~a~%" x) 
  (let ((x 2)) ; x is 2 
    (format t "Outer LET: ~a~%" x) 
    (let ((x 3)) ; x is 3 
      (format t "Inner LET: ~a~%" x)
    ) 
    (format t "Outer LET: ~a~%" x)
  )
  (format t "Parameter: ~a~%" x)
) 
```

Each reference to x will refer to the binding with the smallest enclosing scope. Once control leaves the scope of one binding form, the binding from the immediately enclosing scope is unshadowed and x refers to it instead. Thus, calling foo results in this output:

```c
CL-USER> (foo 1) 
Parameter: 1 
Outer LET: 2 
Inner LET: 3 
Outer LET: 2 
Parameter: 1 
NIL
```

In future chapters I'll discuss other constructs that also serve as binding forms -- any construct that introduces a new variable name that's usable only within the construct is a binding form.

For instance, in Chapter 7 you'll meet the DOTIMES loop, a basic counting loop. It introduces a variable that holds the value of a counter that's incremented each time through the loop. The following loop, for example, which prints the numbers from 0 to 9, binds the variable x:

```c
(dotimes (x 10) 
  (format t "~d " x)
)
```

Another binding form is a variant of LET, `LET*.` The difference is that in a LET, the variable names can be used only in the body of the LET -- the part of the LET after the variables list -- but in a `LET*`, the initial value forms for each variable can refer to variables introduced earlier in the variables list. Thus, you can write the following:

```c
(let* ((x 10) 
       (y (+ x 10))) 
  (list x y)
)
```

but not this:

```c
(let ((x 10) 
      (y (+ x 10))) 
  (list x y)
)
```

However, you could achieve the same result with nested LETs.

```c
(let ((x 10)) 
  (let ((y (+ x 10))) 
    (list x y)
  )
)
```

3 Actually, it’s not quite true to say that all type errors will always be detected—it’s possible to use optional declarations to tell the compiler that certain variables will always contain objects of a particular type and to turn off runtime type checking in certain regions of code. However, declarations of this sort are used to optimize code after it has been developed and debugged, not during normal development.

4 As an optimization certain kinds of objects, such as integers below a certain size and characters, may be represented directly in memory where other objects would be represented by a pointer to the actual object. However, since integers and characters are immutable, it doesn’t matter that there may be multiple copies of “the same” object in different variables. This is the root of the difference between EQ and EQL discussed in Chapter 4.

1『这里又见到「不可变性」，函数式编程里核心的一个概念。上面提到的，整数和字符串在 lisp 里是不可变型的数据类型，但作为变量，整数是可以赋值不同的数的啊，难道是分配给整数的内存空间只能放整数的意思？所以说目前还是不太明白其不变性。（2020-11-03）』

5 In compiler-writer terms Common Lisp functions are “pass-by-value.” However, the values that are passed are references to objects. This is similar to how Java and Python work.

6 The variables in LET forms and function parameters are created by exactly the same mechanism. In fact, in some Lisp dialects—though not Common Lisp—LET is simply a macro that expands into a call to an anonymous function. That is, in those dialects, the following:

```c
(let ((x 10)) (format t "~a" x))
```

is a macro form that expands into this:

```c
((lambda (x) (format t "~a" x)) 10)
```

### 6.2 Lexical Variables and Closures

By default all binding forms in Common Lisp introduce lexically scoped variables. Lexically scoped variables can be referred to only by code that's textually within the binding form. Lexical scoping should be familiar to anyone who has programmed in Java, C, Perl, or Python since they all provide lexically scoped "local" variables. For that matter, Algol programmers should also feel right at home, as Algol first introduced lexical scoping in the 1960s.

However, Common Lisp's lexical variables are lexical variables with a twist, at least compared to the original Algol model. The twist is provided by the combination of lexical scoping with nested functions. By the rules of lexical scoping, only code textually within the binding form can refer to a lexical variable. But what happens when an anonymous function contains a reference to a lexical variable from an enclosing scope? For instance, in this expression:

```c
(let ((count 0)) #'(lambda () (setf count (1+ count))))
```

the reference to count inside the LAMBDA form should be legal according to the rules of lexical scoping. Yet the anonymous function containing the reference will be returned as the value of the LET form and can be invoked, via FUNCALL, by code that's not in the scope of the LET. So what happens? As it turns out, when count is a lexical variable, it just works. The binding of count created when the flow of control entered the LET form will stick around for as long as needed, in this case for as long as someone holds onto a reference to the function object returned by the LET form. The anonymous function is called a closure because it "closes over" the binding created by the LET.

1-2『又见闭包 closure，不过这里目前介绍的闭包概念没弄明白。做一张术语卡片。（2020-11-03）』——已完成

The key thing to understand about closures is that it's the binding, not the value of the variable, that's captured. Thus, a closure can not only access the value of the variables it closes over but can also assign new values that will persist between calls to the closure. For instance, you can capture the closure created by the previous expression in a global variable like this:

```c
(defparameter *fn* 
  (let ((count 0)) 
       #'(lambda () (setf count (1+ count)))
  )
)
```

Then each time you invoke it, the value of count will increase by one.

```c
CL-USER> (funcall *fn*) 
1 
CL-USER> (funcall *fn*) 
2 
CL-USER> (funcall *fn*) 
3
```

A single closure can close over many variable bindings simply by referring to them. Or multiple closures can capture the same binding. For instance, the following expression returns a list of three closures, one that increments the value of the closed over count binding, one that decrements it, and one that returns the current value:

```c
(let ((count 0)) 
  (list 
    #'(lambda () (incf count)) 
    #'(lambda () (decf count)) 
    #'(lambda () count)
  )
)
```

### 6.3 Dynamic, a.k.a. Special, Variables

Lexically scoped bindings help keep code understandable by limiting the scope, literally, in which a given name has meaning. This is why most modern languages use lexical scoping for local variables. Sometimes, however, you really want a global variable -- a variable that you can refer to from anywhere in your program. While it's true that indiscriminate use of global variables can turn code into spaghetti nearly as quickly as unrestrained use of goto, global variables do have legitimate uses and exist in one form or another in almost every programming language. 7 And as you'll see in a moment, Lisp's version of global variables, dynamic variables, are both more useful and more manageable.

Common Lisp provides two ways to create global variables: DEFVAR and DEFPARAMETER. Both forms take a variable name, an initial value, and an optional documentation string. After it has been DEFVARed or DEFPARAMETERed, the name can be used anywhere to refer to the current binding of the global variable. As you've seen in previous chapters, global variables are conventionally named with names that start and end with `*`. You'll see later in this section why it's quite important to follow that naming convention. Examples of DEFVAR and DEFPARAMETER look like this:

```c
(defvar *count* 0 "Count of widgets made so far.") 
(defparameter *gap-tolerance* 0.001 "Tolerance to be allowed in widget gaps.")
```

The difference between the two forms is that DEFPARAMETER always assigns the initial value to the named variable while DEFVAR does so only if the variable is undefined. A DEFVAR form can also be used with no initial value to define a global variable without giving it a value. Such a variable is said to be unbound.

Practically speaking, you should use DEFVAR to define variables that will contain data you'd want to keep even if you made a change to the source code that uses the variable. For instance, suppose the two variables defined previously are part of an application for controlling a widget factory. It's appropriate to define the `*count*` variable with DEFVAR because the number of widgets made so far isn't invalidated just because you make some changes to the widget-making code. 8

On the other hand, the variable `*gap-tolerance*` presumably has some effect on the behavior of the widget-making code itself. If you decide you need a tighter or looser tolerance and change the value in the DEFPARAMETER form, you'd like the change to take effect when you recompile and reload the file.

After defining a variable with DEFVAR or DEFPARAMETER, you can refer to it from anywhere. For instance, you might define this function to increment the count of widgets made:

```c
(defun increment-widget-count () 
  (incf *count*)
)
```

The advantage of global variables is that you don't have to pass them around. Most languages store the standard input and output streams in global variables for exactly this reason -- you never know when you're going to want to print something to standard out, and you don't want every function to have to accept and pass on arguments containing those streams just in case someone further down the line needs them.

However, once a value, such as the standard output stream, is stored in a global variable and you have written code that references that global variable, it's tempting to try to temporarily modify the behavior of that code by changing the variable's value.

For instance, suppose you're working on a program that contains some low-level logging functions that print to the stream in the global variable `*standard-output*`. Now suppose that in part of the program you want to capture all the output generated by those functions into a file. You might open a file and assign the resulting stream to `*standard-output*`. Now the low-level functions will send their output to the file.

This works fine until you forget to set `*standard-output*` back to the original stream when you're done. If you forget to reset `*standard-output*`, all the other code in the program that uses `*standard-output*` will also send its output to the file. 9

What you really want, it seems, is a way to wrap a piece of code in something that says, "All code below here -- all the functions it calls, all the functions they call, and so on, down to the lowest-level functions -- should use this value for the global variable `*standard-output*`." Then when the high-level function returns, the old value of `*standard-output*` should be automatically restored.

It turns out that that's exactly what Common Lisp's other kind of variable -- dynamic variables -- let you do. When you bind a dynamic variable -- for example, with a LET variable or a function parameter -- the binding that's created on entry to the binding form replaces the global binding for the duration of the binding form. Unlike a lexical binding, which can be referenced by code only within the lexical scope of the binding form, a dynamic binding can be referenced by any code that's invoked during the execution of the binding form.10 And it turns out that all global variables are, in fact, dynamic variables.

1『上面信息目前的理解，在 Common Lisp 里 dynamic variables 是结合了局部变量和全局变量的优点，而且还能避免全局变量时常忘记重置的缺点。（2020-11-08）』

Thus, if you want to temporarily redefine `*standard-output*`, the way to do it is simply to rebind it, say, with a LET.

```c
(let ((*standard-output* *some-other-stream*)) (stuff))
```

In any code that runs as a result of the call to stuff, references to `*standard-output*` will use the binding established by the LET. And when stuff returns and control leaves the LET, the new binding of `*standard-output*` will go away and subsequent references to `*standard-output*` will see the binding that was current before the LET. At any given time, the most recently established binding shadows all other bindings. Conceptually, each new binding for a given dynamic variable is pushed onto a stack of bindings for that variable, and references to the variable always use the most recent binding. As binding forms return, the bindings they created are popped off the stack, exposing previous bindings. 11

A simple example shows how this works.

```c
(defvar *x* 10) 
(defun foo () (format t "X: ~d~%" *x*))
```

The DEFVAR creates a global binding for the variable `*x*` with the value 10. The reference to `*x*` in foo will look up the current binding dynamically. If you call foo from the top level, the global binding created by the DEFVAR is the only binding available, so it prints 10.

```c
CL-USER> (foo) 
X: 10 
NIL
```

But you can use LET to create a new binding that temporarily shadows the global binding, and foo will print a different value.

```c
CL-USER> (let ((*x* 20)) (foo)) 
X: 20 
NIL
```

Now call foo again, with no LET, and it again sees the global binding.

```c
CL-USER> (foo) 
X: 10 
NIL
```

Now define another function.

```c
(defun bar () (foo) (let ((*x* 20)) (foo)) (foo))
```

Note that the middle call to foo is wrapped in a LET that binds `*x*` to the new value 20. When you run bar, you get this result:

```c
CL-USER> (bar) 
X: 10 
X: 20 
X: 10 
NIL
```

As you can see, the first call to foo sees the global binding, with its value of 10. The middle call, however, sees the new binding, with the value 20. But after the LET, foo once again sees the global binding.

As with lexical bindings, assigning a new value affects only the current binding. To see this, you can redefine foo to include an assignment to `*x*`.

```c
(defun foo () 
  (format t "Before assignment~18tX: ~d~%" *x*) 
  (setf *x* (+ 1 *x*)) 
  (format t "After assignment~18tX: ~d~%" *x*)
)
```

Now foo prints the value of `*x*`, increments it, and prints it again. If you just run foo, you'll see this:

```c
CL-USER> (foo) 
Before assignment X: 10 
After assignment X: 11 
NIL
```

Not too surprising. Now run bar.

```c
CL-USER> (bar) 
Before assignment X: 11 
After assignment X: 12 
Before assignment X: 20 
After assignment X: 21 
Before assignment X: 12 
After assignment X: 13 
NIL
```

Notice that `*x*` started at 11 -- the earlier call to foo really did change the global value. The first call to foo from bar increments the global binding to 12. The middle call doesn't see the global binding because of the LET. Then the last call can see the global binding again and increments it from 12 to 13.

So how does this work? How does LET know that when it binds `*x*` it's supposed to create a dynamic binding rather than a normal lexical binding? It knows because the name has been declared special. 12 The name of every variable defined with DEFVAR and DEFPARAMETER is automatically declared globally special. This means whenever you use such a name in a binding form -- in a LET or as a function parameter or any other construct that creates a new variable binding -- the binding that's created will be a dynamic binding. This is why the `*naming*` `*convention*` is so important -- it'd be bad news if you used a name for what you thought was a lexical variable and that variable happened to be globally special. On the one hand, code you call could change the value of the binding out from under you; on the other, you might be shadowing a binding established by code higher up on the stack. If you always name global variables according to the `*` naming convention, you'll never accidentally use a dynamic binding where you intend to establish a lexical binding.

2『目前还是没弄明白，`*` 命名全局变量，与普通命名全局变量的本质区别。（2020-11-08）』

It's also possible to declare a name locally special. If, in a binding form, you declare a name special, then the binding created for that variable will be dynamic rather than lexical. Other code can locally declare a name special in order to refer to the dynamic binding. However, locally special variables are relatively rare, so you needn't worry about them.13

Dynamic bindings make global variables much more manageable, but it's important to notice they still allow action at a distance. Binding a global variable has two at a distance effects -- it can change the behavior of downstream code, and it also opens the possibility that downstream code will assign a new value to a binding established higher up on the stack. You should use dynamic variables only when you need to take advantage of one or both of these characteristics.

7 Java disguises global variables as public static fields, C uses extern variables, and Python’s module-level and Perl’s package-level variables can likewise be accessed from anywhere.

8 If you specifically want to reset a DEFVARed variable, you can either set it directly with SETF or make it unbound using MAKUNBOUND and then reevaluate the DEFVAR form.

9 The strategy of temporarily reassigning `*standard-output*` also breaks if the system is multithreaded—if there are multiple threads of control trying to print to different streams at the same time, they’ll all try to set the global variable to the stream they want to use, stomping all over each other. You could use a lock to control access to the global variable, but then you’re not really getting the benefit of multiple concurrent threads, since whatever thread is printing has to lock out all the other threads until it’s done even if they want to print to a different stream.

10 The technical term for the interval during which references may be made to a binding is its extent. Thus, scope and extent are complementary notions—scope refers to space while extent refers to time. Lexical variables have lexical scope but indefinite extent, meaning they stick around for an indefinite interval, determined by how long they’re needed. Dynamic variables, by contrast, have indefinite scope since they can be referred to from anywhere but dynamic extent. To further confuse matters, the combination of indefinite scope and dynamic extent is frequently referred to by the misnomer dynamic scope.

11 Though the standard doesn’t specify how to incorporate multithreading into Common Lisp, implementations that provide multithreading follow the practice established on the Lisp machines and create dynamic bindings on a per-thread basis. A reference to a global variable will find the binding most recently established in the current thread, or the global binding.

12 This is why dynamic variables are also sometimes called special variables.

13 If you must know, you can look up DECLARE, SPECIAL, and LOCALLY in the HyperSpec.

### 6.4 Constants

One other kind of variable I haven't mentioned at all is the oxymoronic "constant variable." All constants are global and are defined with DEFCONSTANT. The basic form of DEFCONSTANT is like DEFPARAMETER.

```c
(defconstant name initial-value-form [ documentation-string ])
```

As with DEFVAR and DEFPARAMETER, DEFCONSTANT has a global effect on the name used -- thereafter the name can be used only to refer to the constant; it can't be used as a function parameter or rebound with any other binding form. Thus, many Lisp programmers follow a naming convention of using names starting and ending with + for constants. This convention is somewhat less universally followed than the *-naming convention for globally special names but is a good idea for the same reason. 14

Another thing to note about DEFCONSTANT is that while the language allows you to redefine a constant by reevaluating a DEFCONSTANT with a different initial-value-form, what exactly happens after the redefinition isn't defined. In practice, most implementations will require you to reevaluate any code that refers to the constant in order to see the new value since the old value may well have been inlined. Consequently, it's a good idea to use DEFCONSTANT only to define things that are really constant, such as the value of NIL. For things you might ever want to change, you should use DEFPARAMETER instead.

14 Several key constants defined by the language itself don’t follow this convention—not least of which are T and NIL. This is occasionally annoying when one wants to use t as a local variable name. Another is PI, which holds the best long-float approximation of the mathematical constant π.

### 6.5 Assignment

Once you've created a binding, you can do two things with it: get the current value and set it to a new value. As you saw in Chapter 4, a symbol evaluates to the value of the variable it names, so you can get the current value simply by referring to the variable. To assign a new value to a binding, you use the SETF macro, Common Lisp's general-purpose assignment operator. The basic form of SETF is as follows:

```c
(setf place value)
```

Because SETF is a macro, it can examine the form of the place it's assigning to and expand into appropriate lower-level operations to manipulate that place. When the place is a variable, it expands into a call to the special operator SETQ, which, as a special operator, has access to both lexical and dynamic bindings.15 For instance, to assign the value 10 to the variable x, you can write this:

```c
(setf x 10)
```

As I discussed earlier, assigning a new value to a binding has no effect on any other bindings of that variable. And it doesn't have any effect on the value that was stored in the binding prior to the assignment. Thus, the SETF in this function:

```c
(defun foo (x) 
  (setf x 10)
)
```

will have no effect on any value outside of foo. The binding that was created when foo was called is set to 10, immediately replacing whatever value was passed as an argument. In particular, a form such as the following:

```c
(let ((y 20)) 
  (foo y) 
  (print y)
)
```

will print 20, not 10, as it's the value of y that's passed to foo where it's briefly the value of the variable x before the SETF gives x a new value. SETF can also assign to multiple places in sequence. For instance, instead of the following:

```c
(setf x 1) 
(setf y 2)
```

you can write this:

```c
(setf x 1 y 2)
```

SETF returns the newly assigned value, so you can also nest calls to SETF as in the following expression, which assigns both x and y the same random value:

```c
(setf x (setf y (random 10)))
```

15 Some old-school Lispers prefer to use SETQ with variables, but modern style tends to use SETF for all assignments.

1『怪不得 autolisp 里用 `setq` 给变量赋值，果然是老古董，哈哈。（2020-11-08）』

### 6.6 Generalized Assignment

Variable bindings, of course, aren't the only places that can hold values. Common Lisp supports composite data structures such as arrays, hash tables, and lists, as well as user-defined data structures, all of which consist of multiple places that can each hold a value.

I'll cover those data structures in future chapters, but while we're on the topic of assignment, you should note that SETF can assign any place a value. As I cover the different composite data structures, I'll point out which functions can serve as "SETFable places." The short version, however, is if you need to assign a value to a place, SETF is almost certainly the tool to use. It's even possible to extend SETF to allow it to assign to user-defined places though I won't cover that. 16

In this regard SETF is no different from the = assignment operator in most C-derived languages. In those languages, the = operator assigns new values to variables, array elements, and fields of classes. In languages such as Perl and Python that support hash tables as a built-in data type, = can also set the values of individual hash table entries. Table 6-1 summarizes the various ways = is used in those languages.

Table 6-1. Assignment with = in Other Languages

|  Assigning to ... |  Java, C, C++  |  Perl  | Python  |
| -- -| -- -| -- -| -- -|
|  ... variable |  x = 10; |  `$x = 10;` |  x = 10 |
|  ... array element |  a[0] = 10;   |  `$a[0] = 10;` |  a[0] = 10 |
|  ... hash table entry |  |  `$hash{'key'} = 10;` |  hash['key'] = 10 |
|  ... field in object |   o.field = 10; | ` $o->{'field'} = 10;` |  o.field = 10 |

1『发现 Perl 的语法跟 PHP 一样的，突然间想起来，PHP 语言本身就是用 Perl 写的。（2020-11-08）』

SETF works the same way -- the first "argument" to SETF is a place to store the value, and the second argument provides the value. As with the = operator in these languages, you use the same form to express the place as you'd normally use to fetch the value. 17 Thus, the Lisp equivalents of the assignments in Table 6-1 -- given that AREF is the array access function, GETHASH does a hash table lookup, and field might be a function that accesses a slot named field of a user-defined object -- are as follows:

```c
Simple variable: 
(setf x 10) 

Array: 
(setf (aref a 0) 10) 

Hash table: 
(setf (gethash 'key hash) 10) 

Slot named 'field': 
(setf (field o) 10)
```

Note that SETFing a place that's part of a larger object has the same semantics as SETFing a variable: the place is modified without any effect on the object that was previously stored in the place. Again, this is similar to how = behaves in Java, Perl, and Python. 18

16 Look up DEFSETF, DEFINE-SETF-EXPANDER for more information.

17 The prevalence of Algol-derived syntax for assignment with the “place” on the left side of the = and the new value on the right side has spawned the terminology lvalue, short for “left value,” meaning something that can be assigned to, and rvalue, meaning something that provides a value. A compiler hacker would say, “SETF treats its first argument as an lvalue.”

18 C programmers may want to think of variables and other places as holding a pointer to the real object; assigning to a variable simply changes what object it points to while assigning to a part of a composite object is similar to indirecting through the pointer to the actual object. C++ programmers should note that the behavior of = in C++ when dealing with objects—namely, a memberwise copy—is quite idiosyncratic.

### 6.7 Other Ways to Modify Places

While all assignments can be expressed with SETF, certain patterns involving assigning a new value based on the current value are sufficiently common to warrant their own operators. For instance, while you could increment a number with SETF, like this:

```c
(setf x (+ x 1))
```

or decrement it with this:

```c
(setf x (- x 1))
```

it's a bit tedious, compared to the C-style ++x and  -- x. Instead, you can use the macros INCF and DECF, which increment and decrement a place by a certain amount that defaults to 1.

```c
(incf x) === (setf x (+ x 1)) 
(decf x) === (setf x (- x 1)) 
(incf x 10) === (setf x (+ x 10))
```

INCF and DECF are examples of a kind of macro called modify macros. Modify macros are macros built on top of SETF that modify places by assigning a new value based on the current value of the place. The main benefit of modify macros is that they're more concise than the same modification written out using SETF. Additionally, modify macros are defined in a way that makes them safe to use with places where the place expression must be evaluated only once. A silly example is this expression, which increments the value of an arbitrary element of an array:

```c
(incf (aref *array* (random (length *array*))))
```

A naive translation of that into a SETF expression might look like this:

```c
(setf (aref *array* (random (length *array*))) 
  (1+ (aref *array* (random (length *array*))))
)
```

However, that doesn't work because the two calls to RANDOM won't necessarily return the same value -- this expression will likely grab the value of one element of the array, increment it, and then store it back as the new value of a different element. The INCF expression, however, does the right thing because it knows how to take apart this expression:

```c
(aref *array* (random (length *array*)))
```

to pull out the parts that could possibly have side effects to make sure they're evaluated only once. In this case, it would probably expand into something more or less equivalent to this:

```c
(let ((tmp (random (length *array*)))) 
  (setf (aref *array* tmp) (1+ (aref *array* tmp)))
)
```

In general, modify macros are guaranteed to evaluate both their arguments and the subforms of the place form exactly once each, in left-to-right order.

The macro PUSH, which you used in the mini-database to add elements to the `*db*` variable, is another modify macro. You'll take a closer look at how it and its counterparts POP and PUSHNEW work in Chapter 12 when I talk about how lists are represented in Lisp.

Finally, two slightly esoteric but useful modify macros are ROTATEF and SHIFTF. ROTATEF rotates values between places. For instance, if you have two variables, a and b, this call:

```c
(rotatef a b)
```

swaps the values of the two variables and returns NIL. Since a and b are variables and you don't have to worry about side effects, the previous ROTATEF expression is equivalent to this:

```c
(let ((tmp a)) 
  (setf a b b tmp) 
  nil
)
```

With other kinds of places, the equivalent expression using SETF would be quite a bit more complex.

SHIFTF is similar except instead of rotating values it shifts them to the left -- the last argument provides a value that's moved to the second-to-last argument while the rest of the values are moved one to the left. The original value of the first argument is simply returned. Thus, the following:

```c
(shiftf a b 10)
```

is equivalent -- again, since you don't have to worry about side effects -- to this:

```c
(let ((tmp a)) 
  (setf a b b 10) 
  tmp
)
```

Both ROTATEF and SHIFTF can be used with any number of arguments and, like all modify macros, are guaranteed to evaluate them exactly once, in left to right order. With the basics of Common Lisp's functions and variables under your belt, now you're ready to move onto the feature that continues to differentiate Lisp from other languages: macros.