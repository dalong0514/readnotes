# 2020080PHP-and-MySQL-Web-R02

## 记忆时间

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

## 03. Using Arrays

This chapter shows you how to use an important programming construct: arrays. The variables used in the previous chapters were scalar variables, which store a single value. An array is a variable that stores a set or sequence of values. One array can have many elements, and each element can hold a single value, such as text or numbers, or another array. An array containing other arrays is known as a multidimensional array.

PHP supports arrays with both numerical and string indexes. You are probably familiar with numerically indexed arrays if you’ve used any other programming language, but you might not have seen arrays using string indexes before, although you may have seen similar things called hashes, maps, or dictionaries elsewhere. Rather than each element having a numeric index, you can use words or other meaningful information.

1『 php 里的数组，键为字符串的类型，其实就是 python 里的字典、JS 里的对象。』

In this chapter, you continue developing the Bob’s Auto Parts example using arrays to work more easily with repetitive information such as customer orders. Likewise, you write shorter, tidier code to do some of the things you did with files in the preceding chapter. Key topics covered in this chapter include: 1) Numerically indexed arrays. 2) Non-numerically indexed arrays. 3) Array operators. 4) Multidimensional arrays. 5) Array sorting. 6) Array functions.

In the next chapter, you will learn about string processing functions. We cover functions that search, replace, split, and merge strings, as well as the powerful regular expression functions that can perform almost any action on a string.

### 3.1 What Is an Array?

You learned about scalar variables in Chapter 1「PHP Crash Course.」A scalar variable is a named location in which to store a value; similarly, an array is a named place to store a set of values, thereby allowing you to group variables. Bob’s product list is the array for the example used in this chapter. In Figure 3.1, you can see a list of three products stored in an array format. These three products are stored in a single variable called \$products. (We describe how to create a variable like this shortly.)

Figure 3.1  Bob’s products can be stored in an array

After you have the information as an array, you can do a number of useful things with it. Using the looping constructs from Chapter 1, you can save work by performing the same actions on each value in the array. The whole set of information can be moved around as a single unit. This way, with a single line of code, all the values in the array can be passed to a function. For example, you might want to sort the products alphabetically. To achieve this, you could pass the entire array to PHP’s sort() function.

1『数组、字典的强大在于可以循环遍历。』

The values stored in an array are called the array elements. Each array element has an  associated index (also called a key) that is used to access the element. Arrays in many programming languages have numerical indices that typically start from zero or one.

PHP allows you to interchangeably use numbers or strings as the array indices. You can use arrays in the traditional numerically indexed way or set the keys to be whatever you like to make the indexing more meaningful and useful. (This approach may be familiar to you if you have used associative arrays, maps, hashes, or dictionaries in other programming languages.) The programming approach may vary a little depending on whether you are using standard numerically indexed arrays or more interesting index values. We begin by looking at numerically indexed arrays and then move on to using user-defined keys.

### 3.2 Numerically Indexed Arrays

Numerically indexed arrays are supported in most programming languages. In PHP, the indices start at zero by default, although you can alter this value.

#### 3.2.1 Initializing Numerically Indexed Arrays

To create the array shown in Figure 3.1, use the following line of PHP code:

```php
$products = array( 'Tires', 'Oil', 'Spark Plugs' );
```

This code creates an array called \$products containing the three values given: 'Tires', 'Oil', and 'Spark Plugs'. Note that, like echo, array() is actually a language construct rather than a function.

1『知识点：array() 是个 language construct 而非函数。』

Since PHP 5.4, you can use a new shorthand syntax for creating arrays. This uses the [ and ] characters in place of the array() operator. For example, to create the array shown in Figure 3.1 with the shorthand syntax, you would use the following line of code:

```php
$products = ['Tires', 'Oil', 'Spark Plugs'];
```

1『以后就用 [] 来构建数组，跟 python、JS 语法保持一致。』

Depending on the contents you need in your array, you might not need to manually  initialize them as in the preceding example. If you have the data you need in another array, you can simply copy one array to another using the = operator. If you want an ascending sequence of numbers stored in an array, you can use the range() function to automatically create the array for you. The following statement creates an array called numbers with elements ranging from 1 to 10:

```php
$numbers = range(1,10);
```

The range() function has an optional third parameter that allows you to set the step size between values. For instance, if you want an array of the odd numbers between 1 and 10, you could create it as follows:

```php
$odds = range(1, 10, 2);
```

The range() function can also be used with characters, as in this example:

```php
$letters = range('a', 'z');
```

1『 range() 函数的用法跟 python 一样一样的。』

If you have information stored in a file on disk, you can load the array contents directly from the file. We look at this topic later in this chapter under the heading「Loading Arrays from Files.」If you have the data for your array stored in a database, you can load the array contents directly from the database. This process is covered in Chapter 11「Accessing Your MySQL Database from the Web with PHP.」You can also use various functions to extract part of an array or to reorder an array. We look at some of these functions later in this chapter under the heading「Performing Other Array Manipulations.」

#### 3.2.2 Accessing Array Contents

To access the contents of a variable, you use its name. If the variable is an array, you access the contents using both the variable name and a key or index. The key or index indicates which of the values in the array you access. The index is placed in square brackets after the name. In other words, you can use \$products[0], \$products[1], and \$products[2] to access each of the contents of the \$products array. You may also use the { } characters to access array elements instead of the [ ] characters if you prefer. For example, you could use \$products{0} to access the first element of the products array.

1『 php 里提取数组的元素，除了常规的 [] 还能用 {}。』

By default, element zero is the first element in the array. The same numbering scheme is used in C, C++, Java, and a number of other languages, but it might take some getting used to if you are not familiar with it. As with other variables, you change array elements’ contents by using the = operator. The following line replaces the first element in the array, 'Tires', with 'Fuses':

```php
$products[0] = 'Fuses';
```

You can use the following line to add a new element—'Fuses'—to the end of the array, giving a total of four elements:

```php
$products[3] = 'Fuses';
```

To display the contents, you could type this line:

```php
echo "$products[0] $products[1] $products[2] $products[3]";
```

Note that although PHP’s string parsing is pretty clever, you can confuse it. If you are having trouble with array or other variables not being interpreted correctly when embedded in a double-quoted string, you can either put them outside quotes or use complex syntax, which we discuss in Chapter 4「String Manipulation and Regular Expressions.」The preceding echo statement works correctly, but in many of the more complex examples later in this chapter, you will notice that the variables are outside the quoted strings.

1『确实，很多时候用 echo 用不好，碰到问题就直接改用 vardump() 了。（2020-04-25）』

Like other PHP variables, arrays do not need to be initialized or created in advance. They are automatically created the first time you use them. The following code creates the same \$products array created previously with the array() statement:

```php
$products[0] = 'Tires';
$products[1] = 'Oil';
$products[2] = 'Spark Plugs';
```

If \$products does not already exist, the first line will create a new array with just one element. The subsequent lines add values to the array. The array is dynamically resized as you add elements to it. This resizing capability is not present in many other programming languages.

1『 php 能动态的自动更新数组大小，好多其他语言没这能力。印象中 JS 好像不行，待确认。（2020-04-25）』

#### 3.2.3 Using Loops to Access the Array

Because the array is indexed by a sequence of numbers, you can use a for loop to more easily display its contents:

```php
for ($i = 0; $i<3; $i++) {  
    echo $products[$i]." ";
}
```

This loop provides similar output to the preceding code but requires less typing than manually writing code to work with each element in a large array. The ability to use a simple loop to access each element is a nice feature of arrays. You can also use the foreach loop, specially designed for use with arrays. In this example, you could use it as follows:

```php
foreach ($products as $current) {  
    echo $current." ";
}
```

1『 foreach 语句遍历是数组独有的。』

This code stores each element in turn in the variable \$current and prints it out.

### 3.3 Arrays with Different Indices

In the \$products array, you allowed PHP to give each item the default index. This meant that the first item you added became item 0; the second, item 1; and so on. PHP also supports arrays in which you can associate any scalar key or index you want with each value.

#### 3.3.1 Initializing an Array

The following code creates an array with product names as keys and prices as values:

```php
$prices = array('Tires'=>100, 'Oil'=>10, 'Spark Plugs'=>4);
```

1『构建「键-值」对数组的方式。』

The symbol between the keys and values (=>) is simply an equal sign immediately followed by a greater than symbol.

#### 3.3.2 Accessing the Array Elements

Again, you access the contents using the variable name and a key, so you can access the information stored in the prices array as \$prices['Tires'], \$prices['Oil'], and \$prices['Spark Plugs']. The following code creates the same \$prices array. Instead of creating an array with three elements, this version creates an array with only one element and then adds two more:

```
$prices = array('Tires'=>100);
$prices['Oil'] = 10;
$prices['Spark Plugs'] = 4;
```

Here is another slightly different but equivalent piece of code. In this version, you do not explicitly create an array at all. The array is created for you when you add the first element to it:

```
$prices['Tires'] = 100;
$prices['Oil'] = 10;
$prices['Spark Plugs'] = 4;
```

1『这个方式构建「键-值」对数组更灵活，方便用在循环体里。』

#### 3.3.3 Using Loops

Because the indices in an array are not numbers, you cannot use a simple counter in a for loop to work with the array. However, you can use the foreach loop or the list() and each() constructs. The foreach loop has a slightly different structure when using non-numerically indexed arrays. You can use it exactly as you did in the previous example, or you can incorporate the keys as well:

```php
foreach ($prices as $key => $value) {  
    echo $key." – ".$value."<br />";
}
```

The following code lists the contents of the \$prices array using the each() construct:

```php
while ($element = each($prices)) {  
    echo $element['key']." – ". $element['value'];  
    echo "<br />";
}
```

The output of this script fragment is shown in Figure 3.2.

Figure 3.2  An each() statement can be used to loop through arrays

In Chapter 1, we looked at while loops and the echo statement. The preceding code uses the each() function, which we have not yet covered. This function returns the current element in an array and makes the next element the current one. Because we are calling each() within a while loop, it returns every element in the array in turn and stops when the end of the array is reached.

In this code, the variable \$element is an array. When you call each(), it gives you an array with four values and the four indices to the array locations. The locations key and 0 contain the key of the current element, and the locations value and 1 contain the value of the current element. Although the one you choose makes no difference, we chose to use the named  locations rather than the numbered ones.

There is a more elegant and common way of doing the same thing. The construct list() can be used to split an array into a number of values. You can separate each set of  values that the each() function gives you like this:

```php
while (list($product, $price) = each($prices)) {  
    echo $product." – ".$price."<br />";
}
```

1『这个方式拆解还是第一次见，而且作者是推荐这种方式的，优雅。』

This line uses each() to take the current element from \$prices, return it as an array, and make the next element current. It also uses list() to turn the 0 and 1 elements from the array returned by each() into two new variables called \$product and \$price.

When you are using each(), note that the array keeps track of the current element. If you want to use the array twice in the same script, you need to set the current element back to the start of the array using the function reset(). To loop through the prices array again, you type the following:

```php
reset($prices);
while (list($product, $price) = each($prices)) {  
    echo $product." – ".$price."<br />";
}
```

This code sets the current element back to the start of the array and allows you to go through again.

### 3.4 Array Operators

One set of special operators applies only to arrays. Most of them have an analogue in the scalar operators, as you can see by looking at Table 3.1.

These operators are mostly fairly self-evident, but union requires some further explanation. The union operator tries to add the elements of \$b to the end of \$a. If elements in \$b have the same keys as some elements already in \$a, they will not be added. That is, no elements of \$a will be overwritten.

You will notice that the array operators in Table 3.1 all have equivalent operators that work on scalar variables. As long as you remember that + performs addition on scalar types and union on arrays—even if you have no interest in the set arithmetic behind that behavior—the  behaviors should make sense. You cannot usefully compare arrays to scalar types.

### 3.5 Multidimensional Arrays

Arrays do not have to be a simple list of keys and values; each location in the array can hold another array. This way, you can create a two-dimensional array. You can think of a two-dimensional array as a matrix, or grid, with width and height or rows and columns.

If you want to store more than one piece of data about each of Bob’s products, you could use a two-dimensional array. Figure 3.3 shows Bob’s products represented as a two-dimensional array with each row representing an individual product and each column representing a stored product attribute.

Figure 3.3  You can store more information about Bob’s products in a two-dimensional array

Using PHP, you would write the following code to set up the data in the array shown in Figure 3.3:

```php
$products = array( array('TIR', 'Tires', 100 ),                   
                                array('OIL', 'Oil', 10 ),                   
                                array('SPK', 'Spark Plugs', 4 ) );
```

You can see from this definition that the \$products array now contains three arrays. To access the data in a one-dimensional array, recall that you need the name of the array and the index of the element. A two-dimensional array is similar, except that each element has two indices: a row and a column. (The top row is row 0, and the far-left column is column 0.) To display the contents of this array, you could manually access each element in order like this:

1『可类比于 pandas 里的 dataframe 对象。』

```php
echo '|'.$products[0][0].'|'.$products[0][1].'|'.$products[0][2].'|<br />';
echo '|'.$products[1][0].'|'.$products[1][1].'|'.$products[1][2].'|<br />';
echo '|'.$products[2][0].'|'.$products[2][1].'|'.$products[2][2].'|<br />';
```

Alternatively, you could place a for loop inside another for loop to achieve the same result:

```
for ($row = 0; $row < 3; $row++) {   
    for ($column = 0; $column < 3; $column++) {      
        echo '|'.$products[$row][$column];   
    }   
    echo '|<br />';
}
```

Both versions of this code produce the same output in the browser:

```
|TIR|Tires|100|
|OIL|Oil|10|
|SPK|Spark Plugs|4|
```

The only difference between the two examples is that your code will be much shorter if you use the second version with a large array. You might prefer to create column names instead of numbers, as shown in Figure 3.3. To store the same set of products, with the columns named as they are in Figure 3.3, you would use the following code:

```php
$products = array(array('Code' => 'TIR',                        
                                        'Description' => 'Tires',                        
                                        'Price' => 100                        
                                        ),                  
                            array('Code' => 'OIL',                        
                                        'Description' => 'Oil',                        
                                        'Price' => 10                        
                                        ),                  
                            array('Code' => 'SPK',                        
                                        'Description' => 'Spark Plugs',                        
                                        'Price' =>4                        
                                        )                 
                            );
```

1『这种构建二维数组的方式是我想要的。』

This array is easier to work with if you want to retrieve a single value. Remembering that the description is stored in the Description column is easier than remembering it is stored in column 1. Using descriptive indices, you do not need to remember that an item is stored at [x][y]. You can easily find your data by referring to a location with meaningful row and column names. You do, however, lose the ability to use a simple for loop to step through each column in turn. Here is one way to write code to display this array:

```php
for ($row = 0; $row < 3; $row++){  
    echo '|'.$products[$row]['Code'].'|'.$products[$row]['Description'].
       '|'.$products[$row]['Price'].'|<br />';
}
```

Using a for loop, you can step through the outer, numerically indexed \$products array. Each row in the \$products array is an array with descriptive indices. Using the each() and list() functions in a while loop, you can step through these inner arrays. Therefore, you can use a while loop inside a for loop:

```php
for ($row = 0; $row < 3; $row++){  
    while (list( $key, $value ) = each( $products[$row])){    
        echo '|'.$value;  
    }  
    echo '|<br />';
}
```

You do not need to stop at two dimensions. In the same way that array elements can hold new arrays, those new arrays, in turn, can hold more arrays. A three-dimensional array has height, width, and depth. If you are comfortable thinking of a two-dimensional array as a table with rows and columns, imagine a pile or deck of those tables. Each element is referenced by its layer, row, and column.

1『作者这个隐喻好，二维数组想象正一张表，三维数组想象成一推叠起来的表。』

If Bob divided his products into categories, you could use a three-dimensional array to store them. Figure 3.4 shows Bob’s products in a three-dimensional array.

From the code that defines this array, you can see that a three-dimensional array is an array containing arrays of arrays:

```php
$categories = array(array(array('CAR_TIR', 'Tires', 100 ),                          
                                        array('CAR_OIL', 'Oil', 10 ),                          
                                        array('CAR_SPK', 'Spark Plugs', 4 )                         
                                        ),                     
                                array(array('VAN_TIR', 'Tires', 120 ),                           
                                        array('VAN_OIL', 'Oil', 12 ),                           
                                        array('VAN_SPK', 'Spark Plugs', 5 )                          
                                        ),                     
                                array(array('TRK_TIR', 'Tires', 150 ),                           
                                array('TRK_OIL', 'Oil', 15 ),                           
                                array('TRK_SPK', 'Spark Plugs', 6 )                          
                                )                   
                            );
```

Because this array has only numeric indices, you can use nested for loops to display its contents:

```php
for ($layer = 0; $layer < 3; $layer++) {  
    echo 'Layer'.$layer."<br />";  
    for ($row = 0; $row < 3; $row++) {    
        for ($column = 0; $column < 3; $column++) {      
            echo '|'.$categories[$layer][$row][$column];    
        }    
        echo '|<br />';  
    }
}
```

Because of the way multidimensional arrays are created, you could create four-, five-, or even six-dimensional arrays. There is no language limit to the number of dimensions, but it is difficult for people to visualize constructs with more than three dimensions. Most real-world problems match logically with constructs of three or fewer dimensions.

1『同感，三维以上人就很像想象了。』

### 3.6 Sorting Arrays

Sorting related data stored in an array is often useful. You can easily take a one-dimensional array and sort it into order. 

#### 3.6.1 Using sort()

The following code showing the sort() function results in the array being sorted into ascending alphabetical order:

```php
$products = array('Tires', 'Oil', 'Spark Plugs');
sort($products);
```

The array elements will now appear in the order Oil, Spark Plugs, Tires. You can sort values by numerical order, too. If you have an array containing the prices of Bob’s products, you can sort it into ascending numeric order as follows:

```php
$prices = array(100, 10, 4);
sort($prices);
```

The prices will now appear in the order 4, 10, 100. Note that the sort() function is case sensitive. All capital letters come before all lowercase letters. So A is less than Z, but Z is less than a.

The function also has an optional second parameter. You may pass one of the constants SORT\_REGULAR (the default), SORT\_NUMERIC, SORT\_STRING, SORT\_LOCALE\_STRING, SORT\_NATURAL, SORT\_FLAG\_CASE. 

The ability to specify the sort type is useful when you are comparing strings that might contain numbers, for example, 2 and 12. Numerically, 2 is less than 12, but as strings '12' is less than '2'. Passing the SORT\_LOCALE\_STRING constant will sort the array as strings depending on the current locale, as sort orders are different in different locales. 

Using SORT\_NATURAL causes a natural sort order to be used. You can also get this by using the natsort() function. Natural sort order is like a combination of string and numeric sorts, to be more intuitive. For example, using a string sort for the strings 'file1', 'file2', and 'file10' would order them as 'file1', 'file10', 'file2'.  Using a natural sort, they would be ordered as 'file1', 'file2', 'file10', which is more intuitive—or more natural—for humans.

The constant SORT\_FLAG\_CASE is used in conjunction with SORT\_STRING or SORT\_NATURAL. Use the bitwise and operator to combine them, as follows:

```php
sort($products, SORT_STRING & SORT_FLAG_CASE);
```

This makes the sort() function ignore case, so 'a' and 'A' are treated as equivalent.

#### 3.6.2 Using asort() and ksort() to Sort Arrays

If you are using an array with descriptive keys to store items and their prices, you need to use different kinds of sort functions to keep keys and values together as they are sorted. The following code creates an array containing the three products and their associated prices and then sorts the array into ascending price order:

```php
$prices = array('Tires'=>100, 'Oil'=>10, 'Spark Plugs'=>4);
asort($prices);
```

The function asort() orders the array according to the value of each element. In the array, the values are the prices, and the keys are the textual descriptions. If, instead of sorting by price, you want to sort by description, you can use ksort(), which sorts by key rather than value. The following code results in the keys of the array being ordered alphabetically—Oil, Spark Plugs, Tires:

```php
$prices = array('Tires'=>100, 'Oil'=>10, 'Spark Plugs'=>4);
ksort($prices);
```

#### 3.6.2 Sorting in Reverse

The three different sorting functions—sort(), asort(), and ksort()—sort an array into ascending order. Each function has a matching reverse sort function to sort an array into descending order. The reverse versions are called rsort(), arsort(), and krsort().

You use the reverse sort functions in the same way you use the ascending sort functions. The rsort() function sorts a single-dimensional numerically indexed array into descending order. The arsort() function sorts a one-dimensional array into descending order using the value of each element. The krsort() function sorts a one-dimensional array into descending order using the key of each element.

### 3.7 Sorting Multidimensional 

ArraysSorting arrays with more than one dimension, or by something other than alphabetical or numerical order, is more complicated. PHP knows how to compare two numbers or two text strings, but in a multidimensional array, each element is an array. There are two approaches to sorting multidimensional arrays: creating a user-defined sort or using the array\_multisort() function. 

#### 3.7.1 Using the array\_multisort() function

The array\_multisort() function can be used either to sort multidimensional arrays, or to sort multiple arrays at once. The following is the definition of a two-dimensional array used earlier. This array stores Bob’s three products with a code, a description, and a price for each:

```php
$products = array(array('TIR', 'Tires', 100),                  
                            array('OIL', 'Oil', 10),                  
                            array('SPK', 'Spark Plugs', 4));
```

If we simply take the function array\_multisort() and apply it as follows, it will sort the array. But in what order?

```php
array_multisort($products);
```

As it turns out, this will sort our \$products array by the first item in each array, using a regular ascending sort, as follows:

```
'OIL', 'Oil', 10
'SPK', 'Spark Plugs', 4
'TIR', 'Tires', 100
```

This function has the following prototype:

```php
bool array_multisort(array &a [, mixed order = SORT_ASC [, mixed sorttype = SORT_REGULAR [, mixed $... ]]] )
```

For the ordering you can pass SORT\_ASC or SORT\_DESC for ascending or descending order, respectively. For the sort type, array\_multisort() supports the same constants as the sort() function.

One important point to note for array\_multisort() is that, while it will maintain key-value associations when the keys are strings, it will not do so if the keys are numeric, as in this example.

#### 3.7.2 User-Defined Sorts

Taking the same array as in the previous example, there are at least two useful sort orders. You might want the products sorted into alphabetical order using the description or by numeric order by the price. Either result is possible, but you can use the function usort() to tell PHP how to compare the items. To do this, you need to write your own comparison function. The following code sorts this array into alphabetical order using the second column in the array—the description:

```php
function compare($x, $y) {  
    if ($x[1] == $y[1]) {    
        return 0;  
    } else if ($x[1] < $y[1]) {    
        return -1;  
    } else {    
        return 1;  
    }
}
usort($products, 'compare');
```

So far in this book, you have called a number of the built-in PHP functions. To sort this array, you need to define a function of your own. We examine writing functions in detail in Chapter 5「Reusing Code and Writing Functions,」but here is a brief introduction.

You define a function by using the keyword function. You need to give the function a name. Names should be meaningful, so you can call it compare() for this example. Many functions take parameters or arguments. This compare() function takes two: one called \$x and one called \$y. The purpose of this function is to take two values and determine their order.

For this example, the \$x and \$y parameters are two of the arrays within the main array, each representing one product. To access the Description of the array \$x, you type \$x[1] because the Description is the second element in these arrays, and numbering starts at zero. You use \$x[1] and \$y[1] to compare each Description from the arrays passed into the function.

When a function ends, it can give a reply to the code that called it. This process is called returning a value. To return a value, you use the keyword return in the function. For example, the line return 1; sends the value 1 back to the code that called the function.

To be used by usort(), the compare() function must compare \$x and \$y. The function must return 0 if \$x equals \$y, a negative number if it is less, or a positive number if it is greater. The function will return 0, 1, or -1, depending on the values of \$x and \$y.

The final line of code calls the built-in function usort() with the array you want sorted (\$products) and the name of the comparison function (compare()).

If you want the array sorted into another order, you can simply write a different comparison function. To sort by price, you need to look at the third column in the array and create this comparison function:

```php
function compare($x, $y) {  
    if ($x[2] == $y[2]) {    
        return 0;  
    } else if ($x[2] < $y[2]) {    
        return -1;  
    } else {    
        return 1;  
    }
}
```

When usort(\$products, 'compare') is called, the array is placed in ascending order by price.

Note: Should you run these snippets to test them, there will be no output. These snippets are meant to be part of large pieces of code you might write.

The u in usort() stands for user because this function requires a user-defined comparison function. The uasort() and uksort() versions of asort and ksort also require user-defined comparison functions. 

Similar to asort(), uasort() should be used when sorting a non-numerically indexed array by value. Use asort if your values are simple numbers or text. Define a comparison function and use uasort() if your values are more complicated objects such as arrays.

Similar to ksort(), uksort() should be used when sorting a non-numerically indexed array by key. Use ksort if your keys are simple numbers or text. Define a comparison function and use uksort() if your keys are more complicated objects such as arrays.

#### 3.7.3 Reverse User Sorts

The functions sort(), asort(), and ksort() all have matching reverse sorts with an r in the function name. The user-defined sorts do not have reverse variants, but you can sort a multidimensional array into reverse order. Because you provide the comparison function, you can write a comparison function that returns the opposite values. To sort into reverse order, the function needs to return 1 if \$x is less than \$y and -1 if \$x is greater than \$y. For example:

```php
function reverse_compare($x, $y) {  
    if ($x[2] == $y[2]) {    
        return 0;  
    } else if ($x[2] < $y[2]) {    
        return 1;  
    } else {    
        return -1;  
    }
}
```

Calling usort(\$products, 'reverse_compare') would now result in the array being placed in descending order by price.

### 3.8 Reordering Arrays

For some applications, you might want to manipulate the order of the array in other ways than a sort. The function shuffle() randomly reorders the elements of your array. The function array\_reverse() gives you a copy of your array with all the elements in reverse order.

#### 3.8.1 Using shuffle()

Bob wants to feature a small number of his products on the front page of his site. He has a large number of products but would like three randomly selected items shown on the front page. So that repeat visitors do not get bored, he would like the three chosen products to be different for each visit. He can easily accomplish his goal if all his products are in an array. Listing 3.1 displays three randomly chosen pictures by shuffling the array into a random order and then displaying the first three.

1『下面的功能实现从数据里随机筛选 3 个呈现给前端。』

Because the code selects random pictures, it produces a different page nearly every time you load it, as shown in Figure 3.5.

#### 3.8.2 Reversing an Array

Sometimes you may want to reverse the order of an array. The simplest way to do this is with the function array\_reverse(), which takes an array and creates a new one with the same contents in reverse order. Using the range() function usually creates an ascending sequence, as follows:

```php
$numbers = range(1,10);
```

You can then use the array\_reverse() function to reverse the array created by range():

```php
$numbers = range(1,10);
$numbers = array_reverse($numbers);
```

Note that array\_reverse() returns a modified copy of the array. If you do not want the original array, as in this example, you can simply store the new copy over the original. Alternatively, you could create the array in descending order in the first place, one element at a time, by writing a for loop:

```php
$numbers = array();
for($i=10; $i>0; $i--) {  
    array_push($numbers, $i);
}
```

A for loop can go in descending order like this: You set the starting value high and at the end of each loop use the -- operator to decrease the counter by one.

Here, we create an empty array and then use array\_push() for each element to add one new element to the end of an array. As a side note, the opposite of array\_push() is array\_pop(). This function removes and returns one element from the end of an array. Note that if the desired array is just a range of descending integers, you can also create it in reverse order by passing –1 as the optional step parameter to range():

```php
$numbers = range(10, 1, -1);
```

### 3.9 Loading Arrays from Files

In Chapter 2,「Storing and Retrieving Data」you learned how to store customer orders in a file. Each line in the file looked something like this:

```
01:34, 14th September 2015 1 tires  2 oil 3 spark plugs $145.2  123 Main Street, Sometown, CA 95128
```

To process or fulfill this order, you could load it back into an array. Listing 3.2 displays the current order file.

Listing 3.2  vieworders.php—Using PHP to Display Orders for Bob

This script produces almost exactly the same output as Listing 2.3 in the preceding chapter, which was shown in Figure 2.4. This time, the script uses the function file(), which loads the entire file into an array. Each line in the file becomes one element of an array. This code also uses the count() function to see how many elements are in an array. Furthermore, you could load each section of the order lines into separate array elements to process the sections separately or to format them more attractively. Listing 3.3 does exactly that.

Listing 3.3 vieworders_v2.php—Using PHP to Separate, Format, and Display Orders for Bob

The code in Listing 3.3 loads the entire file into an array, but unlike the example in Listing 3.2, here we use the function explode() to split up each line so that we can apply some  processing and formatting before printing. The output from this script is shown in Figure 3.6.

Figure 3.6  After splitting order records with explode(), you can put each part of an order in a different table cell for better-looking output

2『上面加载文件成数组后排序的实现代码，好好研究其细节。开发数据流一体化的时候是利用「laravel-excel」包实现加载文件数据成数组的。（2020-04-26）』

The explode function has the following prototype:

```php
array explode(string separator, string string [, int limit])
```

In the preceding chapter, we used the tab character as a delimiter when storing this data, so here we do the following:

```php
$line = explode("\t", $orders[$i]);
```

This code「explodes」the passed-in string into parts. Each tab character becomes a break between two elements. For example, the string:

    16:44, 28th September 2014\t1 tires\t2 oil\t3 spark plugs\t\$145.2\t123 Main Street, Sometown CA 95128 

is exploded into the parts "16:44, 28th September 2014", "1 tires", "2 oil", "3spark plugs", "\$145.2", and "123 Main Street, Sometown CA 95128". Note that the optional limit parameter can be used to limit the maximum number of parts returned.

This example doesn’t do very much processing. Rather than output tires, oil, and spark plugs on every line, this example displays only the number of each and gives the table a heading row to show what the numbers represent.

You could extract numbers from these strings in a number of ways. Here, we used the function intval(). As mentioned in Chapter 1, intval() converts a string to an integer. The conver-sion is reasonably clever and ignores parts, such as the label in this example, which cannot be converted to an integer. We cover various ways of processing strings in the next chapter.

### 3.10 Performing Other Array Manipulations

So far, we have covered only about half the array processing functions. Many others will be useful from time to time; we describe some of them next.

#### 3.10.1 Navigating Within an Array: each(), current(), reset(), end(), next(), pos(), and prev()

We mentioned previously that every array has an internal pointer that points to the current element in the array. You indirectly used this pointer earlier when using the each() function, but you can directly use and manipulate this pointer. 

If you create a new array, the current pointer is initialized to point to the first element in the array. Calling current(\$array_name) returns the first element. Calling either next() or each() advances the pointer forward one element. Calling each(\$array_name) returns the current element before advancing the pointer. The function next() behaves slightly differently: Calling next(\$array_name) advances the pointer and then returns the new current element.

You have already seen that reset() returns the pointer to the first element in the array. Similarly, calling end(\$array_name) sends the pointer to the end of the array. The first and last elements in the array are returned by reset() and end(), respectively.

To move through an array in reverse order, you could use end() and prev(). The prev()  function is the opposite of next(). It moves the current pointer back one and then returns the new current element. For example, the following code displays an array in reverse order:

```php
$value = end($array);
while ($value){  
    echo "$value<br />";  
    $value = prev($array);
}
```

For example, you can declare \$array like this:

```php
$array = array(1, 2, 3);
```

In this case, the output would appear in a browser as follows:

```
3
2
1
```

Using each(), current(), reset(), end(), next(), pos(), and prev(), you can write your own code to navigate through an array in any order.

#### 3.10.2 Applying Any Function to Each Element in an Array: array_walk()

Sometimes you might want to work with or modify every element in an array in the same way. The function array_walk() allows you to do this. The prototype of array\_walk() is as follows:

```php
bool array_walk(array arr, callable func[, mixed userdata])
```

Similar to the way we used usort() earlier, array\_walk() expects you to declare a function of your own. As you can see, array\_walk() takes three parameters. The first, arr, is the array to be processed. The second, func, is the name of a user-defined function that will be applied to each element in the array. The third parameter, userdata, is optional. If you use it, it will be passed through to your function as a parameter. We’ll see how this works shortly.

A handy user-defined function might be one that displays each element with some specified formatting. The following code displays each element on a new line by calling the user-defined function my\_print() with each element of \$array:

```php
function my_print($value){  
    echo "$value<br />";
}
array_walk($array, 'my_print');
```

The function you write needs to have a particular signature. For each element in the array, array\_walk() takes the key and value stored in the array, and anything you passed as  userdata, and calls your function like this:

```php
yourfunction(value, key, userdata)
```

For most uses, your function will be using only the values in the array. For some, you might also need to pass a parameter to your function using the parameter userdata. Occasionally, you might be interested in the key of each element as well as the value. Your function can, as with my_print(), choose to ignore the key and userdata parameter. For a slightly more complicated example, you can write a function that modifies the values in the array and requires a parameter. Although you may not be interested in the key, you need to accept it to accept the optional third parameter:

```php
function my_multiply(&$value, $key, $factor){  
    $value *= $factor;
}
array_walk($array, 'my_multiply', 3);
```

This code defines a function, my\_multiply(), that will multiply each element in the array by a supplied factor. You need to use the optional third parameter to array\_walk() to take a parameter to pass to the function and use it as the multiplication factor. Because you need this parameter, you must define the function, my\_multiply(), to take three parameters: an array element’s value (\$value), an array element’s key (\$key), and the parameter (\$factor). You can choose to ignore the key.

A subtle point to note is the way \$value is passed. The ampersand (&) before the variable name in the definition of my_multiply() means that \$value will be passed by reference. Passing by reference allows the function to alter the contents of the array. We address passing by reference in more detail in Chapter 5. If you are not familiar with the term, for now just note that to pass by reference, you place an ampersand before the variable name in the function declaration.

#### 3.10.3 Counting Elements in an Array: count(), sizeof(), and array_count_values()

You used the function count() in an earlier example to count the number of elements in an array of orders. The function sizeof() is an alias to count(). This function returns the number of elements in an array passed to it. You get a count of one for the number of elements in a normal scalar variable and zero if you pass either an empty array or a variable that has not been set.

The array_count_values() function is more complex. If you call array_count_values(\$array), this function counts how many times each unique value occurs in the array named \$array. The function returns an associative array containing a frequency table. This array contains all the unique values from \$array as keys. Each key has a numeric value that tells you how many times the corresponding key occurs in \$array.

For example, the code:

```php
$array = array(4, 5, 1, 2, 3, 1, 2, 1);
$ac = array_count_values($array);
```

creates an array called \$ac that contains:

This result indicates that 4, 5, and 3 occurred once in \$array, 1 occurred three times, and 2 occurred twice.

#### 3.10.4 Converting Arrays to Scalar Variables: extract()

If you have a non-numerically indexed array with a number of key value pairs, you can turn them into a set of scalar variables using the function extract(). The prototype for extract() is as follows:

```php
extract(array var_array [, int extract_type] [, string prefix] );
```

The purpose of extract() is to take an array and create scalar variables with the names of the keys in the array. The values of these variables are set to the values in the array. Here is a simple example:

```php
$array = array('key1' => 'value1', 'key2' => 'value2', 'key3' => 'value3');
extract($array);
echo "$key1 $key2 $key3";
```

This code produces the following output:

    value1 value2 value3

The array has three elements with keys: key1, key2, and key3. Using extract(), you create three scalar variables: \$key1, \$key2, and \$key3. You can see from the output that the values of \$key1, \$key2, and \$key3 are 'value1', 'value2', and 'value3', respectively. These values come from the original array.

The extract() function has two optional parameters: extract_type and prefix. The  variable extract_type tells extract() how to handle collisions. These are cases in which a variable already exists with the same name as a key. The default response is to overwrite the existing variable. The allowable values for extract_type are shown in Table 3.2.

Table 3.2  Allowed extract_type Parameters for extract()

The two most useful options are EXTR\_OVERWRITE (the default) and EXTR\_PREFIX\_ALL. The other options might be useful occasionally when you know that a particular collision will occur and want that key skipped or prefixed. A simple example using EXTR\_PREFIX\_ALL follows. You can see that the variables created are called prefix_keyname:

```php
$array = array('key1' => 'value1', 'key2' => 'value2', 'key3' => 'value3');
extract($array, EXTR_PREFIX_ALL, 'my_prefix');
echo "$my_prefix_key1 $my_prefix_key2 $my_prefix_key3";
```

This code again produces the following output:

    value1 value2 value3

Note that for extract() to extract an element, that element’s key must be a valid variable name, which means that keys starting with numbers or including spaces are skipped.

1『 extract() 函数的功能如同其名称一般，可以将数组里的元素提取成一个个单独的变量，留意其应用场景。（2020-04-26）』

### 3.11 Further Reading

This chapter covers what we believe to be the most useful of PHP’s array functions. We have chosen not to cover all the possible array functions, as there are a huge variety of them. The online PHP manual available at http://www.php.net/array provides a brief description for each.

## 04. String Manipulation and Regular Expressions

In this chapter, we discuss how you can use PHP’s string functions to format and manipulate text. We also discuss using string functions or regular expression functions to search (and replace) words, phrases, or other patterns within a string. These functions are useful in many contexts. You often may want to clean up or reformat user input that is going to be stored in a database. Search functions are great when building search engine applications (among other things).

Key topics covered in this chapter include: 1) Formatting strings. 2) Joining and splitting strings. 3) Comparing strings. 4) Matching and replacing substrings with string functions. 5) Using regular expressions.

In the next chapter, we discuss several ways you can use PHP to save programming time and effort and prevent redundancy by reusing pre-existing code.

### 4.1 Creating a Sample Application: Smart Form Mail

In this chapter, you will use string and regular expression functions in the context of a Smart Form Mail application. You’ll then add these scripts to the Bob’s Auto Parts site you’ve been building in preceding chapters.

This time, you’ll build a straightforward and commonly used customer feedback form for Bob’s customers to enter their complaints and compliments, as shown in Figure 4.1. However, this application has one improvement over many you will find on the Web. Instead of  emailing the form to a generic email address like feedback@example.com, you’ll attempt to put some  intelligence into the process by searching the input for key words and phrases and then sending the email to the appropriate employee at Bob’s company. For example, if the email contains the word advertising, you might send the feedback to the Marketing department. If the email is from Bob’s biggest client, it can go straight to Bob.

Figure 4.1  Bob’s feedback form asks customers for their name, email address, and comments.

Start with the bare bones script shown in Listing 4.1 and add to it as you read along. Note that this script, while working, should not be deployed as-is, for reasons we’ll discuss in the next section. We’ll look at a refined version later in the chapter, which will be suitable for actual use.

Listing 4.1  processfeedback.php—Basic Script to Email Form Contents

```php
<?php

//create short variable names
$name=$_POST['name'];
$email=$_POST['email'];
$feedback=$_POST['feedback'];

//set up some static information
$toaddress = "feedback@example.com";
$subject = "Feedback from web site";
$mailcontent = "Customer name: ".filter_var($name)."\n".               
                        "Customer email: ".$email."\n".               
                        "Customer comments:\n".$feedback."\n";
$fromaddress = "From: webserver@example.com";

//invoke mail() function to send mail
mail($toaddress, $subject, $mailcontent, $fromaddress);

?>

<!DOCTYPE html>
<html>  
    <head>    
        <title>Bob's Auto Parts - Feedback Submitted</title>  
    </head>  

    <body>
        <h1>Feedback submitted</h1>    
        <p>Your feedback has been sent.</p>
    </body>
</html>
```

Generally, you should check that users have filled out all the required form fields using, for example, isset(). We have omitted this function call from the script and other examples for the sake of brevity.

In this script, you can see that we have concatenated the form fields together and used PHP’s mail() function to email them to feedback@example.com. This is a sample email address. If you want to test the code in this chapter, substitute your own email address here. Because we haven’t yet used mail(), we need to discuss how it works.

Unsurprisingly, this function sends email. The prototype for mail() looks like this:

```php
bool mail(string to, string subject, string message,          
                string [additional_headers [, string additional_parameters]]);
```

The first three parameters are compulsory and represent the address to send email to, the subject line, and the message contents, respectively. The fourth parameter can be used to send any additional valid email headers. Valid email headers are described in the document RFC822, which is available online if you want more details. (RFCs, or Requests for Comment, are the source of many Internet standards; we discuss them in Chapter 18「Using Network and Protocol Functions.」) 

2『终于知道 RFC822 的基本意思了，之前很多地方看到过，做一张术语卡片。Requests for Comment, are the source of many Internet standards. 』

Here, the fourth parameter adds a From: address for the mail. You can also use it to add Reply-To: and Cc: fields, among others. If you want more than one additional header, just separate them by using newlines and carriage returns (\\n) within the string, as follows:

```php
$additional_headers="From: webserver@example.com\r\n "                     
                                    ."Reply-To: bob@example.com";
```

The optional fifth parameter can be used to pass a parameter to whatever program you have configured to send mail. To use the mail() function, set up your PHP installation to point at your mail-sending program. If the script doesn’t work for you in its current form, an installation issue might be at fault, check Appendix A,「Installing Apache, PHP, and MySQL.」

Throughout this chapter, you enhance this basic script by making use of PHP’s string handling and regular expression functions.

### 4.2 Formatting Strings

You often need to clean up user strings (typically from an HTML form interface) before you can use them. The following sections describe some of the functions you can use.

#### 4.2.1 Trimming Strings: chop(), ltrim(), and trim()

The first step in tidying up is to trim any excess whitespace from the string. Although this step is never compulsory, it can be useful if you are going to store the string in a file or database, or if you’re going to compare it to other strings. PHP provides three useful functions for this purpose. In the beginning of the script when you give short names to the form input variables, you can use the trim() function to tidy up your input data as follows:

```php
$name = trim($_POST['name']);
$email = trim($_POST['email']);
$feedback = trim($_POST['feedback']);
```

The trim() function strips whitespace from the start and end of a string and returns the resulting string. The characters it strips by default are newlines and carriage returns (\n and \r), horizontal and vertical tabs (\t and \x0B), end-of-string characters (\0), and spaces. You can also pass it a second parameter containing a list of characters to strip instead of this default list. Depending on your particular purpose, you might like to use the ltrim() or rtrim()  functions instead. They are both similar to trim(), taking the string in question as a parameter and returning the formatted string. The difference between these three is that trim() removes whitespace from the start and end of a string, ltrim() removes whitespace from the start (or left) only, and rtrim() removes whitespace from the end (or right) only.

You may also use the alias chop() for rtrim(). Perl has a similar function but they behave slightly differently, so be cautious in your assumptions if you are coming to PHP from a Perl background.

#### 4.2.2 Formatting Strings for Output

PHP includes a set of functions that you can use to reformat a string in different ways for different purposes.

#### 4.2.2.1 Filtering Strings for Output

Whenever we take user-submitted data and output it somewhere, we need to plan it with the destination in mind. This is because most places we send output to consider some characters and strings as special or control characters and strings, and we don’t want the output destination to interpret user-submitted data as commands.

For example, if echoing user input to a browser, we don’t want to execute any HTML or JavaScript that the user may have included. This is not only because it might break the formatting, but also because it is a security vulnerability to allow the execution of arbitrary user-submitted code or commands. We’ll discuss this in a lot more detail in Part III of this book,「Web Application Security.」In that section, we’ll also cover the filter extension, which enables generic filtering per-destination.

#### 4.2.2.2 Filtering Strings for Output to the Browser with htmlspecialchars()

We used this function in previous chapters, but let’s recap here. The htmlspecialchars() function converts characters that have a special meaning in HTML to their HTML entity equivalent. For example, the character \< is converted to the entity \&lt;. The prototype of this function is as follows:

```php
string htmlspecialchars (string string [, int flags = ENT_COMPAT | ENT_HTML401 [, string encoding = 'UTF-8' [, bool double_encode = true ]]])
```

In general, this function converts characters to their HTML entity equivalents as shown in Table 4.1.

Table 4.1  HTML Entities Encoded by the htmlspecialchars() Function

The default encoding of quotes is to only encode double quotes. Single quotes will remain untranslated. This behavior is controlled by the flags parameter. The first parameter is the string to be translated, and the function returns the translated string.

Note: If the input string is not valid in the specified encoding, the function will return the empty string without raising an error. This is intended to help avoid code injection issues.

The first optional parameter, flags, specifies how the translation should be done. You pass in a bitmask representing the possible values combined together. The default value, as you can see in the prototype above, is ENT\_COMPAT | ENT\_HTML401. The ENT\_COMPAT constant indicates that double quotes should be encoded, and single quotes left as-is, while the ENT\_HTML401 constant indicates that code should be treated as HTML 4.01.

The second optional parameter, encoding, specifies the encoding used for conversion. From PHP 5.4 on, the default is UTF-8. Prior to that, it was ISO-8859-1, commonly known as Latin-1. The list of supported encodings may be found in the PHP documentation.

The third optional parameter, double\_encode, specifies whether to encode HTML entities. The default is to convert them (again).

The full set of possible values that may be combined in the flags parameter can be found in Table 4.2.

Table 4.2  Flags for the htmlspecialchars() Function

#### 4.2.2.3 Filtering Strings for Other Forms of Output

Depending on where you are outputting strings, the characters that may cause problems are different. We previously discussed the htmlspecialchars() function for output to the browser. In the example in Listing 4.1, we are sending output to email. What do we need to take into account here? We don’t care if the email contains HTML, so using the htmlspecialchars() function is not appropriate here.

The main issue in email is that headers are separated by the character string \r\n (carriage return-line feed). We need to take care that user data we use in the email headers does not contain these characters, or we run the risk of a set of attacks, called header injection. (We discuss this in more detail in Part III.) As with many string processing problems, there are multiple ways to approach this. One way is to use the str\_replace() function, as follows:

```php
$mailcontent = "Customer name: ".str_replace("\r\n", "", $name)."\n".               
                        "Customer email: ".str_replace("\r\n", "",$email)."\n".               
                        "Customer comments:\n".str_replace("\r\n", "",$feedback)."\n";
```

If you have more complicated matching or replacement rules, you can use the regular expression functions described later in this chapter. In a simple case like this where you want to entirely replace one string with another, you should always use the str\_replace() function. We’ll discuss the str\_replace() function in more detail later in this chapter.

#### 4.2.2.4 Using HTML Formatting: The nl2br() 

FunctionThe nl2br() function takes a string as a parameter and replaces all the newlines in it with the HTML \<br/> tag. This capability is useful for echoing a long string to the browser. For example, you can use this function to format the customer’s feedback to echo it back:

```html
<p>Your feedback (shown below) has been sent.</p>
<p><?php echo nl2br(htmlspecialchars($feedback)); ?> </p>
```

Remember that HTML disregards plain whitespace, so if you don’t filter this output through nl2br(), it will appear on a single line (except for newlines forced by the browser window). The result is illustrated in Figure 4.2.

Notice that we first applied the htmlspecialchars() function and then the nl2br()  function. This is because if we did them in the opposite order, the \<br/> tags inserted by the nl2br() function would be translated into HTML entities by the htmlspecialchars()  function and hence would have no effect.

Figure 4.2  Using PHP’s nl2br() function improves the display of long strings within HTML.

At this stage, we have an order processing script that formats user data for output to both email and HTML. The revised order processing script is found in Listing 4.2.

Listing 4.2  processfeedback_v2.php—Revised Script to Email Form Contents

```php
<?php

//create short variable names
$name = trim($_POST['name']);
$email = trim($_POST['email']);
$feedback = trim($_POST['feedback']);

//set up some static information
$toaddress = "feedback@example.com";
$subject = "Feedback from web site";
$mailcontent = "Customer name: ".str_replace("\r\n", "", $name)."\n".               
                        "Customer email: ".str_replace("\r\n", "",$email)."\n".               
                        "Customer comments:\n".str_replace("\r\n", "",$feedback)."\n";
$fromaddress = "From: webserver@example.com";

//invoke mail() function to send mail
mail($toaddress, $subject, $mailcontent, $fromaddress);

?>

<!DOCTYPE html>
<html>  
    <head>    
        <title>Bob's Auto Parts - Feedback Submitted</title>  
    </head>  
    
    <body>
        <h1>Feedback submitted</h1>    
        <p>Your feedback (shown below) has been sent.</p>    
        <p><?php echo nl2br(htmlspecialchars($feedback)); ?> </p>  
    </body>
</html>
```

There are many other string processing functions you may find useful. We’ll examine these in the remainder of this section.

#### 4.2.2.5 Formatting a String for Printing

So far, you have used the echo language construct to print strings to the browser. PHP also supports a print() construct, which does the same thing as echo, but returns a value, which is always equal to 1. Both of these techniques print a string「as is.」You can apply some more sophisticated formatting using the functions printf() and sprintf(). They work basically the same way, except that printf() outputs a formatted string and sprintf() returns a formatted string.

If you have previously programmed in C, you will find that these functions are conceptually similar to the C versions. Be careful, though, because the syntax is not exactly the same. If you haven’t, they take getting used to but are useful and powerful.

The prototypes for these functions are

```
string sprintf (string format [, mixed args...])int printf (string format [, mixed args...])
```

The first parameter passed to both of these functions is a format string that describes the basic shape of the output with format codes instead of variables. The other parameters are variables that will be substituted in to the format string. For example, using echo, you can use the variables you want to print inline, like this:

```php
echo "Total amount of order is $total.";
```

To get the same effect with printf(), you would use

```php
printf ("Total amount of order is %s.", $total);
```

The %s in the format string is called a conversion specification. This one means「replace with a string.」In this case, it is replaced with \$total interpreted as a string. If the value stored in \$total was 12.4, both of these approaches would print it as 12.4. The advantage of printf() is that you can use a more useful conversion specification to specify that \$total is actually a floating-point number and that it should have two decimal places after the decimal point, as follows:

```php
printf ("Total amount of order is %.2f", $total);
```

Given this formatting, and 12.4 stored in \$total, this statement will print as 12.40. You can have multiple conversion specifications in the format string. If you have n conversion specifications, you will usually have n arguments after the format string. Each conversion speci-fication will be replaced by a reformatted argument in the order they are listed. For example,

```php
printf ("Total amount of order is %.2f (with shipping %.2f) ",           
            $total, $total_shipping);
```

Here, the first conversion specification uses the variable \$total, and the second uses the  variable \$total\_shipping. Each conversion specification follows the same format, which is

    %[+]['padding_character][-][width][.precision]type

All conversion specifications start with a % symbol. If you actually want to print a % symbol, you need to use %%.The + sign is optional. By default, only numbers that are negative show a sign (in this case -). If you specify a sign here then positive values will be prefixed with the + sign and negative values will be prefixed with the - sign.

The padding\_character is optional. It is used to pad your variable to the width you have specified. An example would be to add leading zeros to a number like a counter. The default padding character is a space. If you are specifying a space or zero, you do not need to prefix it with the apostrophe ('). For any other padding character, you need to prefix it with an apostrophe.

The - symbol is optional. It specifies that the data in the field will be left-justified rather than right-justified, which is the default. The width specifier tells printf() how much room (in characters) to leave for the variable to be substituted in here. The precision specifier should begin with a decimal point. It should contain the number of places after the decimal point you would like displayed. The final part of the specification is a type code. A summary of these codes is shown in Table 4.3.

Table 4.3  Conversion Specification Type Codes

When using the printf() function with conversion type codes, you can use argument numbering. That means that the arguments don’t need to be in the same order as the  conversion specifications. For example,

```php
printf ("Total amount of order is %2\$.2f (with shipping %1\$.2f) ",           
            $total_shipping, $total);
```

Just add the argument position in the list directly after the % sign, followed by an escaped \$ symbol; in this example, 2\$ means「replace with the second argument in the list.」This method can also be used to repeat arguments. Two alternative versions of these functions are called vprintf() and vsprintf(). These  variants accept two parameters: the format string and an array of the arguments rather than a variable number of parameters.

#### 4.2.2.6 Changing the Case of a String

You can also reformat the case of a string. This capability is not particularly useful for the sample application, but we’ll look at some brief examples.

If you start with the subject string, \$subject, which you are using for email, you can change its case by using several functions. The effect of these functions is summarized in Table 4.4. The first column shows the function name, the second describes its effect, the third shows how it would be applied to the string \$subject, and the last column shows what value would be returned from the function.

Table 4.4  String Case Functions and Their Effects








