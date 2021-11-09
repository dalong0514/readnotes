## 记忆时间

## 附件1-CP401-1-Lisp-Advance-Yourself

Lisp: Advance Yourself Beyond A Casual

Are you a casual LISP programmer? Do you get what you want done but feel like you have to bludgeon your way through it? Do you have trouble getting what's under the hood into overdrive? Then, this class is for you. You'll learn many of the things that real power AutoLISP® programmers know, so you can get more done in less time.

About the Speaker:

A Midwestern transplant now based in Southern California, Darren has held a variety of positions over the last 15 years, such as CAD/CAM engineer, CAD administrator, and CAD/CAM systems developer. Currently Darren is the Systems Integration Manager for Southland Industries, one of the top 10 mechanical contractors in the United States. While Darren's true interest is the automation of manufacturing systems, his experience ranges from manufacturing to architecture, and this has led him to projects varying in scope from dress patterns to gas turbine piping. He founded a consulting and development business called Minnesota CADWorks, has been a technical editor for the 2002, 2004, and 2005 versions of the AutoCAD Bible (by Autodesk Registered Author Ellen Finkelstein) and has been a regular contributing author for Inside AutoCAD since 2001.

Work / dyoung@southlandind.com 

Home / darren@mcwi.com

### 1.1 Introduction

This course is for anyone who's casually programmed AutoLISP but knows there's more untapped power under the hood. At the end of this class, You'll know exactly where to look and how to tap into that power increasing your coding abilities and enabling you to write more functional programs, with less code in less time.

With ARX, VBA, and now .Net (Dot Net), there's always a rumor flying around that AutoLISP is dead or going away. that's simply not true. While there are plenty of reasons to use other APIs and languages, there's also plenty of reasons to continue using AutoLISP and Visual LISP. For the non-professional programmer, it's a great, easy to learn language with plenty of power. it's built into AutoCAD, it can do most of what VBA can do, and you don't have to purchase any special development software. If you want to automate AutoCAD, AutoLISP and Visual LISP is a perfectly suitable option. Take it for a test drive and put the petal to the floor. You'll be amazed at what it can do.

### 1.2 Advanced AutoLISP

#### 1.2.1 apply

```c
(apply 'function list)
```

This function takes a quoted function, and applies it to a list of arguments. This can be very useful for functions that require a list of arguments when you don't know how many there will be. If you know how many arguments or variables, it's typically not needed.

```c
(+ 1 3)    ; We know there's 2 numbers to add. It's all that's needed 
(apply ‘+ ‘(1 3))    ; This isn't very readable, efficient to code or helpful
(setq mylist ‘(list 1 3))    ; What if our data was in a list?
(+ (nth 0 mylist) (nth 1 mylist))    ; Now this isn't very efficient or readable 
(apply ‘+ mylist) ;    In this case, this is now better 
(setq mylist ‘(1 3 5…etc…)) ;    What if we didn't know how many items in the list? 
(apply ‘+ mylist) ;    It's still the same no matter how many items
```

When you have a list of raw data, it's not practical to build a new list inserting the function in the front of it so that it can be evaluated. it's also not efficient (coding or processing) to loop through that list of potentially unknown length processing each item one at a time.

This…

```c
(1 3 5) 
```

Turned into this…

```c
(+ 1 3 5)
```

Would require this…

```c
(eval (cons (quote +) mylist))
```

Or require this…

```c
(setq number 0) 
(foreach item mylist 
  (setq number (+ number item)) 
)
```

But is simpler with this…

```c
(apply ‘+ mylist))
```

1『

apply 函数更重要的作用是把函数转化为另一个函数的参数，让我能够拆解函数成颗粒度更细的模块（函数），已数据流中刷管道等级号变更的功能为例。

```c
(defun c:brushPipeClassChangeMacro (/ sourceData pipeClassChangeData instrumentAndPipeData pipeClassChangeInfo)
  (prompt "\n选择变管道等级块以及要刷的管道或仪表数据（变等级块只能选一个）：")
  (setq sourceData (GetInstrumentAndPipeAndPipeClassChangeData))
  (setq pipeClassChangeData (GetPipeClassChangeDataForBrushPipeClassChange sourceData))
  (setq instrumentAndPipeData (GetInstrumentAndPipeDataForBrushPipeClassChange sourceData))
  (setq pipeClassChangeInfo (GetPipeClassChangeInfo (car pipeClassChangeData)))
  (ExecuteFunctionForOneSourceDataUtils (length pipeClassChangeData) 'BrushOnePropertyDataForInstrumentAndPipe 
    (list instrumentAndPipeData pipeClassChangeInfo "PIPECLASSCHANGE")
  )
)

(defun c:brushReducerInfoMacro (/ sourceData ReducerData instrumentAndPipeData reducerInfo entityNameList)
  (prompt "\n选择异径管块以及要刷的管道或仪表数据（异径管块只能选一个）：")
  (setq sourceData (GetInstrumentAndPipeAndReducerData))
  (setq ReducerData (GetReducerDataForBrushReducerInfo sourceData))
  (setq instrumentAndPipeData (GetInstrumentAndPipeDataForBrushReducerInfo sourceData))
  (setq reducerInfo (cdr (assoc "REDUCER" (car ReducerData))))
  (ExecuteFunctionForOneSourceDataUtils (length ReducerData) 'BrushOnePropertyDataForInstrumentAndPipe 
    (list instrumentAndPipeData reducerInfo "REDUCERINFO")
  )
)

; very importance for me, convert a function to the parameter for another function - 2020-12-25
(defun ExecuteFunctionForOneSourceDataUtils (dataListLength functionName argumentList /)
  (if (= dataListLength 1)
    (vl-catch-all-apply functionName argumentList)
    (progn 
      (alert "数据源只能选一个！")
      (princ)
    )
  ) 
)

(defun BrushOnePropertyDataForInstrumentAndPipe (instrumentAndPipeData ChangedInfo propertyName / entityNameList)
  (setq entityNameList (GetEntityNameListByEntityHandleListUtils (GetEntityHandleListByPropertyDictListUtils instrumentAndPipeData)))
  (ModifyMultiplePropertyForBlockUtils entityNameList (list propertyName) (list ChangedInfo))
  (alert "刷数据完成！")(princ)
)
```

这里的关键函数是 `ExecuteFunctionForOneSourceDataUtils`，它帮忙消除了条件语句。其实还可以通过多态来重构，消除 `brushPipeClassChangeMacro` 和 `brushReducerInfoMacro` 里不少重复的代码。(2020-12-25)

』

#### 1.2.2 mapcar

```c
(mapcar 'function list {list} …etc…)
```

This function is similar to (apply) but is different in one key way, while (apply) applied a function to a whole list of arguments at a time, (mapcar) also takes a list (or lists), but applies the function to each item in the list individually, then returns the result in list form, of each item with the function applied. Using the following list…

```c
(setq mylist (“apple” “orange” “banana” “zubrovka”))
```

You could use this code (imagine if there were hundreds of items in your list)…

```c
(list (strcase (nth 0 mylist)) 
      (strcase (nth 1 mylist)) 
      (strcase (nth 2 mylist)) 
      (strcase (nth 3 mylist)) 
)
```

Or this code…

```c
(mapcar ‘strcase mylist)
```

To get this result…

```c
("APPLE" "ORANGE" "BANANA" "ZUBROVKA")
```

When used with multiple lists, each list is processed in parallel one item at a time. Again, using these 2 lists…

```c
(setq mylist1 '(1.0 2.0 3.0)) 
(setq mylist2 '(0.1 0.2 0.3))
```

You could use this code…

```c
(list (+ (car mylist1) (car mylist2)) 
      (+ (cadr mylist1) (cadr mylist2)) 
      (+ (caddr mylist1) (caddr mylist2))
)
```

Or this code…

```c
(mapcar '+ mylist1 mylist2)
```

To get this result…

```c
(1.1 2.2 3.3)
```

But what if the 2 lists contained different numbers of items? (mapcar) only processes the lists while each list contains matching items in the other lists. In other words, it only processes the number of items in the shortest list and ignores (with no errors) any additional items the other lists may contain. Use this to your advantage. If we use two lists of unequal length like this…

```c
(setq mylist1 '(1.0 2.0)) 
(setq mylist2 '(0.1 0.2 0.3))
```

This code…

```c
(mapcar '+ mylist1 mylist2)
```

Returns this result…

```c
(1.1 2.2)
```

#### 1.2.3 lambda

```c
(lambda arguments expression)
```

You don't see this function by itself. it's usually wrapped inside another complex function like (mapcar) or (apply) and some of the Visual Lisp “VL-“ based functions. To truly understand (lambda), it's best to think of it as being almost identical to (defun) which defines a function. When you use (defun) to create a function, the result is a function that you call many times throughout a program because the function is defined and stored in memory by name. Likewise (lambda) also creates a function, but it's not named and not stored in memory, it's used on the spot, then and there without being able to be called again.

that's all fine and good but what does this do for you the programmer? what's it all mean? The essence of (lambda) is that it lets you define a function on the fly at the point in your code where it's needed, which often makes it more understandable, and without having to create the overhead in memory of actually defining a named function that you don't need anymore. Think of it this way…in Lisp programming, you create variables when you think You'll need the value again. If you don't need the value, you take the value and pass it to another function. Take the following two examples, both of which result in telling you how many seconds in a week which; we'll assume is the value we want to use. Would you use this code…

```c
(setq seconds-per-minute 60) 
(setq minutes-per-hour 60) 
(setq hours-per-day 24)
(setq days-per-week 7) 
(setq seconds-per-hour (* 60 60)) 
(setq seconds-per-day (* seconds-per-hour hours-per-day)) 
(setq seconds-per-week (* seconds-per-day days-per-week))
```

Or would you use this code…

```c
(setq seconds-per-week (* 60 60 24 7))
```

Using (lambda) is essentially the same thing but on the function level instead of the variable level. You typically would not create a whole bunch of named functions all over the place (via defun) that you would never use again unless the function was large and complex or had a specific major purpose and objective. In these other cases, you can use the (lambda) construct instead. Let's use our previous (strcase) example that we used with (mapcar) in the preceding section. (mapcar) worked real well with (strcase) when converting to lower case. But what about uppercase? (strcase) in that situation needs a second parameter, a T, to tell (strcase) to convert to lower case. For (mapcar) to work it needs something extra. Let's again use this data…

```c
(setq mylist '("APPLE" "ORANGE" "BANANA" "ZUBROVKA"))
```

You could do something like this to pass the T along with the string to (strcase) by building a list of T's for each string value…

```c
(mapcar ‘strcase mylist ‘(T T T T))
```

1『这里虽然作者用上面「不好的」例子引出 lambda，但上面的例子对目前的自己很有启发。如果 mapcar 一个自己定义好的函数（即传入函数名），这个函数有 2 个入参，mapcar 的第一个参数列表用已有的数组，第二个列表可以人为造一个数组。（2021-11-09）』

This works well because as you learned earlier, each of the lists passes its items in parallel meaning a T goes along with each sting to (strcase). However, you could also do this…

```c
(mapcar ‘(lambda (x) (strcase x T)) mylist)
```

doesn't seem much different does it. it's actually less clear using (lambda). But what if you don't know ahead of time how many strings are going to be passed? You'll have to create a loop that creates enough T's for that second list which further complicates the first example. In the second example that uses (lambda), it doesn't matter. We defined a function with (lambda) that adds the T. (mapcar) then just passes each item to the function, which is accessed with the function's argument X.

Also, consider that the first example worked well because we just blindly passed items from the lists to (strcase). But what if we needed to perform some type of operation on them? Mathematical operations, conditional testing (if/cond/eq/equal/…etc…) all would not have worked unless they were inside the (lambda) function, which could perform any number of operations in the data.

Let's take a look at another example. This time, we're going to give (mapcar) a list of Month names and we'd like back from (mapcar), a list of Month names abbreviated to the first 3 letters, with the initial letter being upper case and the last two lower case. Let's use this as our list…

```c
(setq months ‘(“JANUARY” “february” “March” “aPRIL” “MaY” “JUNE” “july” “AuGusT” “SEPtember” “octOBER” “NOVEMBER” “DeCemBer”))
```

With this data list, (strcat) can't do it. Neither can the (substr) function. Using them together along with (strcat), we can do it with the following code…

```c
(mapcar '(lambda (x) 
           (strcat (strcase (substr x 1 1)) (strcase (substr x 2 2) T)) 
         ) 
         months 
)
```

Which returns this as our list…

```c
("Jan" "Feb" "Mar" "Apr" "May" "Jun" "Jul" "Aug" "Sep" "Oct" "Nov" "Dec")
```

Now wasn't that much easier? You can even use multiple lists with (lambda), just make sure there's enough argument variables declared so that there's one for each list that will be passing values from. Again, take this for an example…

```c
(setq pt1 ‘(-3.24 2.82 0.0)) 
(setq pt2 ‘(2.5 8.76))
```

With (mapcar) and (lambda), we can easily find the midpoint between those 2 points using this code…

```c
(mapcar '(lambda (c1 c2) (/ (+ c1 c2) 2.0)) 
        pt1 
        pt2 
)
```

This results in the point (-0.37 5.79) being returned. Notice that one of the points doesn't have a Z-coordinate yet the function doesn't error out. If you're working with 2d points, that's a good thing. If they both had a Z-coordinate, it would have worked with that we well. Now Here's a variation of that same code you may see…

```c
(mapcar (function 
          (lambda (c1 c2) (/ (+ c1 c2) 2.0))
        ) 
        pt1 
        pt2
)
```

In this example, (mapcar) isn't using a quoted function ('), instead it's using the (function) function. This was introduced because when running compiled AutoLISP code (FAS or VLX files), if the code fails in the right place in the right conditions, the quoted (lambda) function's source code could be exposed and displayed on the text screen. By wrapping it the (function) statement, it's protected from viewing during these types of failures. Using either form is perfectly fine, and one is not more correct than the other. Using the quoted function is a little easier to read and typically all that's needed if you aren't worried about keeping people from viewing your source code. Just as there's a quote function (quote) that can be used in place of the quote symbol ('), the (function) function does a similar thing at the function level. Now hopefully that wasn't too confusing with all the function functions and quote quotes.

#### 1.2.4 Putting It All Together Back At The Office

When you can back to the office, try this for an exercise. This is the exact very same example I had years ago when I made the leap into using more advanced functions like (mapcar), (apply), and (lambda). I'd seen those advanced functions used before, but I never took the time to use them or figure them out let alone mixing several all together nested. Then, I found the need to use the (nentsel) function, which returned nested data from a user selection. That is, I wanted information about a coordinate of an object within a block, not information about the block. The (nentsel) explanation in the AutoLISP reference explains the data it returns and how it's processed using the transformation matrix to get what you are looking for. The following code was what I came up with after 2 days where pt1 was the point and mat was the transformation matrix as turned by (nentsel) …

```c
(setq pt1
  (list (+ (* (nth 0 (nth 0 mat)) (nth 0 pt1)) 
           (* (nth 0 (nth 1 mat)) (nth 1 pt1)) 
           (* (nth 0 (nth 2 mat)) (nth 2 pt1)) 
           (nth 0 (nth 3 mat))) 
        (+ (* (nth 1 (nth 0 mat)) (nth 0 pt1)) 
           (* (nth 1 (nth 1 mat)) (nth 1 pt1)) 
           (* (nth 1 (nth 2 mat)) (nth 2 pt1)) 
           (nth 1 (nth 3 mat))) 
        (+ (* (nth 2 (nth 0 mat)) (nth 0 pt1)) 
           (* (nth 2 (nth 1 mat)) (nth 1 pt1)) 
           (* (nth 2 (nth 2 mat)) (nth 2 pt1)) 
           (nth 2 (nth 3 mat)))
  )
)
```

It worked, but frustrated with the amount of effort and knowing that there must be a better way, I posted the question on the old ACAD forum on CompuServe (now part of AOL). I don't even recall whom the person was any more, but this is the code they posted back that did the same thing…

```c
(setq pt (append pt (list 1.0))) 
(mapcar '(lambda (x) (apply '+ x)) 
         (list (mapcar '* pt (mapcar 'car mat)) 
               (mapcar '* pt (mapcar 'cadr mat)) 
               (mapcar '* pt (mapcar 'caddr mat)) 
         ) 
)
```

As you can see, it's a lot smaller and more efficient. It was upon viewing that code, that I committed to breaking down this small snippet and figuring out exactly what it does and how it does it. When you're back at the office, try doing the same. Refer back to the (nentsel) documentation in the AutoLISP Reference so you know what the code is attempting to do. I guarantee, that when you go through this snippet and actually understand how it works and why, You'll never have trouble with (apply), (mapcar), or (lambda) ever again. Use the following blank lines to make notes as you disassemble this code and figure out what it does.

#### 1.2.5 Recursive Programming – It's Kind Of Like Talking To Yourself

One of the oddest concepts that a lot of casual programmers have difficulty understanding, let alone implementing in code is known as Recursion. The simplest example of recursion is something most people have seen at one time or another. If you took a television camera and recorded the television itself, and played that to that same television you were recording, you'd see a recursive graphic. The television, would be displaying a picture of itself, displaying a picture of itself, displaying a picture of itself, etc.

Recursion in programming is essentially the same thing, it's when a program calls itself. Of course, unlike the television picture that goes on and on forever, with recursive programming, you need to have an “out” or your program would just go on forever and ever in an endless loop until your software or computer ran out of memory.

It's a difficult concept to grasp beyond the basic definition of “a program that calls itself”. Anyone can understand that, but wrapping your head around how you'd use such a technique in your programs is a little more mind numbing. So to get you thinking about it and understanding it, let's look at a few examples, which might get you thinking about how you can apply this from a programming perspective.

Suppose you built a machine that has one conveyor that fed into it, and one that fed out of it. The machine, removes cardboard boxes to reveal the contents of the box. Boxes move down the in feed conveyor, into the machine, the cardboard box is removed, and the contents come out on the exit conveyor. Now, what would happen if one of the boxes contained more cardboard boxes? As the machine processed the big box that had more, smaller cardboard boxes inside, it stopped accepting big boxes from the feed conveyor. It then took the smaller boxes, and fed those back into the machine again. The machine then stripped the cardboard off the small boxes, except one of those contained even more tiny boxes. The small boxes stopped feeding into the machine, and the tiny boxes went back in. When all the tiny boxes finished going into the machine, the small boxes started again, and when all those were done, the large boxes started again. This process that the machine we built was performing, can be thought of as recursion.

Now instead of a conveyor of boxes, think of data in a List. Maybe the List has strings, integers, real numbers. Maybe some of the items are Lists and some of those may or may not contain Lists. How would you process this data not knowing how deep it was nested? you'd build a recursive function that processed the List, and when it encountered a nested List inside of the List, it would halt processing the List (temporarily), while it called itself and handled the nested List and when finished with the nested List, it would continue with the main list.

Another good example is a program that processes folders on your hard drive and finds files. You can point it to a folder, but does that folder contain more folders? And do those folders contain more folders? And are files scattered through out at all levels within those “unknown” levels of sub-folders? This would be a good case for using recursion. This is the essence of recursive programming. Anytime you have an unknown set of potentially nested conditions or processes you need to perform, or data you need to examine, recursive programming can come to the rescue.

Let's start looking at some code. To begin with, we'll write code that returns the factorial of the number 4. If you're unfamiliar with factorials, it's the mathematical process where you take a number, multiply it by a number one less, multiplied by a number one less until you get to 1. So, the factorial for the number 4 is the following formula 4 * 3 * 2 * 1 =  24.

```c
(defun factorial (n) 
  (cond 
    ((= n 0) 1) 
    (T (* n (factorial (1- n))))
  )
)
```

1-2『

[cond (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-7BA45202-D95F-4F2D-8D83-965024826074)

The cond function accepts any number of lists as arguments. It evaluates the first item in each list (in the order supplied) until one of these items returns a value other than nil. It then evaluates those expressions that follow the test that succeeded.

```c
(cond 
   ((minusp a) (- a)) 
   (t a)
)
```

If the variable a is set to the value-10, this returns 10. As shown, cond can be used as a case type function. It is common to use T as the last (default) test expression. Here's another simple example. Given a user response string in the variable s, this function tests the response and returns 1 if it is Y or y, 0 if it is N or n; otherwise nil.

```c
(cond
   ((= s "Y") 1) 
   ((= s "y") 1) 
   ((= s "N") 0) 
   ((= s "n") 0) 
   (t nil)
)
```

cond 语句感觉还是很有用的，类似于其他语言里的 case 语句，多个不同的场景返回不同的值，这个场景可以通过 cond 来实现。看到这些例子，发现一般最后一条语句采用 `T` 结合默认结果来收尾。做一张术语卡片。（2020-10-27）——已完成

』

Recursion is a good option here because we don't always know how many times we'll need to multiply unless we know the number before hand. In this case we do and it's 4 so we call the function with the syntax (factorial 4). Now, while our formula is 4 * 3 * 2 * 1, this program takes a slightly different approach, it works from the opposite direction, it's actually calculating 1 * 2 * 3 * 4. If you think about it, that's what all of your AutoLISP programs do, they work into the nested most functions, then slowly work back.

In this case, the program doesn't try to perform (4 * 3), it tries to perform (4 * (factorial of 3)). But to calculate the factorial of 3, it needs to multiply it by the factorial of 2, which it also doesn't know and so on. What might help you understand a little better, is to list the formula so it reflects more closely what's going on is this…

```c
Factorial of 4 = (* 4 (Factorial of 3)) 
Factorial of 3 = (* 3 (Factorial of 2)) 
Factorial of 2 = (* 2 (Factorial of 1)) 
Factorial of 1 = (1 * 1)
```

Or putting it all together in an AutoLISP like syntax it looks like this…

```c
(factorial 4) = (* 4 (* 3 (* 2 (* 1 1))))
```

Here's some code that reflects this without using recursion (without the program calling itself)…

```c
(defun factorial4 (n) 
  (* n (factorial3 (1- n))) 
) 
(defun factorial3 (n) 
  (* n (factorial2 (1- n))) 
) 
(defun factorial2 (n) 
  (* n (factorial1 (1- n))) 
) 
(defun factorial1 (n) 
  n 
)
```

Calling the above code (factorial4 4) will do the same thing as the recursive example. Except in this case, instead of calling itself, it calls a completely different function that's almost identical. As you can see, a lot of the code is the same. And the “unknown” nature of not knowing how many times (how deep is it nested) makes this a good application for recursion.

1-2『判断何时应该使用递归的办法，遇到那种自己都不知道要计算多少次的场景时，自己要有意识的想想能不能用递归函数来实现。该信息合并进递归的术语卡里。（2020-10-27）』

The fact that we're dealing with numbers in this example, means that it would really not be that hard to create a loop with a few counter variables to perform this same calculation. But not all cases would be that easy. Let's look at another example that deals with nested lists…

```c
(setq mylist '(1 2 3 (4 5 (6 7 (8 9) 10) 11) 12 13 (14 15 (16)))) 

(defun item-in-list (L I) 
  (vl-some '(lambda (x) 
              (cond 
                ((= x I) T) 
                ((= (type x) 'LIST) (item-in-list x I)) 
                (T nil))
            ) 
            L
  )
)
```

The code in this example looks for a user specified item within a list. The AutoLISP function (member) typically handles this type of need. But if the list contains other nested lists, (member) just doesn't do it anymore. In this case, we're using a function called (vl-some). This function takes a quoted function, just like (apply) or (mapcar). The purpose of (vl-some) is to return T if the function evaluates to T for at least 1 (one) item in the list. If the function evaluates to NIL for all items, it returns NIL. it's the perfect function for our needs. Next, we build our function. Just like (mapcar), (vl-some) will be handed each item in the list, one at a time. Your function then needs to check if that item matches what we're looking for. that's not hard. But what if the list item, is another list? Our function must also check for that, and if the list item is another list, it calls itself again to process the nested list. Now, (vl-some) itself isn't looking for our item, our (lambda) function is doing that. What (vl-some) does is looks for T or NIL and it returns T or NIL. (lambda) is pasting the T and/or NILs to (vl-some).

1-2-3『

看到 `vl-some` 后印象中「JS 忍者秘籍」讲数组操作的那章有一个函数功能相同，去查了下是 `some` 函数，顺带看到 JS 里配套的一个 `every` 函数，果然又在 autolisp 里查到 `vl-every` 函数，哈哈。相关知识做一张术语卡。（2020-10-27） ——已完成

忍者秘籍里：

测试数组，元素处理集合的元素时，常常遇到需要知道数组的全部元素或部分元素是否满足某些条件。为了尽可能有效地编写这段代码，JavaScript 数组具有内置的 every 和 some 方法，如清单 9.8 所示。1）every 方法接收回调函数，对集合中的每个 ninja 对象检查是否含有 name 属性。当且仅当全部的回调函数都返回 true 时，every 方法才返回 true，否则返回 false。

```js
var allNinjasAreNamed = ninjas.every(ninja => "name" in ninja);
```

some 方法从数组的第 1 项开始执行回调函数，直到回调函数返回 true。如果有一项元素执行回调函数时，返回 true, some 方法返回 true；否则，some 方法返回 false。

```js
const someNinjasAreArmed = ninjas.some(ninja => "weapon" in ninja);
```

[vl-every (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-8BF61C9E-1382-4168-A778-FEA394A361CC)

Checks whether the predicate is true for every element combination.

```c
(vl-every predicate-function list [list ...])
```

predicate-function. Type: Subroutine or Symbol. The test function. This can be any function that accepts as many arguments as there are lists provided with vl-every, and returns T on any user-specified condition. The predicate-function value can take one of the following forms:

```c
A symbol (function name)
'(LAMBDA (A1 A2) ...)
(FUNCTION (LAMBDA (A1 A2) ...))
```

list. Type: List. A list to be tested.

Return Values. Type: T or nil. T, if predicate-function returns a non-nil value for every element combination; otherwise nil.

Remarks. The `vl-every` function passes the first element of each supplied list as an argument to the test function, followed by the next element from each list, and so on. Evaluation stops as soon as one of the lists runs out.

Examples

Check whether there are any empty files in the current directory:

```c
(vl-every
'(lambda (fnm) (> (vl-file-size fnm) 0))
   (vl-directory-files nil nil 1))
T
```

Check whether the list of numbers in nlst is ordered by `'<=`:

```
(setq nlst (list 0 2 pi pi 4))
(0 2 3.14159 3.14159 4)

(vl-every '<= nlst (cdr nlst))
T
```

1『这个实现好，判断一个数组是否排好了序，直觉上以后肯定会遇到这个功能。（2020-10-27）』

Compare the results of the following expressions:

```c
(vl-every '= '(1 2) '(1 3))
nil

(vl-every '= '(1 2) '(1 2 3))
T
```

The first expression returned nil because vl-every compared the second element in each list and they were not numerically equal. The second expression returned T because vl-every stopped comparing elements after it had processed all the elements in the shorter list (1 2), at which point the lists were numerically equal. If the end of a list is reached, vl-every returns a non-nil value.

The following example demonstrates the result when vl-every evaluates one list that contains integer elements and another list that is nil:

```c
(setq alist (list 1 2 3 4))
(1 2 3 4)

(setq junk nil)
nil

(vl-every '= junk alist)
T
```

The return value is T because vl-every responds to the nil list as if it has reached the end of the list (even though the predicate has not yet been applied to any elements). And since the end of a list has been reached, vl-every returns a non-nil value.

[vl-some (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-2840F793-DA88-4140-8A9D-EBAC47B62F9D)

Checks whether the predicate is not nil for one element combination.

```c
(vl-some predicate-function lst [lst ...])
```

predicate-function. Type: Subroutine or Symbol. The test function. This can be any function that accepts as many arguments as there are lists provided with vl-some, and returns T on a user-specified condition. The predicate-function value can take one of the following forms:

lst. Type: List. A list to be tested.

Return Values. Type: List or nil.

The predicate value, if predicate-function returned a value other than nil; otherwise nil.

Remarks. The vl-some function passes the first element of each supplied list as an argument to the test function, then the next element from each list, and so on. Evaluation stops as soon as the predicate function returns a non-nil value for an argument combination, or until all elements have been processed in one of the lists.

Examples

The following example checks whether nlst (a number list) has equal elements in sequence:

```c
(setq nlst (list 0 2 pi pi 4))
(0 2 3.14159 3.14159 4)

(vl-some '= nlst (cdr nlst))
T
```

自己写了一个例子：

```c
(defun foo () 
  (vl-some '(lambda (x) (= x 2)) 
    '(1 3 4 5 2)
  )
)
```

』

When processing a nested list that contains our item, (vl-some) returns T but it returns it to itself because it was called from a function it was using. And because a T was returned to it, it then returns a T. So with our example, calling (item-in-list mylist 13) would return T while calling (item-in-list mylist “Cat”) would return NIL because it's not contained in any of the data in the list or nested lists.

Now that you've seen a couple examples, it's really not that hard. In fact, the hardest part of writing a program that uses recursion, is to make sure the program has an “out” or at some point stops processing and doesn't just blindly call itself forever. But it takes a while; you won't be an expert just by reading this. You'll become and expert only after using this technique many times. To help you with this, Here's a little sample code. This code was posted to the AutoCAD's Customization discussion group. It was created by Owen Wengerd ([ManuSoft Home](http://www.manusoft.com/) & [Cadlock.com](http://ww1.cadlock.com/)) and is a very good example of short, well-written recursive program.

```c
(defun Str+ (source / prefix rchar) 
  (cond 
    ((= source "") "A") 
    ((= (setq prefix (substr source 1 (1- (strlen source))) 
              rchar (substr source (strlen source))
        ) 
        "Z"
     ) 
     (strcat (Str+ prefix) "A") 
    ) 
    ((strcat prefix (chr (1+ (ascii rchar)))))
  )
)
```

What this codes does, it takes a string character and increments it. Its intent is to generate the next revision letter based in the current revision. So Let's say your drawing is at revision “B”, calling the function (str+ “B”) would return “C”. Calling the program with (str+ “C”) would return “D” and so on. that's not that hard in itself, and you wouldn't need recursion to perform it. But what happens when you get to revision “Z” and need to go to “AA” or you're at revision “AZ” and need to go to “BA”. This program handles that and that's where the recursion comes in. So your homework when you get back to your office is to slice and dice this program up and see how it works. Play with it a little and see if you can truly understand what it's doing. And if you're really ambitious, try modifying the program so that it works as described, but does Not use the letters “O” (oh) and “I” (eye) which resemble 0 (zero) and 1 (one). Use the following lines to make notes on recursion, this class or how you might use it in your own environment.

### 1.3 Visual LISP Primer

#### 1.3.1 Why Visual LISP? – 2905 Reasons, That's Why!

If you've ever wondered what's in Visual LISP that might make it attractive for you to use, Here's a little teaser to peek your interest.

- 80 Visual LISP function (those prefixed with VL-)

- 1971 ActiveX function specific to AutoCAD's object model. (those beginning with “vla-“ prefix)

- 47 Reactor functions (those beginning with “vlr-“ prefix)

- 121 Reactor types or event triggers (those beginning with “:vlr-“ prefix)

- 118 Generic ActiveX functions (those beginning with “vlax-“ prefix)

- 946 ActiveX constants (those beginning with “ac”, “acrx-”, and “:vlax-”) 

Of course there are more than just additional functions that make it attractive. For starters, you can step through your code line-by-line, watching where control flows and the values of variables as they are changed. Look at A in the following image. You can add breakpoints to your code then use one of the buttons marked C to load the code with breakpoint information into memory. At the bottom of the screen E, you can then call your code and it will pause at the breakpoint. The Watch Window B then displays your variable's values (you need to add which ones you want to watch) as you manually step through the code using the buttons marked D.

When you use the Visual LISP editor it makes troubleshooting your code a lot easier with this ability. You can easily see where, when as well as why some variables are not containing the information you think they are which in turn allows you to more quickly fix the issue.

Of course, there are still other benefits to using the Visual LISP editor. As you likely already know, it allows you to build compiled AutoLISP files such as FAS (Fast load AutoLISP Source) and VLX (Visual Lisp Applications). Contrary to popular belief, there are a lot of reasons to compile your projects other than to protect the source code.

1『目前还是觉得写 autolisp 代码在 vscode 里舒服。（2020-10-27）』

One of the benefits of creating FAS files is that you can build them from a project. And a project, as shown in the image to the left, can have a number of AutoLISP files defined in it. What does this do for you? You can more easily build libraries of reusable utility functions that you can access from your code. In the example to the left, the TicketAutomation project is referencing utilities that work with the Registry, Solids, Plines, Coordinates, Dimensions and Blocks. This code isn't copied and pasted to he new AutoLISP file, it's just referenced and then compiled into the same FAS file (or separate if you like). As more functions are added to the library code or the existing ones updated, a quick recompile of the project, and any other projects that use that library code are then updated. It makes code sharing and reuse a lot easier.

1-2『上面的插件集成，直觉上会用到，待实践。』——未完成

Still another advantage of the Visual LISP editor is the ability to compile Applications (VLX). Similar to Projects which build FAS files, Visual LISP applications offer a lot more options, including the ability to include within them, other projects, Lisp source code, compiled Lisp code (FAS), text files and even DCL dialog files. All this within one file makes distributing more complex programs and applications a lot simpler. there's even an option to compile the Visual LISP Application in such a way that it runs in its own namespace which means all the code and variables run in it's own protected memory space. If you've ever had an AutoLISP program fail because another program used the same variable name and it was set to something different then your program expected, compiling an application to run in a separate memory name space would solve this problem.

1『上面有关「分割内存空间」的技巧，直觉上以后也会用到。』

there's simply a lot in the Visual LISP editor, which makes it very worth your while to learn how to use it. Unfortunately, there's just too much to cover completely in this course, which is why we've just covered some of the major highlights that can really affect your coding productivity.

#### 1.3.2 Reactors – Code That Knows Not Just What To Do, But When To Do It

Another nice thing about Visual LISP is the ability to create Reactors. Reactors are event triggers. That is, when certain “events” happen within your drawing or AutoCAD, the “trigger” calls some code or action. You, the programmer, define all the Events and the Actions that the Triggers call. Reactors aren't that difficult to master, but there are a few things to know so here's a rundown.

First, there are two types of Reactors, Transient and Persistent. Transient reactors are not saved with the drawing and are the default method when Reactors are created. If a Reactor is transient, and you want it to apply to a drawing all the time, you need to add it each time the drawing is loaded. If you want a Persistent reactor, you need to add a reactor (it'll be transient) then convert it to Persistent. Persistent reactors are saved in the drawing and do not need to be added again unless they are intentionally removed with other AutoLISP code.

Second, regardless if a Reactor is transient or persistent, know that the reactor itself is just a trigger that calls an AutoLISP function. If the functions the Reactors are supposed to call are not loaded, the reactors will give the user an error. For this reason, transient reactors are typically all that's needed in most cases because if you make considerations for loading the code the reactors call, you might just as well load the reactor anyway as well.

Third, when you review the VLR- functions in the AutoLISP reference, you will see some function names that refer to “Reactors” and a few that refer to “Reactions”. There are 19 Reactors and each Reactor has one or more Events. These Events are what the Reaction functions are talking about. For example, there is a `:vlr-DWG-Reactor` that deals with things that happen to the drawing database. That particular Reactor has 8 Events or Reactions that it can use which are `:vlr-beginClose`, `:vlr-databaseConstructed`, `:vlr-databaseToBeDestroyed`, `:vlrbeginDwgOpen`, `:vlr-endDwgOpen`, `:vlr-dwgfileOpened`, `:vlr-beginSave`, and `:vlr-saveComplete`.

Fourth, the callback function is the function the reactor calls. Each callback function takes two arguments, one (the first) holds the event name that ended up calling the code, the other contains any other data (if any) that that particular event may pass back. The event `:vlrcommandEnded` for the `:vlr-command-reactor` for example, will pass a string indicating the command name that ended.

Now that those issues have been addressed, Let's look at some example code. The following code needs to be run manually. The function (save-pre) and (save-post) are callback functions that will be called when you save a drawing. The command `(c:Load-My-Reactor)` will create different event reactors for the `:vlr-DWG-Reactor` reactor. Once you load the AutoLISP code into memory, run at the command line Load-My-Reactor. Nothing will appear to happen but something actually did, the Reactor had 2 different event triggers added to your drawing. When you save your drawing, You'll be alerted pre-save and post-save with an alert box.

```c
;;; Load Up The Reactor 
(defun c:Load-my-reactor ( / myreactor) 
  (vl-load-com) 
  (setq myreactor (vlr-dwg-reactor 
                    "This is my SAVE Reactor" 
                    '((:vlr-beginSave . save-pre) 
                      (:vlr-savecomplete . save-post)
                    )
                  ) 
  ) 
  (vlr-add myreactor)
)

;;; Pre-Save Reactor Callback 
(defun save-pre (reactor data) 
  (alert (strcat "Drawing is about to be saved by " 
                 (getvar "loginname")
         )
  ) 
)

;;; Post Save Reactor Callback 
(defun save-post (reactor data) 
  (alert (strcat "Drawing has been saved by " 
                 (getvar "loginname")
         ) 
  ) 
)
```

Now, because these Reactors are transient, if you close and reopen your drawing, future drawing saves will not show the alerts unless you recreate the reactors again by running the code again. If you want a reactor to be present all the time in your drawing file, you will want to add code to your `ACAD/ACADDOC.LSP` file for this purpose.

Now, something that's less known, is that you can add the same reactor more than once. If you load the code above and run the command Load-My-Reactor several times, when you save your drawing You'll get several messages. Typically if you are adding reactors upon drawing open, this isn't a big issue. But if you have code that's manually initiated by a user, like in this example, it's possible to add the reactor more than once, which may cause you problems. For this reason, it's wise to verify if the reactor is loaded already first, before adding it to your drawing. The following 2 functions will do this for you.

```c
;;; VLisp Reactor - Is Reactor Loaded ?
;;; Call: (au:vlr-loaded-p fname {rtype} {revnt}) ;;; Return: T/nil 
;;;___________________________________ 
;;; fname = Function name / 'function 
;;; rtype = Reactor type / :vlr-xxxx-Reactor 
;;; revnt = Reactor event / :vlr-xxx 
;;;___________________________________ 
;;; Dependent Functions...
;;; au:vlr-fun-eq-cback 
;;;___________________________________ 
(defun au:vlr-loaded-p (fname rtype revnt / au$reactors) 
  (if fname 
    (progn 
      ;; Get List of Reactor Types w/Reactors Loaded - If Any 
      (if (vl-member-if '(lambda (i) (eq i rtype)) (vlr-types) ) 
        (setq au$reactors (vlr-reactors rtype)) 
        (setq au$reactors (vlr-reactors)) 
      ) 
      ;; Check If Reactor Callback Loaded 
      (vl-some 
        '(lambda (i) 
          ;; Check If Reactor Callback Loaded For Any Reactor 
          (vl-some 
            '(lambda (ii) 
              ;; Check If Reactor Callback Loaded For Each Reactor 
              (au:vlr-fun-eq-cback fname ii revnt) 
             ) 
            i 
          )
         ) 
        (mapcar 'cdr au$reactors)
      )
    ) 
    nil
  )
)
```

```c
;;; VLisp Reactor - Is Function Equal To Callback 
;;;___________________________________ 
;;; (au:vlr-fun-eq-cback 'fname robj {revnt}) 
;;;___________________________________ 
;;; fname = Function name / 'function 
;;; robj = Reactor object / reactor 
;;; revnt = Reactor callback event / :vlr-? 
;;;___________________________________ 
;;; Dependent Functions...
;;; N/A 
;;;___________________________________ 
(defun au:vlr-fun-eq-cback (fname robj revnt / au$revnt-list) 
  ;; Get Reactions 
  (setq au$revnt-list (vlr-reactions robj)) 
  ;; If Event Specified, Restrict To Event - Else Look At All 
  (if revnt
    ;; Restrict To Event
    ;; If Function Name = Reactor Callback
    (if (eq fname (cdr (assoc revnt au$revnt-list))) 
      T 
      nil
    )
    ;; Else Look At all
    (vl-some 
      '(lambda (i) 
         (eq fname (cdr i))
       ) 
      au$revnt-list
    )
  )
)
```

The explanation of all that these two functions do and how they do it is beyond what we have time for here in this class. However, note that the function `(au:vlr-loaded-p)` is the only function you need to call. The second function is used only by the first. The comments at the heading of the function explain how to call it, but essentially, you call the function and pass the quoted callback function, the reactor, and the event/reaction as parameters and the code will then return T if that function is already associated with that event or that reactor. If it's not, then it will return NIL. With that in mind, we can modify the Load-My-Reactor code to the following to keep it from loading the reactors more than once.

```c
;;; Load Up The Reactor (load only once) 
(defun c:Load-my-reactor (/ myreactor) 
  (if (and 
        (not (au:vlr-loaded-p 
               'save-pre 
               :vlr-dwg-reactor 
               :vlr-beginsave
             )
        ) 
        (not (au:vlr-loaded-p 
               'save-post 
               :vlr-dwg-reactor 
               :vlr-savecomplete
             )
        )
      )
      (progn 
        (vl-load-com) 
        (setq myreactor (vlr-dwg-reactor 
                          "This is my SAVE Reactor" 
                          '((:vlr-beginSave . save-pre) (:vlr-savecomplete . save-post))
                        ) 
        ) 
        (vlr-add myreactor)
      )
  )
)
```

Some other things that are important to know about reactors are that you shouldn't prompt for user input or call the (command) function in a reactor's callback function. While it can be done successfully in some cases, it can also cause problems because some reactors fire while commands are still active. don't count on being able to do this and be prepared for problems. Also note that just like with recursive programming, it's possible to have a reactor fire itself. That is, if your save reactor saved the drawing, or if an object reactor modified an object, it could fire itself resulting in an endless loop. You'll need to make programming considerations in your code to check for those conditions to prevent them from occurring. The most common method is to have your callback function check for the value in a variable, and if it's not set, set it and proceed with the callback function. If the event triggers itself, it'll see that the variable is already set and not finish. Just don't forget to clear the flag when your code is finished processing whatever it's doing.

there's a lot to reactors. Review the AutoLISP reference for the various types of reactors available as well as their events and the various functions that help you manage reactors. If you're ambitious, dissect the 2 utility functions I've supplied and see how they work. If you can understand the logic and workings of those 2 utility functions, You'll have already mastered programming reactors in Visual LISP.

### 1.4 ActiveX – The Power Of Visual Basic In Visual LISP

There are a number of additional functions in Visual LISP that provide ActiveX functionality inside of AutoCAD and other applications. These functions aren't initially available inside Visual LISP unless support for them has been explicitly loaded. You can load and access these ActiveX functions easily with the Visual LISP function `(vl-load-com)`.

1『又见 `(vl-load-com)` 语句，只有先加载，才能使用 ActiveX 相关的功能。（2020-10-27）』

These ActiveX functions provide access to the methods, and properties of the AutoCAD object model as well as supporting functions and those that provide access to the object models of other applications that support ActiveX. If you browse through the AutoLISP Reference (in AutoCAD's Developer Help), You'll see the reactor (vlr-) and (vlax-) based ActiveX functions listed. The vlax-based functions are more generic in nature and therefore covered fairly well in the AutoLISP Reference. The vla- functions on the other hand, are a different story. You won't find a list of them or documentation of them anywhere in AutoCAD's help system. In fact there's likely not a complete list or explanation of the vla- Visual LISP functions anywhere on the planet other the smaller lists of certain functions that people have put in CAD books or on their CAD based web sites. Nowhere have I found a complete list of them with explanations let alone sample code. Just looking at the sheer number of the functions involved, this likely explains why that is. The question then comes to mind, if these ActiveX Visual LISP functions aren't listed anywhere, then how does someone find out about them, let alone figure out how to use them? You'll find out how in this section of this course.

To start with, You'll need to be familiar with what's referred to as AutoCAD's “Object Model”. it's a tree like structure that holds everything related to AutoCAD. In essence, it's a family tree for all things AutoCAD. Other software programs that support ActiveX automation have object models too. This “Object Model” is how an ActiveX based application defines the database structure of AutoCAD and defines its properties and methods. Oh, yea, I almost forgot to tell you, “Methods” are the term used for “functions” when dealing with ActiveX automation.

1-3『

[Object Model (ActiveX)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-A809CD71-4655-44E2-B674-1FE200B9FE30#GUID-A809CD71-4655-44E2-B674-1FE200B9FE30)

这张大的，CAD 树形数据对象图，以后铁定有大用，会成为自己实现深度学习功能的基石。（2020-10-27）

』

To give you an idea of what an object model looks like, You'll have to go to AutoCAD's ActiveX and VBA Reference. From the image at the top of this page, you can see where to access in the AutoCAD Developer help system, a view of AutoCAD's Object Model. You'll be accessing this information almost constantly if you're going to be doing ActiveX automation from Visual LISP until you become more familiar with its use.

When you get to the Object Model in the ActiveX and VBA Reference, clicking on any of the items in the Object Model will display information for that item. You'll also notice by looking at the object model that there are rectangular shapes with square corners and rectangular shapes with rounded corners. Looking at the legend, you can see that those with square corners are a Collection and those with rounded corners are an Object.

A Collection is really a type of object as well but it's special in that it really doesn't do much other than contain and group other objects. Every Layer in AutoCAD is stored and accessed in the Layers collection. Every Block is stored and accessed in the Blocks collection and every drawing entity (line, arc, circle, text, dimension, etc.) is stored and accessed in either the ModelSpace, PaperSpace collection or the Block object.

1『这里出现了一个重要的概念「Collection」。（2020-10-27）』

So to start, Let's look at a Line in the Object Model (Application -> Documents -> Document -> ModelSpace -> Line). If you look at the help for the Line object, You'll see several Methods, Properties and Events listed. If you look at the Properties specifically, You'll see one of those is for Length. From AutoCAD's Object Model, you can directly extract a Line's Length instead of calculating it with the (distance) function in AutoLISP. You'll find a lot of these useful properties for the various entities in AutoCAD that you previously needed to calculate yourself in AutoLISP. But now with the ActiveX functionality in Visual LISP, you can get access to a lot of this information quicker than ever before.

1-3『

[Line Object (ActiveX)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-2A2C2B78-3B64-4083-A8EC-984DB223053F#GUID-2A2C2B78-3B64-4083-A8EC-984DB223053F)

[Length Property (ActiveX)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-6D7C13B5-1DAB-4591-80E5-8C05923331F3)

```c
(vl-load-com)
(defun c:Example_Length()
    ;; This example adds a line in model space and returns the length of the new line
    (setq acadObj (vlax-get-acad-object))
    (setq doc (vla-get-ActiveDocument acadObj))

    ;; Define the start and end points for the line
    (setq startPoint (vlax-3d-point 1 1 0)
          endPoint (vlax-3d-point 5 5 0))

    ;; Create the line in model space
    (setq modelSpace (vla-get-ModelSpace doc))
    (setq lineObj (vla-AddLine modelSpace startPoint endPoint))

    (vla-ZoomAll acadObj)
    
    (alert (strcat "The length of the new Line is: " (rtos (vla-get-Length lineObj) 2)))
)
```

你不用从起点到终点计算 line 的长度，可以直接读取 line 这个对象的 length 属性。同样，CAD 很多其他的对象数据都有很多属性，直接读取出来的话可能有大用。这里关于属性的信息很值得深思。（2020-10-27）

』

But the question still remains, how do you take this information in the Visual Basic documentation and turn it into an ActiveX function in Visual LISP? The answer is that you already have all the information you need; you just need to know how to translate it. And the key is this…Visual LISP ActiveX functions specific to the object model take on a predictable format. For starters, they all start with “vla-“. Next, are you extracting a property or setting a property? If you are extracting a property, the next part of the function is “get-“ and if you are setting a property, the next part of the function is “put-“. And finally, the last part of the function name is the property name in VBA. In this example, that's “length”. So, to extract the length of a line, the name of our Visual LISP function would by `(vla-get-length)`.

If you notice in the documentation, Length is a Read-Only property. That means you can't “set” the property and therefore there isn't a `(vla-put-length)` function in Visual LISP. If the property was not Read-Only, there would be a corresponding `vla-put-<VBA Property>` function. This format is the same for ALL properties You'll find in the ActiveX and VBA Reference. With this format information, you now know how to figure out the ActiveX Visual LISP function for every property in the AutoCAD Object Model. Very easy don't you think? To make sure you have the proper function name, you can easily test this by typing the function in the Visual LISP editor, making note of its color. don't forget to call `(vl-load-com)` function first. Typically, you would call `(vl-load-com)` once in every AutoLISP program you write that uses ActiveX but in reality, once it's called, it stays loaded for the entire AutoCAD session.

Now that you know how to figure out the ActiveX functions in Visual LISP for getting or setting an ActiveX property, the next thing to figure out is what the names of the Visual LISP functions are for ActiveX methods. This information you also had previously. If you look back at the help information for the Line object, You'll see that it says it can be created with the AddLine method. This is the key to figuring out the function name. Again, the beginning of any AutoCAD Object Model specific function in Visual LISP starts with “vla-“. Only this time, you just add the method name. This would make the ActiveX Visual LISP function to create a line `(vla-addline)`. This format holds true for ALL ActiveX methods in Visual LISP, they are named in exactly the same way. Again, this can be verified by typing it in the Visual LISP editor, making note of the color of the function name.

Now you're armed with all the information you need to figure out what all the 1710 different Visual LISP ActiveX functions are. The only thing left if to figure out how to use them but that will come shortly. Next, we'll explore a couple different ways other than the ActiveX and VBA Reference to find these types of function names. For starters, you can list all of these functions right from within the Visual LISP editor. To do this, all you need is the Apropos function in the editor.

You'll notice that there's just too many entries to list all at once so to see all of them You'll have to search for prefix strings like “vla-a” or “vla-r”. This can come in handy, after you've used ActiveX Visual LISP functions for a while and you already know how to call them but just need a quick refresher on their spelling or need to quickly browse for a function that you know exists but don't quite recall how it was spelled. But there's also another easy way to browse this type of information in its Visual Basic format. To do this, start the VBA editor by selecting Tools -> Macro -> Visual Basic Editor in AutoCAD (not the Visual LISP IDE) from the pull down menu. Once in the VBA editor, open the “Object Browser” by selecting View -> Object Browser from the pull down menu.

The Visual Basic editor opens the Object Browser with it set to display the AutoCAD Object Model library. Using this object browser won't help a whole lot when you first start using ActiveX in Visual LISP but its most likely the preferred way to look for objects & methods after you're familiar and comfortable with using ActiveX in Visual LISP.

Now that you know of several ways to find Visual Basic methods and properties and convert that data into a Visual LISP function, the next step is to figure out how to call them. This is the most difficult part by far of working with ActiveX objects in Visual LISP. The first task will be to get the length of a line in AutoCAD with the (vla-get-length) function that we determined we needed earlier to extract this type of information.

If you look at the Help section for this, You'll see the signature for using this property is object.length. This is how this property is used in Visual Basic. Object is the AutoCAD object that you're using the property on and Length is the property you're using on that object. In Visual Basic, there are often parameters associated with methods. Properties on the other hand are generally just set with an “=” in Visual Basic. In the case of the Read-Only Length property, there are no arguments that go along with it in Visual Basic. The only information it needs, is the object that is specified prior to the property and separated with a period. In Visual LISP, this object needs to be specified as an argument (parameter). it's always the first argument in the function. If the property or method as listed in the ActiveX and VBA Reference has additional arguments or values to set, they are listed after the object argument in the same order that they appear in the ActiveX and VBA Reference documentation.

To extract the length of a line, you would call the `(vla-get-length)` function passing to it a Line object. Because you are using ActiveX methods and properties, your arguments need to be ActiveX arguments as well. This means that you can't just pass an entity name to the function like you are use to doing in AutoLISP but instead it must be converted to an ActiveX object. This is done with one of the more generic ActiveX Visual LISP functions `(vlax-ename->vlaobject)`. Here's how it would look…

Notice that we first called `(vl-load-com)`. If this was done previously in this session of AutoCAD, there's no need to do it again. If you do call it again, it does nothing so calling it when it's not needed is not a problem. Next, we selected a line and determined its entity name. It was then converted to a ActiveX Line Object with the help of the `(vlax-ename->vla-object)` function. Once that was done, we could then use the (vla-getlength) function to extract the length of the line with the function being called in the in the following format… `(vla-get-length lineobject)`.

As any good programmer knows, error checking is always an important factor. With that in mind, what if the operator selected something that didn't have a length property like a piece of Text? The answer is by using the (vlax-propertyavailable-p) function that is documented in the Visual LISP Reference. This will tell us if the property we want to use is valid for the object selected. This function requires the Line object and the property quoted as an argument.

Here's how this would look with this type of error checking…

You'll see that by first testing what we think is a Line object; we can make certain that a Length property is indeed available for the selected object. You should also start noticing that the vlaxfunctions go hand in hand with the vla- functions.

Now that we can extract a property, Let's try setting one. This property will be the Layer property. Using the function naming convention we outlined earlier, the function would start with “vla-”. The next part of the function would be “put-” because we are setting a property or “Putting” a value in that property. Finally, the property itself is “Layer”. This would make the Visual LISP ActiveX function (vla-put-layer).

Because the Layer property is not Read-Only that means it can be set with a value indicating the new layer. But according to the format of how these functions are called, we need to specify the Line object first so that will be our first argument to the function. The next thing is the value for the Layer name. This would then be the second argument to the function. Calling that function would look something like this… (vla-put-layer lineobject layername).

I know you're catching on to all this so this example includes error checking. It also includes an additional error checking function (vlax-write-enabled-p) that will tell you if the specified object is allowed to be modified or not. This would prevent an error if for some reason a particular object couldn't be modified. The only thing to watch here is that the Layer you are going to change to already exists in the drawing.

This covers extracting and setting properties quite well. The next thing we need to cover is Methods. For this example, we'll create a line using ActiveX in Visual LISP.

From the help for the AddLine method, you can see that Visual Basic requires two arguments. In addition, the Object lists several possibilities. The Modelspace collection, Paperspace collection and a Block object. That means that a Line needs to be in either Paperspace, Modelspace or part of a Block definition. In this case, we'll be adding it to the Modelspace collection. What this means is that our (vla-addline) function will need three parameters, the Modelspace object being the first parameter, and Start Point as the second and the End Point as the third.

we'll start with the first parameter. This is the Modelspace collection object. You can't really just select the Modelspace object in AutoLISP so the (vlax-ename->vla-object) function that was used before doesn't really help in this case. For this task, you need to start from the root of the Object Model and that's the Application Object. To get the application object, you can use the (vlax-get-acad-object) function.

Now if you look at the Application Object from the Object Model in the help, You'll see there's an ActiveDocument property. This gives you the object of the currently open, active document in the Documents collection.

With AutoCAD being able to have multiple documents open at once, each open document is stored in the Documents collection. You could iterate through all the different documents in the documents collection until you get to the one document with it's Active property set to True but this ActiveDocument property is a shortcut through all that work. Now that you know how to get the application object, and how to get to the document level, you can figure out how to get the document object. You'll use the (vla-get-activedocument) function passing the Application object as its argument.

Finally, from the Document object, you need to get to the ModelSpace object. If you look at the Document object (not the Documents collection – remember we skipped past it with ActiveDocument), You'll see the Modelspace property. This property returns the ModelSpace collection which is what we need to tell Visual LISP where to add the line. To jump to the ModelSpace collection object, You'll be using the (vla-get-modelspace) function that returns the Modelspace object we need. The code we'll eventually end up using looks something like one of these two examples. You'll see one takes each, one step at a time (if you think You'll need the Application or ActiveDocument objects again) and the other does them all at once (if you won't need the Application or ActiveDocument objects again later).

The next step is getting the points we need for the start and end of the line. Looking back at the AddLine method, You'll see it specifies the StartPoint and EndPoint as a Variant – 3 element Array of Doubles. A “Double” is a Visual Basic data type similar to a Real number. And Array, is Visual Basic's equivalent to a List. And funally, a Variant, is a special Visual Basic data type that can hold any data type (string, real, double, etc.).

This is a lot different that how AutoLISP specified points with a list of three Real numbers. It sounds complicated but once you get use to it, it's not a big deal, it still takes a little while to see and understand what's really going on. The best way to see how a point like this is structured is to extract a point from an existing line and look at how it's structured. This way, AutoCAD shows you what it uses, and then you can duplicate it. Let's look at the endpoint of the line we previously changed the layer of using the (vla-get-startpoint) function.

Now that you have the Variant as it was returned by the StartPoint property using the code shown in the image above, you can examine it further with the Inspect tool in the Visual LISP editor.

As you can see, by using the Inspect tool, and double clicking on the results, you can progressively work your way into the contents of the variable deeper and deeper to see exactly how it's constructed. You can also see that the end result is a list of three Real numbers. This is where we'll start to build our point. Next, this list needs to be built into a Safe Array. This can be done with the (vlax-make-safearray) function. This function is called with a couple arguments which are explained as follows…

```c
(vlax-make-safearray type ‘(l-bound . u-bound) *‘(l-bound . u-bound)+…) 

type = Constant or Integer indicating the type of the safe array 
        vlax-vbInteger (2) 
        vlax-vbLong (3) 
        vlax-vbSingle (4) 
        vlax-vbDouble (5) 
        vlax-vbString (8) 
        vlax-vbObject (9) 
        vlax-vbBoolean (11) 
        vlax-vbVariant (12) 
l-bound = lower array limits (integer) 
u-bound = upper array limits (integer)
```

Calling this function just initializes the array. It doesn't actually put any data values in it. To fill the array with values, You'll use the function (vlax-safearray-fill). This fills the data into the array that was just created. Once this is done, you can convert this safe array into a variant by using the (vlax-make-variant) function. Here's a description of (vlax-make-variant).

```c
(vlax-make-variant [value] [type])

value =  The value to be assigned to the variant
type = Constant or Integer indicating the type of variant 
        vlax-vbEmpty (0) 
        vlax-vbNull (1) 
        vlax-vbInteger (2) 
        vlax-vbLong (3) 
        vlax-vbSingle (4) 
        vlax-vbDouble (5) 
        vlax-vbString (8) 
        vlax-vbObject (9) 
        vlax-vbBoolean (11) 
        vlax-vbArray (8192)
```

After this last step, the point in now ready for use by Visual LISP's (vla-addline) function. Here's how it would look to create this point in the Visual LISP editor. Notice that when the function (vla-safearray-fill) is used, you don't need to save its return value although you can if you like.

This is a lot of work just to get a point for use in Visual LISP ActiveX. You could always make a wrapper function to do this or, you could use the easier to use function (vlax-3D-point). This function takes a list, or separate coordinate data like you are use to dealing with in AutoLISP and returns a safe array. Let's take a look at how that's done for the Line's EndPoint.

You can see from this image, that it's a lot easier with this function to create a 3d point. This is really the best way to go about it. The only reason I showed you the other method was because there are times when working in ActiveX from Visual LISP that You'll need to create an array in a similar fashion when it doesn't involve point coordinates.

So now that we have out ModelSpace collection object and our two points for the start and ending of the line, we're ready to use the (vla-addline) function to create a new line in AutoCAD. This is done by calling the function as we discussed earlier and looks something like this…

don't forget to save the results of your (vla-addline) function to a variable. This function returns the created Line ActiveX object that can then be used if you want to set the Layer or Linetype or some other property of the newly created line.

You now should have enough information to do just about anything in AutoCAD that its object model supports. you've extracted and set property values for existing geometry. you've also created geometry from scratch. don't worry that all you did was change and create a line.

If you are familiar with the AutoCAD Object Model and follow the procedures demonstrated here, You'll have enough information to find out what the Visual LISP ActiveX function is named, and You'll be able to find out how to call it. Just remember that if a particular function requires an argument and you don't understand what format it's looking for, the easiest thing to do is to create the same thing manually in AutoCAD. Using Visual LISP and its editor, you can then extract the existing value of what you created manually to figure out what you need to do in your code. it's a simple technique but it'll have you lots of headaches in the end.

2-3『

[Autodesk University](https://www.autodesk.com/autodesk-university/zh-hans)

找到了作者在 AutoCAD 官方文档里的教学视频：[Advanced AutoLISP | Autodesk University](https://www.autodesk.com/autodesk-university/zh-hans/forge-content/au_class-urn%3Aadsk.content%3Acontent%3A804989f7-dee0-411e-9f9f-cf0bc6b09aad)。视频值得消化吸收，并转为为文字版。

Learning Objectives: 1) Learn how to use advanced Autolisp functions. 2) Understand advanced concepts like recursion. 3) Understand how reactors work. 4) Learn how to use the nearly 2000 undocumented Autolisp functions.

』——未完成