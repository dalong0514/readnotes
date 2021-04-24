yield the given detail information if available.

You have now reached the end of Volume I of Core Java. This volume covered the fundamentals of the Java programming language and the parts of the standard library that you need for most programming projects. We hope that you enjoyed your tour through the Java fundamentals and that you found useful information along the way. For advanced topics, such as the Java platform module system, networking, advanced user interface and graphics programming, security, and internationalization, please turn to Volume II.

Appendix A

This appendix lists all keywords of the Java language. Some keywords are「restricted.」They have a special meaning only in certain circumstances (for example, in module declarations). Elsewhere, they can be identifiers.

Table A.1 Java Keywords

Keyword

Meaning

See Chapter

abstract

An abstract class or method

5

assert

Used to locate internal program error

7

boolean

The Boolean type

3

break

Breaks out of a switch or loop

3

byte

The 8-bit integer type

3

case

A case of a switch

3

catch

The clause of a try block catching an exception

7

char

The Unicode character type

3

class

Defines a class type

4

const

Not used

continue

Continues at the end of a loop

3

default

The default clause of a switch, or a default method in an interface

3, 6

do

The top of a do/while loop

3

double

The double-precision floating-number type

3

else

The else clause of an if statement

3

enum

An enumerated type

3

exports

Exports a package of a module (restricted)

9 (Vol. II)

extends

Defines the parent class of a class, or an upper bound of a wildcard

4

final

A constant, or a class or method that cannot be overridden

5

finally

The part of a try block that is always executed

7

float

The single-precision floating-point type

3

for

A loop type

3

goto

Not used

if

A conditional statement

3

implements

Defines the interface(s) that a class implements

6

import

Imports a package

4

instanceof

Tests if an object is an instance of a class

5

int

The 32-bit integer type

3

interface

An abstract type with methods that a class can implement

6

long

The 64-bit long integer type

3

native

A method implemented by the host system

12 (Vol. II)

new

Allocates a new object or array

3

null

A null reference (note that null is technically a literal, not a keyword)

3

module

Declares a module (restricted)

9 (Vol. II)

open

Modifies a module declaration (restricted)

9 (Vol. II)

opens

Opens a package of a module (restricted)

9 (Vol. II)

package

A package of classes

4

private

A feature that is accessible only by methods of this class

4

protected

A feature that is accessible only by methods of this class, its children, and other classes in the same package

5

provides

Indicates that a module uses a service (restricted)

9 (Vol. II)

public

A feature that is accessible by methods of all classes

4

return

Returns from a method

3

short

The 16-bit integer type

3

static

A feature that is unique to a class or interface, not to instances of a class

3, 6

strictfp

Use strict rules for floating-point computations

2

super

The superclass object or constructor, or a lower bound in a wildcard

5

switch

A selection statement

3

synchronized

A method or code block that is atomic to a thread

12

this

The implicit argument of a method, or a constructor of this class

4

throw

Throws an exception

7

to

A part of an exports or opens declaration (restricted)

9 (Vol. II)

throws

The exceptions that a method can throw

7

transient

Marks data that should not be persistent

2 (Vol. II)

transitive

Modifies a requires declaration (restricted)

9 (Vol. II)

try

A block of code that traps exceptions

7

uses

Indicates that a module uses a service (restricted)

9 (Vol. II)

var

Declares a variable whose type is inferred (restricted)

3

void

Denotes a method that returns no value

3

volatile

Ensures that a field is coherently accessed by multiple threads

12

with

Defines the service class in a provides statement (restricted)

9 (Vol. II)

while

A loop

3

Index

Symbols

- (minus sign)

arithmetic operator, 52, 61

printf flag, 80

-- operator, 58, 61

-> (in lambda expressions), 323–326

_ (underscore)

as a variable name, 49

delimiter, in number literals, 43

in instance field names (C++), 174

, (comma)

operator (C++), 62

printf flag, 80

; (semicolon)

for statements, 41, 48

in class path (Windows), 189

: (colon)

in assertions, 399

in class path (UNIX), 189

inheritance token (C++), 208

:: operator (C++), 151, 159, 211, 328

! operator, 59, 61

!= operator, 59, 61, 97

?: operator, 59, 61

/ (slash), arithmetic operator, 52, 61

// comments, 42

/* . . . */ comments, 42

/** . . . */ comments, 42, 198–199

. (period), in class paths, 189–190

... (ellipsis), in varargs, 260

^ operator, 60–61, 324

~ operator, 60–61

', " (single, double quote), escape sequences for, 46

". . ." (double quotes), for strings, 41

( (left parenthesis), printf flag, 80

() (empty parentheses), in method calls, 41

(. . .) (parentheses)

for casts, 57, 61, 223

for operator hierarchy, 61–62

[] (empty square brackets), in generics, 437

[. . .] (square brackets), for arrays, 108, 112

{. . .} (curly braces)

for blocks, 40–41, 86

for enumerated type, 52

in lambda expressions, 324

{{. . .}} (double curly braces), in inner classes, 354

@ (at), in javadoc comments, 199–200

$ (dollar sign)

delimiter, for inner classes, 346

in variable names, 49

printf flag, 80, 82

* (asterisk)

arithmetic operator, 52, 61

echo character, 647

in class path, 189

in imports, 182

\ (backslash)

escape sequence for, 46

in file names, 83

& (ampersand)

bitwise operator, 60–61

in bounding types, 439

in reference parameters (C++), 168

&& operator, 59, 61

# (number sign)

in javadoc hyperlinks, 202

printf flag, 80

% (percent sign)

arithmetic operator, 52, 61

formatting output for, 79

printf flag, 82

+ (plus sign)

arithmetic operator, 52, 56, 61

for objects and strings, 63, 242

printf flag, 80

++ operator, 58, 61

< (left angle bracket)

in shell syntax, 85

printf flag, 80, 83

relational operator, 59, 61

<? (in wildcard types), 459

<<, >>, >>> operators, 60–61

<= operator, 59, 61

<. . .> (angle brackets), for type parameters, 248, 435

> (right angle bracket)

in shell syntax, 85, 427

relational operator, 59, 61

>& (in shell syntax), 427

>= operator, 59, 61

= operator, 50, 58

== operator, 59, 61

for class objects, 266

for enumerated types, 261

for floating-point numbers, 97

for identity hash maps, 530

for strings, 65

for wrappers, 257

| operator, 60–61

|| operator, 59, 61

0, 0b, 0x prefixes (in integers), 43

0, printf flag, 80

2> (in shell syntax), 427

2D shapes, 579–587

(beer mug), 67

(octonions), 48, 67

A

Abstract classes, 225–231

extending, 227

interfaces and, 305–306

object variables of, 227

abstract keyword, 225–231

ABstract methods, 226

in functional interfaces, 326

AbstractAction class, 609, 613, 673, 676

AbstractButton class, 622–623, 674–677

is/setSelected methods, 677

setAction method, 674

setActionCommand method, 658

setDisplayedMnemonicIndex method, 680–681

setHorizontalTextPosition method, 675

setMnemonic method, 681

abstractClasses/Employee.java, 230

abstractClasses/Person.java, 229

abstractClasses/PersonTest.java, 229

abstractClasses/Student.java, 230

AbstractCollection class, 307, 489, 502

AbstractQueue class, 485

Accelerators (in menus), 680–681

accept method

of FileFilter (Swing), 726, 731

of java.io.FileFilter, 726

acceptEither method (CompletableFuture), 819–820

Access modifiers

checking, 271

final, 51, 155, 221–223, 303, 350–351, 772

private, 146, 187–188, 344

protected, 231–232, 290–291, 319

public, 38–39, 52, 143–146, 187–188, 297–298

public static final, 304

static, 40, 156–163

static final, 51

void, 40

Access order, 528

AccessibleObject class

isAccessible, trySetAccessible methods, 282

setAccessible method, 278, 282

Accessor methods, 138–141, 152–153, 461

Accessory components, 728

accumulate method (LongAccumulator), 774

accumulateAndGet method (AtomicType), 773

Action interface, 608–614, 673

actionPerformed method, 608

add/removePropertyChangeListener methods, 608–609

get/putValue methods, 608, 613

is/setEnabled methods, 608, 613

predefined action table names, 609

Action listeners, 608–614

ActionEvent class, 598, 622

getActionCommand, getModifiers methods, 622

ActionListener interface

actionPerformed method, 310–311, 322, 342, 348, 352, 599, 608–609, 622, 780

overriding, 673

implementing, 327, 599

ActionMap class, 612

Actions, 608–614

associating with keystrokes, 611

names of, 613

predefined, 609

ActiveX, 5, 15

Adapter classes, 605–607

add method

of ArrayList, 249–254

of BigDecimal, BigInteger, 107

of BlockingQueue, 782–783

of ButtonGroup, 658

of Collection, 485, 489–492

of Container, 601, 604, 639

of GregorianCalendar, 138

of HashSet, 509

of JFrame, 579

of JMenu, 672–674

of JToolBar, 689–690

of List, 492, 505

of ListIterator, 493, 499–501, 506

of LongAdder, 774

of Queue, 516

of Set, 494

addAll method

of ArrayList, 434

of Collection, 489, 491

of Collections, 548

of List, 505

addChoosableFileFilter method (JFileChooser), 730

addExact method (Math), 55

addFirst method

of Deque, 517

of LinkedList, 506

addHandler method (Logger), 422

addItem method (JComboBox), 662–664

Addition operator, 52, 61

for different numeric types, 56

for objects and strings, 63, 242

addLast method

of Deque, 517

of LinkedList, 506

addLayoutComponent method (LayoutManager), 706

addPropertyChangeListener method (Action), 608–609

addSeparator method of JMenu, 672, 674

of JToolBar, 689–690

addShutdownHook method (Runtime), 180

addSuppressed method (Throwable), 390, 393

AdjustmentEvent class, 622

AdjustmentListener interface, 622

Adobe Flash, 10

Aggregation, 129–131

Algorithms, 126

for binary search, 546–547

for shuffling, 544

for sorting, 543–546

QuickSort, 113, 544

simple, in the standard library, 547–549

writing, 551–552

Algorithms + Data Structures = Programs (Wirth), 126

Algorithms in C++ (Sedgewick), 544

Alice in Wonderland (Carroll), 510, 512

allOf method

of CompletableFuture, 819–820

of EnumSet, 531

allProcesses method (ProcessHandle), 835, 838

Alt+F4, in Windows, 681

and, andNot methods (BitSet), 560

Andreessen, Mark, 11

Android, 824

Annotations, 446

Anonymous arrays, 108

Anonymous inner classes, 352–355

anonymousInnerClass/AnonymousInnerClassTest.java, 354

Antisymmetry rule, 303

anyOf method (CompletableFuture), 819–820

append method

of JTextArea, 650

of StringBuilder, 74–75

appendCodePoint method (StringBuilder), 75

Applets, 9–10, 15

changing warning string in, 188

running in a browser, 9

Application Programming Interfaces (APIs), online documentation for, 68, 71–73

Applications

closing by user, 570

compiling/launching from the command line, 24–26, 39

debugging, 25–26, 372–380

extensible, 221

for different Java releases, 195–197

localization of, 132, 270, 409–410

managing in JVM, 429

responsive, 823

terminating, 40

testing, 399–403

applyToEither method (CompletableFuture), 819–820

arguments method (ProcessHandle.Info), 838

Arguments. See Parameters

Arithmetic operators, 52–53

accuracy of, 53

autoboxing with, 257

combining with assignment, 58

precedence of, 61

Array class, 283–286

get, getXxx, set, setXxx methods, 286

getLength method, 284, 286

newInstance method, 283, 286

Array lists, 108, 507

anonymous, 354

capacity of, 250

elements of:

accessing, 251–254

adding, 249–253

removing, 253

traversing, 253

generic, 248–256

raw vs. typed, 255–256

Array variables, 108

ArrayBlockingQueue class, 782, 787

ArrayDeque class, 484, 516, 518

as a concrete collection type, 495

ArrayIndexOutOfBoundsException, 110, 375–377

ArrayList class, 110, 248–256, 432–434, 496

add method, 249–254

addAll method, 434

as a concrete collection type, 495

ensureCapacity method, 249, 251

get, set methods, 251, 254

iterating over, 486

remove method, 253–254

removeIf method, 328

size, trimToSize methods, 250–251

synchronized, 799

toArray method, 452

arrayList/ArrayListTest.java, 253

Arrays, 108–123

anonymous, 108

circular, 484–485

cloning, 320

converting to collections, 550–551

copying, 111–112

on write, 797

creating, 108

elements of:

computing in parallel, 798

numbering, 109

remembering types of, 218

removing from the middle, 496–497

traversing, 108, 110, 118

equality testing for, 238

generic methods for, 283–286

hash codes of, 241

in command-line parameters, 112–113

initializing, 108–109

multidimensional, 116–121, 243

not of generic types, 332, 448, 458

of integers, 243

of subclass/superclass references, 218

of wildcard types, 448

out-of-bounds access in, 374

parallel operations on, 797

printing, 118, 243

ragged, 120–123

size of, 110, 250, 284

equal to 0, 109, 551

increasing, 111

setting at runtime, 248

sorting, 113–116, 300, 797

type erasure and, 451–452

Arrays class

asList method, 533, 540, 550

binarySearch method, 116, 365

copyOf method, 111, 116, 283

copyOfRange method, 116

deepToString method, 118, 243

equals method, 116, 238

fill method, 116

hashCode method, 241

parallelXxx methods, 797–798

sort method, 113–116, 297, 300, 302, 322, 326

toString method, 111, 116

arrays/CopyOfTest.java, 285

ArrayStoreException, 218, 448–449, 458

Ascender, ascent (in typesetting), 591

ASCII standard, 47

asIterator method (Enumeration), 554

asList method (Arrays), 533, 540, 550

assert keyword, 399–403

Assertions, 399–403

checking parameters with, 401–402

defined, 399

documenting assumptions with, 402–403

enabling/disabling, 399–401

Assignment operator, 50, 58

Asynchronous computations, 814–831

Asynchronous methods, 800

AsyncTask class, 824

atan, atan2 methods (Math), 54

Atomic operations, 773–775

client-side locking for, 769

in concurrent hash maps, 790–794

performance of, 774

AtomicType classes, 773

@author comment (javadoc), 201, 203

Autoboxing, 256–260

AutoCloseable interface, 389

close method, 389–390

await method (Condition), 741, 760–764

AWT (Abstract Window Toolkit), 565

event hierarchy in, 620–624

preferred field sizes in, 643

AWTEvent class, 620

B

\b (backspace escape sequence), 46

Background color

default, 570

setting, 588–589, 602

BadCastException, 468

Base classes. See Superclasses

Baseline (in typesetting), 591

Basic multilingual planes, 47

BasicButtonUI class, 636

Batch files, 191

Beans, 192

beep method (Toolkit), 313

BiConsumer interface, 337

BiFunction interface, 327, 337

BIG-5 standard, 47

BigDecimal, BigInteger classes, 105–107

add, compareTo, subtract, multiply, divide, mod, sqrt methods, 107

valueOf method, 105–107

BigIntegerTest/BigIntegerTest.java, 106

Binary search, 546–547

BinaryOperator interface, 337

binarySearch method

of Arrays, 116, 365

of Collections, 546–547

BiPredicate interface, 337

Bit masks, 60

Bit sets, 559–563

Bitecode files, 39

BitSet interface, 482, 559–563

methods of, 560

Bitwise operators, 60–61

blank method (String), 69

Blank lines, printing, 41

Blocking queues, 781–788

BlockingDeque interface, methods of, 788

BlockingQueue interface

add, element, peek, remove methods, 782–783

offer, poll, put, take methods, 782–783, 788

blockingQueue/BlockingQueueTest.java, 784

Blocks, 40–41, 86–87

nested, 86

Boolean class

converting from boolean, 256

hashCode method, 241

boolean operators, 59, 61

boolean type, 48

default initialization of, 171

formatting output for, 79

no casting to numeric types for, 57

BooleanHolder class, 259

Border layout manager, 639–641

BorderFactory class, createTypeBorder methods, 658–660

BorderLayout class, 639–641

Borders, 658–661

compound, 659

styling, 658–659

with a title, 659

Bounded collections, 485

Bounding rectangle, 582–583

Bounds checking, 112

Box layout, 691

break statement, 100–104

labeled/unlabeled, 102

Bridge methods, 444–445, 456

Buckets (of hash tables), 508

Bulk operations, 549–550

button/ButtonFrame.java, 603

ButtonGroup class, 654

add method, 658

getSelection method, 656, 658

ButtonModel interface, 634

getActionCommand method, 656, 658

getSelectedObjects method, 656

properties of, 636

Buttons

appearance of, 632

associating actions with, 610

clicking, 602

creating, 601

event handling for, 600–604

model-view-controller analysis of, 634, 636

rearranging automatically, 637

ButtonUIListener class, 636

Byte class

converting from byte, 256

hashCode method, 241

toUnsignedInt method, 44

byte type, 43

C

C programming language

assert macro in, 400

function pointers in, 286

integer types in, 6

C# programming language, 8

foreach loop in, 86

polymorphism in, 222

useful features of, 12

C++ programming language

, (comma) operator in, 62

:: operator in, 151, 211

>> operator in, 60

access privileges in, 154

algorithms in, 543

arrays in, 112, 122

bitset template in, 559

boolean values in, 48

classes in, 40

nested, 341

code units and code points in, 62

copy constructors in, 135

dynamic binding in, 213

dynamic casts in, 225

exceptions in, 375, 378–379, 383

fields in:

instance, 173–174

static, 159

for loop in, 86, 96

function pointers in, 286

#include in, 183

inheritance in, 208, 217, 305

integer types in, 6, 43

iterators as parameters in, 554

methods in:

accessor, 138

default, 308

destructor, 180

static, 159

namespace, using directives in, 183

new operator in, 147

NULL, object pointers in, 135

operator overloading in, 105

passing parameters in, 165, 168

performance of, compared to Java, 561

polymorphism in, 222

protected modifier in, 232

pure virtual functions (= 0) in, 227

references in, 135

Standard Template Library in, 482, 487

static member functions in, 40

strings in, 64–66

superclasses in, 212

syntax of, 3

templates in, 12, 436, 439, 442

this pointer in, 175

type parameters in, 438

variables in, 51

redefining in nested blocks, 87

vector template in, 250

virtual constructors in, 267

void* pointer in, 233

Calendar class, 136

get/setTime methods, 222

Calendars

displaying, 138–140

vs. time measurement, 136

CalendarTest/CalendarTest.java, 140

Call by reference, 163

Call by value, 163–170

Callable interface, 806

call method, 800–801

wrapper for, 801

Callables, 800–802

Callbacks, 310–313

Camel case (CamelCase), 38

cancel method (Future), 801–802, 804, 826

CancellationException, 826

Carriage return, escape sequence for, 46

case statement, 100

cast method (Class), 468

Casts, 57, 223–225

bad, 374

checking before attempting, 224

catch statement, 381–395

ceiling method (NavigableSet), 516

ChangeListener interface, stateChanged method, 666

char type, 46–47

Character class

converting from char, 256

hashCode method, 241

isJavaIdentifierXxx methods, 49

Characters, formatting output for, 79

charAt method (String), 67–68

checkBox/CheckBoxFrame.java, 653

Checkboxes, 651–654

in menus, 676–677

Checked exceptions, 265–268

applicability of, 397

declaring, 375–378

suppressing with generics, 454–455

Checked views, 536

checkedCollection methods (Collections), 539

Child classes. See Subclasses

children method (ProcessHandle), 835, 838

Choice components, 651–671

borders, 658–661

checkboxes, 651–654

combo boxes, 661–664

radio buttons, 654–658

sliders, 665–671

ChronoLocalDate interface, 463

Church, Alonzo, 323

circleLayout/CircleLayout.java, 703

circleLayout/CircleLayoutFrame.java, 706

Circular arrays, 484–485

Clark, Jim, 11

Class class, 264–267

cast method, 468

forName method, 265, 267

generic, 450, 467–470

getAudioClip method, 269

getClass method, 264

getComponentType method, 284

getConstructor method, 267, 468

getConstructors, getDeclaredConstructors methods, 271, 276

getDeclaredConstructor method, 468

getDeclaredMethods method, 271, 275, 287

getEnumConstants method, 468

getField, getDeclaredField methods, 282

getFields, getDeclaredFields methods, 271, 275, 279, 282

getGenericXxx methods, 478

getImage method, 269

getMethod method, 287

getMethods method, 271, 275

getName method, 247, 264–266

getPackageName method, 276

getResource, getResourceAsStream methods, 269, 271

getSuperclass method, 247, 468

getTypeParameters method, 478

newInstance method, 266, 468

Class constants, 51

Class diagrams, 130–131

.class file extension, 39

Class files, 184, 189

compiling, 39

locating, 190–191

names of, 39, 143

class keyword, 38

Class loaders, 363, 399–400

Class path, 189–191

setting, 191–192

Class wins rule, 310

Class<T> parameters, 469

ClassCastException, 224, 283, 303, 452, 459, 537

Classes, 127–128, 208–232

abstract, 225–231, 305–306

access privileges for, 154

adapter, 605–607

adding to packages, 184–187

analyzing:

capabilities of, 271–277

objects of, at runtime, 277–283

companion, 306–307

constructors for, 146

defining, 141–156

at runtime, 363

designing, 129, 204–206

documentation comments for, 199–202

encapsulation of, 127–128, 151–153

extending, 128

final, 221–223

generic, 248–249, 434–437, 459, 661

helper, 696

immutable, 155

implementing multiple interfaces, 305

importing, 181–183

inner, 340–359

instances of, 127, 132

loading, 265, 428

multiple source files for, 145

names of, 25, 38, 181, 206

full package, 181

number of basic types in, 204

package scope of, 187

parameters in, 150–151

predefined, 131–141

private methods in, 155

protected, 231–232

public, 199

accessing, 181

relationships between, 129–131

sharing, among programs, 189

unit testing, 160

wrapper, 256–260

ClassLoader class, 403

CLASSPATH environment variable, 26, 191

Cleaner class, 180

clear method

of BitSet, 560

of Collection, 489, 491

clearAssertionStatus method (ClassLoader), 403

Client-side locking, 768–769

clone method

of array types, 320

of Object, 153, 314–321, 326

clone/CloneTest.java, 320

clone/Employee.java, 320

Cloneable interface, 314–321

CloneNotSupportedException, 318

close method

of AutoCloseable, 389–390

of Handler, 422

Closeable interface, close method, 389

Closures, 334

Code errors, 373

Code planes, 47

Code points, code units, 47, 66

codePointAt, codePoints methods (String), 69

codePointCount method (String), 67, 70

Collection interface, 485, 492, 502

add method, 485, 489–492

addAll, clear methods, 489, 491

contains method, 489–490, 502

containsAll method, 489, 491, 502

equals method, 489

generic, 489–491

implementing, 307

isEmpty method, 307, 489–490

iterator method, 485, 490

remove, removeAll methods, 489, 491

removeIf method, 491, 549

retain method, 489

retainAll method, 491

size method, 489–490

stream method, 308

toArray method, 252, 489, 491

Collections, 481–563

algorithms for, 541–543

bounded, 485

bulk operations in, 549–550

concrete, 494–519

concurrent modifications of, 501

converting to arrays, 550–551

debugging, 502

elements of:

inserting, 492

maximum, 541

removing, 488

traversing, 486–487

interfaces for, 482–492

legacy, 552–563

mutable, 533

ordered, 492, 498

performance of, 493–494, 509

searching in, 546–547

sorted, 511

thread-safe, 536, 781–800

type parameters for, 434

using for method parameters, 552

Collections class, 544

addAll method, 548

binarySearch method, 546–547

checkedCollection methods, 539

copy method, 548

disjoint method, 549

emptyCollection methods, 540

emptySet method, 533, 540

enumeration method, 554–555

fill method, 548

frequency method, 549

indexOfSubList, lastIndexOfSubList methods, 548

list method, 555

max, min methods, 548

nCopies method, 533, 539

replaceAll method, 548

reverse method, 548

rotate method, 549

shuffle method, 544–545

singleton, singletonXxx methods, 533, 540

sort method, 543–546

swap method, 548

synchronizedCollection methods, 536, 539, 800

unmodifiableCollection methods, 535–536, 539

Collections framework. See Java collections framework (JCF)

Color class, 587–589

Colors

background/foreground, 588

changing, 609

predefined/custom, 588

Columns (of a text field), 643

Combo boxes, 661–664

adding items to, 662

current selection in, 662

comboBox/ComboBoxFrame.java, 663

command method (ProcessHandle.Info), 838

Command line

compiling/launching applications from, 24–26, 39

parameters in, 112–113

commandLine method (ProcessHandle.Info), 838

Comments, 41–42

blocks of, 42

for automatic documentation, 42, 198–204

not nesting, 42

to the end of line, 42

Companion classes, 306–307

Comparable interface, 296, 365, 439, 462, 543

compareTo method, 297–302

comparator method (SortedMap), 515, 523

Comparator interface, 313–314, 322, 339–340, 543

chaining comparators in, 339

comparing method, 339–340

lambdas and, 326

naturalOrder method, 340

nullFirst/Last methods, 340

reversed, reverseOrder methods, 340, 543, 546

thenComparing method, 339–340

compare method (integer types), 302, 326

compareAndSet method (AtomicType), 773

compareTo method

in subclasses, 303

of BigDecimal, BigInteger, 107

of Comparable, 297–302, 439, 462

of Enum, 263

of String, 69

Compilation errors, 31

Compiler

autoboxing in, 258

bridge methods in, 444

command-line options of, 429

creating bytecode files in, 39

deducting method types in, 438

enforcing throws specifiers in, 382

error messages in, 31, 377

just-in-time, 6–7, 15, 151, 222, 561

launching, 25

optimizing method calls in, 7, 222

overloading resolution in, 219

shared strings in, 64–65

translating inner classes in, 346

translating typed array lists in, 255

type parameters in, 433

warnings in, 101, 255

whitespace in, 40

CompletableFuture class, 817–823

acceptEither, applyToEither methods, 819–820

allOf, anyOf methods, 819–820

handle method, 819

runAfterXxx methods, 819–820

thenAccept, thenAcceptBoth, thenCombine, thenRun, whenComplete methods, 819

thenApply, thenApplyAsync, thenCompose methods, 817, 819

completableFutures/CompletableFutureDemo.java, 821

CompletionStage interface, 820

Component class, 623

getBackground/Foreground methods, 589

getFont method, 645

getPreferredSize method, 577, 579

getSize method, 573

inheritance hierarchies of, 638

isVisible method, 573

repaint method, 576, 579

setBackground/Foreground methods, 588–589

setBounds, setLocation methods, 570, 572–573

setCursor method, 620

setSize method, 573

setVisible method, 570, 573

validate method, 645

Components, 638

displaying information in, 574

labeling, 645–646

CompoundInterest/CompoundInterest.java, 118

Computations

asynchronous, 814–831

performance of, 53, 55

truncated, 53

compute, computeIfPresent/Absent methods (Map), 524

Concrete collections, 494–519

Concrete methods, 226

Concurrent hash maps

atomic updates in, 790–794

bulk operations on, 794–796

efficiency of, 789

size of, 789

vs. synchronization wrappers, 799

Concurrent modification detection, 501

Concurrent programming, 8, 733–834

synchronization in, 750–781

Concurrent sets, 796–797

ConcurrentHashMap class, 789–790

atomic updates in, 790–794

compute, computeIfXxx methods, 791–792

forEach method, 794–796

get method, 791

keySet, newKeySet methods, 796

mappingCount method, 789

merge method, 792

organizing buckets as trees in, 789

put, putIfAbsent methods, 791

reduce, reduceXxx methods, 794–796

replace method, 791

search, searchXxx methods, 794–796

concurrentHashMap/CHMDemo.java, 792

ConcurrentLinkedQueue class, 789–790

ConcurrentModificationException, 501, 789, 799

ConcurrentSkipListMap/Set classes, 789–790

Condition interface, 764

await method, 741

signal, signalAll methods, 775

vs. synchronization methods, 766

Condition objects, 758–764

Condition variables, 758

Conditional statements, 87–90

config method (Logger), 406, 421

Configuration files, 624–630

Confirmation dialogs, 709

Console class

reading passwords with, 77

readLine/Password methods, 78

console method (System), 78

Console, printing messages to, 38–41

ConsoleHandler class, 410–415, 423

const keyword, 52

Constants, 51–52

documentation comments for, 201

names of, 51

public, 52, 157

static, 157–158

Constructor class, 271

getDeclaringClass method, 276

getModifiers, getName methods, 271, 276

getXxxTypes methods, 276

newInstance method, 267, 469

Constructor expressions, 450

Constructor references, 332–333

Constructors, 146–148, 170–180

calling another constructor in, 175

defined, 132

documentation comments for, 199

field initialization in:

default, 171

explicit, 173

final, 271

initialization blocks in, 175–180

names of, 132, 147

no-argument, 172, 212, 361

overloading, 170–171

parameter names in, 174

private, 271

protected, 199

public, 199, 271

with super keyword, 211

ConstructorTest/ConstructorTest.java, 178

Consumer interface, 337

Consumer threads, 781

Container class, 638

add method, 601, 604, 639

setLayout method, 639

Containers, 638

contains method

of Collection, 489–490, 502

of HashSet, 509

containsAll method (Collection), 489, 491, 502

containsKey/Value methods (Map), 522

Content pane, 575

continue statement, 104

Control flow, 86–105

block scope, 86–87

breaking, 102–105

conditional statements, 87–90

loops, 91–95

determinate, 95–99

「for each」, 110–111

multiple selections, 99–101

Controllers, 632

Conversion characters, 79

Cooperative scheduling, 740

Coordinated Universal Time (UTC), 136

copy method (Collections), 548

copyArea method (Graphics), 597

copyOf method (Arrays), 111, 116, 283

copyOfRange method (Arrays), 116

CopyOnWriteArrayList class, 797, 799

CopyOnWriteArraySet class, 797

Core Java program examples, 23

Cornell, Gary, 1

Corruption of data, 750–754

cos method (Math), 54

Count of Monte Cristo, The (Dumas), 512, 825–827

Covariant return types, 445

createTypeBorder methods (BorderFactory), 658–660

Ctrl+\, for thread dump, 775

Ctrl+C, for program termination, 751, 761

Ctrl+O, Ctrl+S accelerators, 680

current method

of ProcessHandle, 835, 838

of ThreadLocalRandom, 779

Current user, 625

currentThread method (Thread), 743–746

Cursor class, getPredefinedCursor method, 615

Cursor shapes, 616

Custom layout managers, 702–706

Customizations. See Preferences

D

D suffix (double numbers), 45

Daemon threads, 746

Data exchange, 716–723

Data fields

initializing, 175–180

public, 146

Data types, 42–48

boolean type, 48

casting between, 57

char type, 46–47

conversions between, 56–57, 223–225

floating-point, 44–45

integer, 43–44

dataExchange/DataExchangeFrame.java, 719

dataExchange/PasswordChooser.java, 720

Date and time

formatting output for, 79–82

no built-in types for, 132

Date class, 136

getDay/Month/Year methods (deprecated), 137

toString method, 133

DateInterval class, 444

Deadlocks, 760, 775–779

in GUI, 780

Debugging, 8, 425–430

collections, 502

debuggers for, 426

generic types, 536

GUI programs, 381

including class names in, 354

intermittent bugs, 65, 569

messages for, 380

reflection for, 278

trapping program errors in a file for, 427

when running applications in terminal window, 25–26

Decrement operators, 58

decrementExact method (Math), 55

Deep copies, 316

deepToString method (Arrays), 118, 243

Default methods, 307–308

resolving conflicts in, 308–310

default statement, 100, 307–308

DefaultButtonModel class, 634, 636

DefaultComboBoxModel class, 662

Deferred execution, 336

Delayed interface, 783

getDelay method, 783, 787

DelayQueue class, 783, 787

delete method (StringBuilder), 75

Dependence, 129–131

Deprecated methods, 137–138

Deque interface, 516–518

methods of, 517

Deques, 516–518

Derived classes. See Subclasses

deriveFont method (Font), 591, 595

descendants method (ProcessHandle), 835, 838

Descender, descent (in typesetting), 591

descendingIterator method (NavigableSet), 516

destroy, destroyForcibly methods (Process), 834, 837

Determinate loops, 95–99

Development environments

choosing, 23–29

in terminal window, 25

integrated, 29–32

Device errors, 373

dialog/AboutDialog.java, 715

dialog/DialogFrame.java, 714

Dialogs, 706–732

accepting/canceling, 717

centering, 312

closing, 606, 681, 714, 717

confirmation, 709

creating, 712–716

data exchange in, 716–723

default button in, 718

displaying, 714

modal, 707–712

modeless, 707, 713–714

data exchange with, 717

root pane of, 718

Diamond syntax, 248

with anonymous subclasses, 433

Directories

starting, for a launched program, 84

working, for a process, 832

directory method (ProcessBuilder), 832, 836

disjoint method (Collections), 549

divide method (BigDecimal/BigInteger), 107

Division operator, 52

do/while loop, 92–93

Documentation comments, 42, 198–204

extracting, 203–204

for fields, 201

for methods, 200–201

for packages, 202

general, 201

HTML markup in, 199

hyperlinks in, 202

inserting, 199

links to other files in, 199

overview, 204

doInBackground method (SwingWorker), 825–826, 831

Do-nothing methods, 606

Double brace initialization, 354

Double class

compare method, 302

converting from double, 256

hashCode method, 241

POSITIVE_INFINITY, NEGATIVE_INFINITY, NaN constants, 45

double type, 44

arithmetic computations with, 53

converting to other numeric types, 56–57

DoubleAccumulator, DoubleAdder classes, 775

Double-precision numbers, 44–45

Doubly linked lists, 497

draw method (Graphics2D), 580

draw/DrawTest.java, 584

drawImage method (Graphics), 597

Drawing with mouse, 614–620

drawString method (Graphics/Graphics2D), 596

Drop-down lists, 661

Dynamic binding, 213, 218–221

Dynamic languages, 8

E

e (exponent), in numbers, 45

E

as type variable, 435

constant (Math), 55

Echo character, 647

Eclipse, 24, 29–32, 425

configuring projects in, 30

editing source files in, 31

error messages in, 31–32

imports in, 182

Effectively final variables, 390

Eiffel programming language, multiple inheritance in, 305

element method

of BlockingQueue, 782–783

of Queue, 517

Ellipse2D class, 580, 583

setFrameFromCenter method, 583

Ellipse2D.Double class, 587

Ellipses, 580, 583

bounding rectangles of, 582–583

constructing, 583

filling with color, 588

else statement, 87–89

else if statement, 89–90

emojis, 67

EmployeeTest/EmployeeTest.java, 144

empty method (String), 69

emptyCollection methods (Collections), 540

emptySet method (Collections), 533, 540

EmptyStackException, 396–398

Encapsulation, 127–128

benefits of, 151–153

protected instance fields and, 291

endsWith method (String), 69

ensureCapacity method (ArrayList), 249, 251

entering method (Logger), 421

Enterprise Edition (Java EE), 12, 19

entry method (Map), 533, 538

entrySet method (Map), 525–526

Enum class, 261–263

compareTo, ordinal methods, 263

toString, valueOf methods, 262–263

enum keyword, 52

Enumerated types, 52

equality testing for, 261

in switch statement, 101

enumeration method (Collections), 554–555

Enumeration interface, 482, 553–555

asIterator method, 554

nextElement, hasMoreElements methods, 487, 553–554

Enumeration maps/sets, 529

Enumerations, 261–263

legacy, 553–555

EnumMap class, 529, 531

as a concrete collection type, 495

enums/EnumTest.java, 262

EnumSet class, 529

allOf, noneOf, of, range methods, 531

as a concrete collection type, 495

environment method (ProcessBuilder), 837

environment variables, modifying, 833

EOFException, 378–379

Epoch, 136

equals method, 310

for wrappers, 257

hashCode method and, 239–240

implementing, 236

inheritance and, 234–238

of Arrays, 116, 238

of Collection, 489

of Object, 233–238, 247, 536

of proxy classes, 368

of Set, 494

of String, 65, 69

redefining, 239–240

equals/Employee.java, 244

equals/EqualsTest.java, 244

equals/Manager.java, 246

equalsIgnoreCase method (String), 65, 69

Error class, 374

Errors checking, in mutator methods, 152

code, 373

compilation, 31

device, 373

internal, 374, 377, 401

messages for, 384

NoClassDefFoundError, 26

physical limitations, 373

ThreadDeath, 742, 749, 780

user input, 373

Escape sequences, 46

Event delegation model, 598

Event dispatch thread, 569, 780–781

Event handling

defined, 598

semantic vs. low-level events, 621–622

summary of, 620–624

Event listeners, 598–599

with lambda expressions, 604

Event objects, 598

Event procedures, 598

Event sources, 598–599

EventObject class, 598

getActionCommand, getSource methods, 620

Exception class, 374, 393

Exception handlers, 267, 373

Exception specification, 376

Exceptions

ArrayIndexOutOfBoundsException, 110, 375–377

ArrayStoreException, 218, 448–449, 458

BadCastException, 468

CancellationException, 826

catching, 267–268, 377, 381–395

multiple, 383–384

changing type of, 384

checked, 265–268, 375–378, 397

ClassCastException, 224, 283, 303, 452, 459, 537

classification of, 373–375

CloneNotSupportedException, 318

ConcurrentModificationException, 501, 789, 799

creating classes for, 379–380

documentation comments for, 200

EmptyStackException, 396–398

EOFException, 378–379

FileNotFoundException, 376–378

finally clause in, 386–389

generics in, 454–455

hierarchy of, 373, 397

IllegalAccessException, 278–279, 282

IllegalStateException, 488, 492, 506, 516–517, 783

InterruptedException, 735, 743–746, 801

InvocationTargetException, 266

IOException, 85, 376–378, 382, 389

logging, 407, 416

micromanaging, 396

NoSuchElementException, 486, 492, 506, 517

NullPointerException, 149–150, 163, 258, 330, 375, 398

NumberFormatException, 398

propagating, 382, 398

rethrowing and chaining, 384, 427

RuntimeException, 374, 397

ServletException, 384

squelching, 398

stack trace for, 391–395

「throw early, catch late」, 399

throwing, 267–268, 378–379

TimeoutException, 801

tips for using, 396–399

uncaught, 428, 742, 747–749

unchecked, 268, 375–377, 397

unexpected, 407, 416

UnsupportedOperationException, 526, 535, 537, 539

using type variables in, 453

variables for, implicitly final, 384

vs. simple tests, 396

wrapping, 385

.exe file extension, 195

exec method (Runtime), 832

Executable JAR files, 194–195

Executable path, 20

execute method (SwingWorker), 826, 831

Execution flow, tracing, 406

ExecutorCompletionService class, 806

poll, submit, take methods, 811

Executors, 800–814

groups of tasks, controlling, 806–811

scheduled, 804

Executors class

newSingleThreadExecutor method, 803–804

newSingleThreadScheduledExecutor method, 803–805

newXxxThreadPool methods, 803–805

executors/ExecutorDemo.java, 808

ExecutorService interface, 802–805

invokeAny/All methods, 806, 811

shutdown method, 804–805

shutdownNow method, 804, 806

submit method, 803–805

Exit codes, 40

exit method (System), 40

exiting method (Logger), 406, 421

exitValue method (Process), 834, 837

exp method (Math), 55

Explicit parameters, 150–151

exploratory programming, 7

exportXxx methods (Preferences), 626, 630

extends keyword, 208–232, 439

External padding, 694

F

F suffix (float numbers), 45

Factorial functions, 392

Factory methods, 159

Fair locks, 758

Fallthrough behavior, 101

fdlibm (Freely Distributable Math Library), 55

Field class, 271

get method, 277, 283

getDeclaringClass method, 276

getModifiers, getName methods, 271, 276

getType method, 271

set method, 283

Field width, of numbers, 79

Fields

adding, in subclasses, 211

default initialization of, 171

documentation comments for, 199, 201

final, 157, 222

instance, 127, 146–152, 155, 173, 204

private, 204, 210

protected, 199, 231, 290–291

public, 199, 201

public static final, 304

static, 156–157, 177, 183, 452

volatile, 771–772

File dialogs, 723–732

adding accessory components to, 728

FileFilter class (Swing), methods of, 726, 731

FileFilter interface (java.io package), 726

FileHandler class, 410–415, 423

configuration parameters of, 412

FileNameExtensionFilter interface, 731

FileNotFoundException, 376–378

Files

filters for, 726–728

locating, 84

names of, 25, 83

opening/saving in GUI, 723–732

reading, 83

all words from, 390

in a separate thread, 825

writing, 84

FileView class, 727

getDescription, getName methods, 727, 731

getIcon, getTypeDescription methods, 727, 732

isTraversable method, 727, 732

fill method

of Arrays, 116

of Collections, 548

of Graphics2D, 588–589

Filter interface, 414

isLoggable method, 414, 425

final access modifier, 51, 221–223

checking, 271

for fields in interfaces, 304

for instance fields, 155

for methods in superclass, 303

for shared fields, 772

inner classes and, 350–351

finalize method, 180

finally clause, 386–389

return statements in, 388

unlock operation in, 755

without catch, 387

Financial calculations, 45

fine, finer, finest methods (Logger), 406, 421

first method (SortedSet), 515

First Person, Inc., 11

firstKey method (SortedMap), 523

FirstSample/FirstSample.java, 42

Flash, 567

Float class

converting from float, 256

hashCode method, 241

POSITIVE_INFINITY, NEGATIVE_INFINITY, NaN constants, 45

float type, 44

converting to other numeric types, 56–57

Floating-point numbers, 44–45

arithmetic computations with, 53

equality of, 97

formatting output for, 79

rounding, 45, 57

Floating-point overflow, 53

floor method (NavigableSet), 516

floorMod method (Math), 54

Flow layout manager, 637

FlowLayout class, 639

flush method (Handler), 422

FocusEvent class, 622

isTemporary method, 623

FocusListener interface, methods of, 623

Font class, 590–595

deriveFont method, 591, 595

getFamily, getFontName, getName methods, 595

getLineMetrics method, 592, 595

getStringBounds method, 591–592, 595

font/FontTest.java, 593

FontMetrics class, getFontRenderContext method, 596

Fonts, 589–596

checking availability of, 589

names of, 589–590

size of, 590–591

styles of, 590

typesetting properties of, 591

「for each」loop, 108–111

for array lists, 253

for collections, 486, 799

for multidimensional arrays, 118

for loop, 95–99

comma-separated lists of expressions in, 62

defining variables inside, 97

for collections, 486

forEach method

of ConcurrentHashMap, 794–796

of Map, 522

of StackWalker, 394

forEachRemaining method (Iterator), 485, 492

Foreground color, specifying, 588

Fork-join framework, 811

forkJoin/ForkJoinTest.java, 813

Format specifiers (printf), 79

format, formatTo methods (String), 80

Formattable interface, 80

Formatter class, methods of, 415, 425

forName method (Class), 265, 267

Frame class, 567

getIconImage method, 574

getTitle method, 573

isResizable method, 573

setIconImage method, 570, 574

setResizable method, 570, 573

setTitle method, 570, 573

Frames

closing by user, 570

creating, 567

displaying:

information in, 574–597

text in, 577

positioning, 570–574

properties of, 570–574

frequency method (Collections), 549

Function interface, 337

Functional interfaces, 326–328

abstract methods in, 326

annotating, 339

conversion to, 326

generic, 327

using supertype bounds in, 464

@FunctionalInterface annotation, 339

Functions. See Methods

Future interface, 806

cancel, get methods, 801–802, 804, 826

isCancelled, isDone methods, 801–802, 804

Futures, 800–802

combining, 819–820

completable, 817–823

FutureTask class, 800–802

G

Garbage collection, 65, 135

hash maps and, 526–527

GB18030 standard, 47

General Public License (GPL), 15

Generic programming, 431–479

classes in, 248–249, 434–437, 661

extending/implementing other generic classes, 459

no throwing or catching instances of, 453

collection interfaces in, 550

converting to raw types, 458

debugging, 536

expressions in, 442

in JVM, 441, 469–473

inheritance rules for, 457–458

legacy code and, 445

methods in, 437–438, 443–445, 489–492

not for arrays, 451–452

reflection and, 467–479

required skill levels for, 433

static fields or methods and, 452

type erasure in, 441–447, 451

clashes after, 455–456

type matching in, 469

vs. arrays, 332

vs. inheritance, 432–434

wildcard types in, 459–467

GenericArrayType interface, 470

getGenericComponentType method, 479

genericReflection/GenericReflectionTest.java, 471

genericReflection/TypeLiterals.java, 474

get method

of Array, 286

of ArrayList, 251, 254

of BitSet, 560

of ConcurrentHashMap, 791

of Field, 277, 283

of Future, 801–802, 804, 826

of LinkedList, 502

of List, 492, 505

of LongAccumulator, 774

of Map, 492, 520, 522

of Paths, 306

of Preferences, 625, 630

of ServiceLoader.Provider, 361–362

of ThreadLocal, 779

of Vector, 769

getActionCommand method

of ActionEvent, 622

of ButtonModel, 656, 658

of EventObject, 620

getActionMap method (JComponent), 614

getActualTypeArguments method (ParameterizedType), 479

getAdjustable, getAdjustmentType methods (AdjustmentEvent), 622

getAncestorOfClass method (SwingUtilities), 718, 723

getAndType methods (AtomicType), 773

getAscent method (LineMetrics), 596

getAudioClip method (Class), 269

getAvailableFontFamilyNames method (GraphicsEnvironment), 589

getBackground method (Component), 589

getBoolean method (Array), 286

getBounds method (TypeVariable), 478

getByte method (Array), 286

getCause method (Throwable), 393

getCenterX/Y methods (RectangularShape), 582, 586

getChar method (Array), 286

getClass method

always returning raw types, 447

of Class, 264

of Object, 247

getClassName method

of StackFrame, 394

of StackTraceElement, 395

getClickCount method (MouseEvent), 614, 620, 623

getColumns method (JTextField), 645

getComponentPopupMenu method (JComponent), 679

getComponentType method (Class), 284

getConstructor method (Class), 267, 468

getConstructors method (Class), 271, 276

getDataType methods (Preferences), 625, 630

getDay method (Date, deprecated), 137

getDayXxx methods (LocalDate), 137, 141

getDeclaredConstructor method (Class), 468

getDeclaredConstructors method (Class), 271, 276

getDeclaredField method (Class), 282

getDeclaredFields method (Class), 271, 275, 279, 282

getDeclaredMethods method (Class), 271, 275, 287

getDeclaringClass method

of java.lang.reflect, 276

of StackFrame, 394

getDefaultToolkit method (Toolkit), 313, 572, 574

getDefaultUncaughtExceptionHandler method (Thread), 748

getDelay, 783, 787

getDescent method (LineMetrics), 596

getDescription method

of FileFilter, 726, 731

of FileView, 727, 731

getDouble method (Array), 286

getEnumConstants method (Class), 468

getErrorStream method (Process), 832–833, 837

getExceptionTypes method (Constructor), 276

getFamily method (Font), 595

getField method (Class), 282

getFields method (Class), 271, 275, 282

getFileName method

of StackFrame, 394

of StackTraceElement, 395

getFilter method (Handler, Logger), 422

getFirst method (Deque), 517

getFloat method (Array), 286

getFont method (Component), 645

getFontMetrics method (JComponent), 592, 596

getFontName method (Font), 595

getFontRenderContext method

of FontMetrics, 596

of Graphics2D, 591, 596

getForeground method (Component), 589

getFormatter method (Handler), 423

getGenericComponentType method (GenericArrayType), 479

getGenericParameterTypes, getGenericReturnType methods (Method), 478

getGenericXxx methods (Class), 478

getGlobal method (Logger), 404, 427

getHandlers method (Logger), 422

getHead method (Formatter), 415, 425

getHeight method

of LineMetrics, 596

of RectangularShape, 582, 587

getIcon method

of FileView, 727, 732

of JLabel, 646

getIconImage method (Frame), 574

getImage method

of Class, 269

of ImageIcon, 574, 597

getInheritsPopupMenu method (JComponent), 679

getInputMap method (JComponent), 612, 614

getInputStream method (Process), 832, 837

getInstance method (StackWalker), 391, 394

getInstant method (LogRecord), 424

getInt method (Array), 286

getItem, getItemSelectable methods (ItemEvent), 623

getItemAt method (JComboBox), 662

getKey method (Map.Entry), 526

getKeyStroke method (KeyStroke), 611, 614

getKeyXxx methods (KeyEvent), 623

getLargestPoolSize method (ThreadPoolExecutor), 805

getLast method (Deque) of Deque, 517

getLeading method (LineMetrics), 596

getLength method (Array), 284, 286

getLevel method

of Handler, 423

of Logger, 422

of LogRecord, 423

getLineMetrics method (Font), 592, 595

getLineNumber method

of StackFrame, 394

of StackTraceElement, 395

getLogger method (Logger), 405, 420

getLoggerName method (LogRecord), 423

getLogManager method (LogManager), 424

getLong method (Array), 286

getLowerBounds method (WildcardType), 479

getMaxX/Y methods (RectangularShape), 586

getMessage method

of LogRecord, 424

of Throwable, 380

getMethod method (Class), 287

getMethodName method (StackFrame, StackTraceElement), 395

getMethods method (Class), 271, 275

getMillis method (LogRecord), 424

getMinX/Y methods (RectangularShape), 586

getModifiers method

of ActionEvent, 622

of java.lang.reflect, 271, 276

getMonth method (Date, deprecated), 137

getMonthXxx methods (LocalDate), 137, 141

getName method

of Class, 247, 264–266

of FileView, 727, 731

of Font, 595

of java.lang.reflect, 271, 276

of TypeVariable, 478

getNewState, getOldState methods (WindowEvent), 624

getOppositeWindow method (WindowEvent), 624

getOrDefault method (Map), 522

getOutputStream method (Process), 832, 837

getOwnerType method (ParameterizedType), 479

getPackageName method (Class), 276

getPaint method (Graphics2D), 589

getParameters method (LogRecord), 424

getParameterTypes method (Method), 276

getParent method (Logger), 422

getPassword method (JPasswordField), 647

getPoint method (MouseEvent), 620, 623

getPredefinedCursor method (Cursor), 615

getPreferredSize method (Component), 577, 579

getProperties method (System), 556, 558

getProperty method

of Properties, 556–557

of System, 84, 558

getProxyClass method (Proxy), 368–369

getRawType method (ParameterizedType), 479

getResource, getResourceAsStream methods (Class), 269, 271

getResourceBundle, getResourceBundleName methods (LogRecord), 424

getReturnType method (Method), 276

getRootPane method (JComponent), 718, 723

getScreenSize method (Toolkit), 572, 574

getScrollAmount method (MouseWheelEvent), 623

getSelectedFile/Files methods (JFileChooser), 725, 730

getSelectedItem method (JComboBox), 662–664

getSelectedObjects method (ItemSelectable), 656

getSelection method (ButtonGroup), 656, 658

getSequenceNumber method (LogRecord), 424

getShort method (Array), 286

getSize method (Component), 573

getSource method (EventObject), 620

getSourceXxxName methods (LogRecord), 424

getStackTrace method (Throwable), 391, 393

getState method

of SwingWorker, 831

of Thread, 743

getStateChange method (ItemEvent), 623

getStringBounds method (Font), 591–592, 595

getSuperclass method (Class), 247, 468

getSuppressed method (Throwable), 390, 393

getTail method (Formatter), 415, 425

Getter/setter pairs. See Properties

getText method

of JLabel, 646

of JTextComponent, 644

getThrown, getThreadID methods (LogRecord), 424

getTime method (Calendar), 222

getTitle method (Frame), 573

getType method (Field), 271

getTypeDescription method (FileView), 727, 732

getTypeParameters method (Class, Method), 478

getUncaughtExceptionHandler method (Thread), 748

getUpperBounds method (WildcardType), 479

getUseParentHandlers method (Logger), 422

getValue method

of Action, 608, 613

of AdjustmentEvent, 622

of Map.Entry, 526

getWheelRotation method (MouseWheelEvent), 623

getWidth method

of Rectangle2D, 582

of RectangularShape, 582, 587

getWindow method (WindowEvent), 623

getX/Y methods of MouseEvent, 614, 620, 623

of RectangularShape, 587

getYear method

of Date (deprecated), 137

of LocalDate, 137, 141

GMT (Greenwich Mean Time), 136

Goetz, Brian, 734, 771

Gosling, James, 10–11

goto statement, 86, 102

Graphical User Interface (GUI), 565–630

components of, 631–732

choice components, 651–671

dialog boxes, 706–732

menus, 671–690

text input, 643–651

toolbars, 687–689

tooltips, 689–690

deadlocks in, 780

debugging, 381

events in, 598

keyboard focus in, 611

layout of, 636–642, 690–706

long-running tasks in, 823–831

Graphics class, 579, 597

copyArea, drawImage methods, 597

drawImage method, 597

Graphics editor applications, 614–620

Graphics2D class, 579–587

draw method, 580

drawString method, 596

fill method, 588–589

getFontRenderContext method, 591, 596

getPaint method, 589

setPaint method, 587–589

GraphicsEnvironment class, 589

Green project, 10–11

GregorianCalendar class, 138

add method, 138

constructors for, 136, 170–171

Grid bag layout, 691–702

padding in, 694

Grid layout, 642

gridbag/FontFrame.java, 697

gridbag/GBC.java, 698

GridBagConstraints class, 693

fill, anchor parameters, 694, 701

gridx/y, gridwidth/height parameters, 693, 701

helper class for, 696

insets field, 694, 701–702

ipadx/y parameters, 702

weightx/y fields, 694, 701

GridLayout class, 639, 642

Group layout, 691

GUI. See Graphical User Interface

H

handle method (CompletableFuture), 819

Handler class, 413

close method, 422

flush method, 422

get/setFilter methods, 423

get/setLevel methods, 423

getFormatter method, 423

publish method, 414, 422

setFormatter method, 415, 423

Handlers, 410–414

Hansen, Per Brinch, 770–771

「Has–a」relationship, 129–131

hash method (Objects), 240

Hash codes, 238–241, 507

default, 239

formatting output for, 79

Hash collisions, 508

Hash maps, 519

concurrent, 789–790

identity, 530–532

linked, 527–529

setting, 520

vs. tree maps, 520

weak, 526–527

Hash sets, 507–511

adding elements to, 512

linked, 527–529

Hash tables, 507–508

legacy, 553

load factor of, 509

rehashing, 509

hashCode method, 238–241

equals method and, 239–240

null-safe, 240

of Arrays, 241

of Boolean, Byte, Character, Double, Float, Integer, Long, Short, 241

of Object, 240, 511

of Objects, 240

of proxy classes, 368

of Set, 494

of String, 507

HashMap class, 519, 522

as a concrete collection type, 495

HashSet class, 509–511

add, contains methods, 509

as a concrete collection type, 495

iterating over, 486–487

Hashtable interface, 482, 552–553, 799–800

as a concrete collection type, 495

synchronized methods, 553

hasMoreElements method (Enumeration), 487, 553–554

hasNext method

of Iterator, 485–487, 492

of Scanner, 77

hasNextXxx methods (Scanner), 77–78

hasPrevious method (ListIterator), 499, 506

headMap method

of NavigableMap, 541

of SortedMap, 534, 541

headSet method

of NavigableSet, 534, 541

of SortedSet, 534, 540

Heap, 518

Height (in typesetting), 592

Helper classes, 696

Helper methods, 155, 306, 465

Hexadecimal numbers

formatting output for, 79

prefix for, 43

higher method (NavigableSet), 516

Hoare, Tony, 770

Hold count, 756

Holder types, 259

HotJava browser, 11

Hotspot just-in-time compiler, 561

HTML (HyperText Markup Language), 12–13

in javadoc comments, 199

in labels, 646

tables in, 691

HTML editors, 633

I

Icons

in menu items, 675–676

in sliders, 667

Identity hash maps, 530–532

identityHashCode method (System), 530, 532

IdentityHashMap class, 530–532

as a concrete collection type, 495

IEEE 754 specification, 45, 55

if statement, 87–90

IFC (Internet Foundation Classes), 566

IllegalAccessException, 278–279, 282

IllegalStateException, 488, 492, 506, 516–517, 783

ImageIcon class, 572

getImage method, 574, 597

Images, displaying, 597

ImageViewer/ImageViewer.java, 27

Immutable classes, 155

Implementations, 482–485

implements keyword, 298

Implicit parameters, 150–151

none, in static methods, 158

state of, 426

import statement, 181–183

importPreferences method (Preferences), 626, 630

Inconsistent state, 779

increment method (LongAdder), 774

Increment operators, 58

Incremental linking, 7

incrementAndGet method (AtomicType), 773

incrementExact method (Math), 55

Index (in arrays), 108

@index comment (javadoc), 202

indexOf method

of List, 505

of String, 69

indexOfSubList method (Collections), 548

info method

of Logger, 404, 406, 421

of ProcessHandle, 838

Information hiding. See Encapsulation

Inheritance, 129–131, 207–293

design hints for, 290–293

equality testing and, 234–238

hierarchies of, 216–217

multiple, 217, 305

preventing, 221–223

vs. type parameters, 432, 457–459

inheritance/Employee.java, 214

inheritance/Manager.java, 215

inheritance/ManagerTest.java, 214

inheritIO method (ProcessBuilder), 836

initCause method (Throwable), 393

Initialization blocks, 175–180

static, 177

initialize method (ThreadLocal), 779

Inlining, 7, 222

Inner classes, 340–359

accessing object state with, 341–345

anonymous, 352–355

applicability of, 346–349

defined, 340

local, 349

private, 344

static, 341, 356–359

syntax of, 345–346

vs. lambdas, 327

innerClass/InnerClassTest.java, 344

Input dialogs, 710

Input maps, 611–613

Input, reading, 75–78

InputTest/InputTest.java, 76

insert method

of JMenu, 674

of StringBuilder, 75

insertItemAt method (JComboBox), 662, 664

insertSeparator method (JMenu), 674

Instance fields, 127

final, 155

initializing, 204

explicit, 173

not present in interfaces, 297, 304

private, 146, 204

protected, 290–291

public, 146

shadowing, 148, 174

values of, 152

volatile, 771–772

vs. local variables, 148, 151, 171

instanceof operator, 61, 224–225, 304

Instances, 127

creating on the fly, 266

int type, 43

converting to other numeric types, 56–57

fixed size for, 6

platform-independent, 44

random number generator for, 180

Integer class compare method, 302, 326

converting from int, 256

hashCode method, 241

intValue method, 259

parseInt method, 258–259

toString method, 259

valueOf method, 259

Integer types, 43–44

arithmetic computations with, 52

arrays of, 243

computations of, 55

formatting output for, 79

no unsigned types in Java, 44

Integrated Development Environment (IDE), 20, 29–32

interface keyword, 296

Interface types, 484

Interface variables, 303

Interfaces, 296–313

abstract classes and, 305–306

binary- vs. source-compatible, 308

callbacks and, 310–313

constants in, 304

defined, 296

documentation comments for, 199

evolution of, 308

extending, 304

for custom algorithms, 551–552

functional, 326–328

implementing, 298, 304–306

methods in:

clashes between, 308–310

do-nothing, 606

nonabstract, 326

private, 306

static, 306

no instance fields in, 297, 304

properties of, 303–305

public, 199

tagging, 317, 442, 494

vs. implementations, 482–485

interfaces/Employee.java, 301

interfaces/EmployeeSortTest.java, 300

Intermittent bugs, 65, 569

Internal errors, 374, 377, 401

Internal padding, 694

Internationalization. See Localization

Internet Explorer browser

Java in, 10

security of, 15

Interpreted languages, 15

Interpreter, 7

interrupt method (Thread), 743–746

interrupted method (Thread), 745–746

InterruptedException, 735, 743–746, 801

IntHolder class, 259

Intrinsic locks, 764, 770

Introduction to Algorithms (Cormen et al.), 512

intValue method (Integer), 259

Invocation handlers, 363

InvocationHandler interface, 363, 368

InvocationTargetException, 266

invoke method

of InvocationHandler, 363, 368

of Method, 286–290

invokeAny/All methods (ExecutorService), 806, 811

IOException, 85, 376–378, 382, 389

「Is–a」relationship, 129–131, 217, 291

isAbstract method (Modifier), 277

isAccessible method (AccessibleObject), 282

isActionKey method (KeyEvent), 623

isAlive method (Process), 834, 837

isCancelled, isDone methods (Future), 801–802, 804

isDefaultButton method (JButton), 723

isEditable method

of JComboBox, 664

of JTextComponent, 643

isEmpty method (Collection), 307, 489–490

isEnabled method (Action), 608, 613

isFinal method (Modifier), 271, 277

isInterface method (Modifier), 277

isInterrupted method (Thread), 743–746

isJavaIdentifierXxx methods (Character), 49

isLoggable method (Filter), 414, 425

isNaN method (Double), 45

isNative method (Modifier), 277

isNativeMethod method (StackFrame, StackTraceElement), 395

ISO 8859-1 standard, 47

isPopupTrigger method (JPopupMenu, MouseEvent), 678

isPrivate, isProtected, isPublic methods (Modifier), 271, 277

isProxyClass method (Proxy), 368–369

isResizable method (Frame), 573

isSelected method

of AbstractButton, 677

of JCheckBox, 652, 654

isStatic, isStrict, isSynchronized, isVolatile methods (Modifier), 277

isTemporary method (FocusEvent), 623

isTraversable method (FileView), 727, 732

isVisible method (Component), 573

ItemEvent class, 622

getXxx methods, 623

ItemListener interface, itemStateChanged method, 623

ItemSelectable interface, getSelectedObjects method, 656

Iterable interface, 110

iterator method

of Collection, 485, 490

of ServiceLoader, 362

Iterator interface, 485–488

「for each」loop, 486

forEachRemaining method, 485, 492

generic, 489

hasNext method, 485–487, 492

next method, 485–488, 492

remove method, 485, 487–488, 492

Iterators, 485–488

being between elements, 487

weakly consistent, 789

IzPack utility, 195

J

J#, J++ programming languages, 8

Jar Bundler utility, 195

JAR files, 189, 192–198

creating, 192–193

dropping in jre/lib/ext directory, 192

executable, 194–195

manifest of, 193–194

multi-release, 195–197

resources and, 268–271

jar program, 192–193

command-line options of, 193–194, 197–198

Java 2 (J2), 19

Java 2D library, 579–587

floating-point coordinates in, 580

Java browser plug-in, 10

Java bug parade, 39

Java collections framework (JCF), 481–563

algorithms in, 541–543

converting to/from arrays in, 550–551

interfaces in, 492–494

legacy classes in, 552–563

operations in:

bulk, 549–550

optional, 537

separating interfaces from implementations in, 482–485

views and wrappers in, 532–541

vs. traditional collections libraries, 487

Java Concurrency in Practice (Goetz), 734

Java Development Kit (JDK), 6, 17–35

documentation in, 71–73, 613

downloading, 18–20

fonts shipped with, 590

installation of, 18–23

default, 192

setting up, 20–22

.java file extension, 39

Java Language Specification, 39

Java look-and-feel, 611

Java Memory Model and Thread Specification, 771

java program, 25

command-line options of, 197, 400–401

Java programming language architecture-neutral object file format of, 6

as a programming platform, 1–2

available under GPL, 15

basic syntax of, 38–41, 142

calling by value in, 164

case-sensitiveness of, 26, 38, 48–50, 553

design of, 2–8

documentation for, 23

dynamic, 8

dynamic binding in, 213, 218–221

garbage collection in, 65, 135

history of, 10–13

interpreter in, 7

libraries in, 12, 14

installing, 22–23

misconceptions about, 13–16

multithreading in, 8, 733–838

networking capabilities of, 4

no multiple inheritance in, 305

no operator overloading in, 105

no unsigned types in, 44

performance of, 7, 561

portability of, 6, 14, 53

reliability of, 4

reserved words in, 38, 49, 52

security of, 5, 15

simplicity of, 3–4, 323

strongly typed, 42, 299

versions of, 11, 13, 565, 691

vs. C++, 3

Java Runtime Environment (JRE), 19

Java virtual machine (JVM), 6

generics in, 441, 469–473

launching, 25

managing applications in, 429

optimizing execution in, 406

precomputing method tables in, 220

thread priority levels in, 749

truncating arithmetic computations in, 53

watching class loading in, 428

Java Virtual Machine Specification, 39

java.awt.BorderLayout API, 641

java.awt.Color API, 589

java.awt.Component API, 573, 579, 589, 620, 645

java.awt.Container API, 604, 639

java.awt.event.MouseEvent API, 620, 678

java.awt.event.WindowListener API, 607

java.awt.event.WindowStateListener API, 607

java.awt.FlowLayout API, 639

java.awt.Font API, 595

java.awt.font.LineMetrics API, 596

java.awt.FontMetrics API, 596

java.awt.Frame API, 573–574

java.awt.geom.RectangularShape API, 586–587

java.awt.geom.Xxx2D.Double APIs, 587

java.awt.Graphics API, 597

java.awt.Graphics2D API, 589, 596

java.awt.GridBagConstraints API, 701–702

java.awt.GridLayout API, 642

java.awt.LayoutManager API, 706

java.awt.Toolkit API, 313, 574

java.awt.Window API, 573, 579

java.io.Console API, 78

java.io.PrintWriter API, 85

java.lang.Boolean API, 241

java.lang.Byte API, 241

java.lang.Character API, 241

java.lang.Class API, 247, 267, 271, 275–276, 282, 468, 478

java.lang.ClassLoader API, 403

java.lang.Comparable API, 302

java.lang.Double API, 241, 302

java.lang.Enum API, 263

java.lang.Exception API, 393

java.lang.Float API, 241

java.lang.Integer API, 241, 259, 302

java.lang.Long API, 241

java.lang.Object API, 128, 240, 247, 511, 768

java.lang.Objects API, 240

java.lang.Process API, 837–838

java.lang.ProcessBuilder API, 836–837

java.lang.ProcessHandle API, 838

java.lang.ProcessHandle.Info API, 838

java.lang.reflect package, 271, 283

java.lang.reflect.AccessibleObject API, 282

java.lang.reflect.Array API, 286

java.lang.reflect.Constructor API, 267, 276, 469

java.lang.reflect.Field API, 276, 283

java.lang.reflect.GenericArrayType API, 479

java.lang.reflect.InvocationHandler API, 368

java.lang.reflect.Method API, 276, 290, 478

java.lang.reflect.Modifier API, 276–277

java.lang.reflect.ParameterizedType API, 479

java.lang.reflect.Proxy API, 369

java.lang.reflect.TypeVariable API, 478

java.lang.reflect.WildcardType API, 479

java.lang.Runnable API, 739

java.lang.RuntimeException API, 394

java.lang.Short API, 241

java.lang.StackTraceElement API, 395

java.lang.StackWalker API, 394

java.lang.StackWalker.StackFrame API, 394–395

java.lang.String API, 68–70

java.lang.StringBuilder API, 74–75

java.lang.System API, 78, 532, 558

java.lang.Thread API, 739, 741, 743, 746–749

java.lang.Thread.UncaughtExceptionHandler API, 748

java.lang.ThreadGroup API, 749

java.lang.ThreadLocal API, 779

java.lang.Throwable API, 267, 380, 393

java.logging module, 404

java.math.BigDecimal API, 107

java.math.BigInteger API, 107

java.nio.file.Path API, 86

java.text.NumberFormat API, 260

java.time.LocalDate API, 141

java.util.ArrayDeque API, 518

java.util.ArrayList API, 251, 254

java.util.Arrays API, 116, 238, 241, 302, 540

java.util.BitSet API, 560

java.util.Collection API, 490–491, 549

java.util.Collections API, 539–540, 544–545, 547–549, 555, 800

java.util.Comparator API, 546

java.util.concurrent package, 755

efficient collections in, 789–790

java.util.concurrent.ArrayBlockingQueue API, 787

java.util.concurrent.atomic package, 773

java.util.concurrent.BlockingDeque API, 788

java.util.concurrent.BlockingQueue API, 788

java.util.concurrent.Callable API, 801

java.util.concurrent.ConcurrentXxx APIs, 790

java.util.concurrent.Delayed API, 787

java.util.concurrent.DelayQueue API, 787

java.util.concurrent.ExecutorCompletionService API, 811

java.util.concurrent.Executors API, 804–805

java.util.concurrent.ExecutorService API, 805, 811

java.util.concurrent.Future API, 802

java.util.concurrent.FutureTask API, 802

java.util.concurrent.LinkedBlockingDeque API, 787

java.util.concurrent.LinkedBlockingQueue API, 787

java.util.concurrent.locks.Condition API, 764

java.util.concurrent.locks.Lock API, 758, 763

java.util.concurrent.locks.ReentrantLock API, 758

java.util.concurrent.PriorityBlockingQueue API, 787

java.util.concurrent.ScheduledExecutorService API, 805

java.util.concurrent.ThreadLocalRandom API, 779

java.util.concurrent.ThreadPoolExecutor API, 805

java.util.concurrent.TransferQueue API, 788

java.util.Deque API, 517

java.util.Enumeration API, 554

java.util.EnumMap API, 531

java.util.EnumSet API, 531

java.util.function API, 327

java.util.HashMap API, 522

java.util.HashSet API, 511

java.util.IdentityHashMap API, 531

java.util.Iterator API, 492

java.util.LinkedHashMap API, 530–531

java.util.LinkedHashSet API, 530

java.util.LinkedList API, 506

java.util.List API, 505, 538, 540, 545, 549

java.util.ListIterator API, 506

java.util.logging.ConsoleHandler API, 423

java.util.logging.FileHandler API, 423

java.util.logging.Filter API, 425

java.util.logging.Formatter API, 425

java.util.logging.Handler API, 422–423

java.util.logging.Logger API, 420–422

java.util.logging.LogManager API, 424–425

java.util.logging.LogRecord API, 423–424

java.util.Map API, 522, 524, 526, 538

java.util.Map.Entry API, 526

java.util.NavigableMap API, 541

java.util.NavigableSet API, 516, 541

java.util.Objects API, 238

java.util.prefs.Preferences API, 629–630

java.util.PriorityQueue API, 519

java.util.Properties API, 557

java.util.Queue API, 516–517

java.util.Random API, 180

java.util.Scanner API, 77–78, 85

java.util.ServiceLoader API, 362

java.util.ServiceLoader.Provider API, 362

java.util.Set API, 538

java.util.SortedMap API, 523, 541

java.util.SortedSet API, 515, 540

java.util.Stack API, 559

java.util.TreeMap API, 523

java.util.TreeSet API, 515

java.util.WeakHashMap API, 530

JavaBeans, 729

javac program, 25

command-line options of, 197–198

current directory in, 190

javadoc program, 198–204

command-line options of, 203

comments in, 199–202

extracting, 203–204

overview, 204

redeclaring Object methods for, 326

HTML markup in, 199

hyperlinks in, 202

links to other files in, 199

online documentation of, 204

JavaFX platform

and threads, 824

versions of, 195–197, 567

javafx.css.CssParser class, 195–197

javap program, 197, 347

JavaScript programming language, 15

javax.swing package, 569

javax.swing.AbstractAction API, 676

javax.swing.AbstractButton API, 658, 674–677, 681

javax.swing.Action API, 613

javax.swing.border.LineBorder API, 661

javax.swing.border.SoftBevelBorder API, 660

javax.swing.BorderFactory API, 659–660

javax.swing.ButtonGroup API, 658

javax.swing.ButtonModel API, 658

javax.swing.event.MenuListener API, 683

javax.swing.filechooser.FileFilter API, 731

javax.swing.filechooser.FileNameExtensionFilter API, 731

javax.swing.filechooser.FileView API, 731–732

javax.swing.ImageIcon API, 574

javax.swing.JButton API, 604, 723

javax.swing.JCheckBox API, 654

javax.swing.JCheckBoxMenuItem API, 676

javax.swing.JComboBox API, 664

javax.swing.JComponent API, 579, 596, 614, 645, 661, 679, 690, 723

javax.swing.JDialog API, 716

javax.swing.JFileChooser API, 730–731

javax.swing.JFrame API, 579, 674

javax.swing.JLabel API, 646

javax.swing.JMenu API, 673–674

javax.swing.JMenuItem API, 674–675, 681, 683

javax.swing.JOptionPane API, 312, 710–712

javax.swing.JPasswordField API, 647

javax.swing.JPopupMenu API, 678

javax.swing.JRadioButton API, 657

javax.swing.JRadioButtonMenuItem API, 677

javax.swing.JRootPane API, 723

javax.swing.JScrollPane API, 651

javax.swing.JSlider API, 671

javax.swing.JTextArea API, 650–651

javax.swing.JTextField API, 645

javax.swing.JToolBar API, 690

javax.swing.KeyStroke API, 614

javax.swing.SwingUtilities API, 723

javax.swing.SwingWorker API, 831

javax.swing.text.JTextComponent API, 643

javax.swing.Timer API, 313

JButton class, 601, 604, 610, 635

isDefaultButton method, 723

JCheckBox class, 651–654

is/setSelected methods, 652, 654

JCheckBoxMenuItem class, 676–677

JComboBox class, 622–623, 661–664

addItem method, 662–664

getItemAt method, 662

getSelectedItem method, 662–664

insertItemAt method, 662, 664

isEditable method, 664

removeXxx methods, 662, 664

setEditable method, 662, 664

setModel method, 662

JComponent class, 575

action maps, 612

get/setComponentPopupMenu methods, 678–679

get/setInheritsPopupMenu methods, 678–679

getActionMap method, 614

getFontMetrics method, 592, 596

getInputMap method, 612, 614

getRootPane method, 718, 723

input maps, 611–613

paintComponent method, 575–577, 579, 592, 597

revalidate method, 644–645

setBorder method, 659, 661

setFont method, 645

setToolTipText method, 690

jconsole program, 429, 775

logging control with, 409

JDialog class, 712–716

setDefaultCloseOperation method, 714

setVisible method, 714, 716–717

JDK. See Java Development Kit

JEditorPane class, 649

JFileChooser class, 723–732

addChoosableFileFilter method, 730

getSelectedFile/Files methods, 725, 730

resetChoosableFilters method, 727, 731

setAcceptAllFileFilterUsed method, 726, 730

setAccessory method, 731

setCurrentDirectory method, 724, 730

setFileFilter method, 726, 730

setFileSelectionMode method, 725, 730

setFileView method, 727–728, 731

setMultiSelectionEnabled method, 725, 730

setSelectedFile/Files methods, 725, 730

showDialog, showXxxDialog methods, 718, 723, 725, 730

JFrame class, 567–571, 638

add method, 579

internal structure of, 575

setJMenuBar method, 672, 674

JLabel class, 645–646, 728

methods of, 646

JMenu class

add method, 672–674

addSeparator method, 672, 674

insert, insertSeparator methods, 674

remove method, 674

JMenuBar class, 672–674

JMenuItem class, 674–675

setAccelerator method, 680–681

setEnabled method, 682–683

setIcon method, 675

Jmol applet, 9

join method (Thread), 70, 741–743

JOptionPane class, 707–712

message types, 708

showConfirmDialog method, 707–711

showInputDialog method, 707–709, 712

showInternalConfirmDialog method, 711

showInternalInputDialog method, 712

showInternalMessageDialog method, 710

showInternalOptionDialog method, 711

showMessageDialog method, 312, 707–710

showOptionDialog method, 707–709, 711

JPanel class, 637

JPasswordField class, getPassword, setEchoChar methods, 647

JPopupMenu class, 677–679

isPopupTrigger, show methods, 678

JRadioButton class, 654–658

JRadioButtonMenuItem class, 677

JRootPane class, setDefaultButton method, 718, 723

JScrollbar class, 622

JScrollPane class, 651

JShell program, 7, 32–35

JSlider class, 665–671

setInverted method, 667

setLabelTable method, 445, 667, 671

setPaintLabels, setPaintTicks, setSnapToTicks methods, 666, 671

setPaintTrack method, 667, 671

setXxxTickSpacing methods, 671

JTextArea class, 647–648

append method, 650

setColumns, setRows methods, 647, 650

setLineWrap method, 648, 650

setTabSize method, 651

setWrapStyleWord method, 651

JTextComponent class getText method, 644

is/setEditable methods, 643

setText method, 643–644

JTextField class, 622, 643–645

getColumns method, 645

setColumns method, 644–645

JToolBar class, 688–689

add, addSeparator methods, 689–690

JUnit framework, 426

Just-in-time compiler, 6–7, 15, 151, 222, 561

JVM. See Java virtual machine

K

K type variable, 435

Key/value pairs. See Properties

Keyboard

associating with actions, 611

focus of, 611

mnemonics for, 679–681

KeyEvent class, 622

getKeyXxx, isActionKey methods, 623

KeyListener interface, keyXxx methods, 623

keys method (Preferences), 626, 629

keySet method

of ConcurrentHashMap, 796

of Map, 525–526

KeyStroke class, getKeyStroke method, 611, 614

Knuth, Donald, 102

KOI-8

standard, 47

L

L suffix (long integers), 43

Labeled break statement, 102

Labels

for components, 645–646

for slider ticks, 666

Lambda expressions, 322–340

accessing variables in, 333–335

atomic updates with, 773

capturing values by, 334

for event listeners, 604

functional interfaces and, 326

method references and, 328

no assigning to a variable of type Object, 327

parameter types of, 324

processing, 335–339

result type of, 325

scope of, 335

syntax of, 323–326

this keyword in, 335

vs. inner classes, 327

lambda/LambdaTest.java, 325

Langer, Angelika, 479

last method (SortedSet), 515

lastIndexOf method

of List, 505

of String, 70

lastIndexOfSubList method (Collections), 548

lastKey method (SortedMap), 523

Launch4J utility, 195

Layout management, 636–642

border, 639–641

box, 691

custom, 702–706

flow, 637

grid, 642

grid bag, 691–702

group, 691

sophisticated, 690–706

spring, 691

layoutContainer method (LayoutManager), 706

LayoutManager interface

designing custom, 702–706

methods of, 706

LayoutManager2 interface, 703

Leading (in typesetting), 592

Legacy code and generics, 445–446

Legacy collections, 552–563

bit sets, 559–563

enumerations, 553–555

hash tables, 553

property maps, 555–558

stacks, 558

length method

of arrays, 110

of BitSet, 560

of String, 66–67, 70

of StringBuilder, 74

Line2D class, 580, 584

Line2D.Double class, 587

LineBorder class, 659, 661

Linefeed, escape sequence for, 46

LineMetrics class, 592

getXxx methods, 596

Lines, 580

constructing, 584

@link comment (javadoc), 202

Linked hash maps/sets, 527–529

Linked lists, 496–506

concurrent modifications of, 501

doubly linked, 497

printing, 503

random access in, 502, 542

removing elements from, 498

LinkedBlockingDeque class, 787

LinkedBlockingQueue class, 782, 787

LinkedHashMap class, 527–531

access vs. insertion order, 528

as a concrete collection type, 495

removeEldestEntry method, 528, 531

LinkedHashSet class, 527–530

as a concrete collection type, 495

LinkedList class, 484, 498, 502, 516

addFirst/Last, getFirst/Last methods, 506

as a concrete collection type, 495

get method, 502

listIterator method, 499

next/previousIndex methods, 503

removeAll method, 503

removeFirst/Last methods, 506

linkedList/LinkedListTest.java, 504

Linux operating system

Eclipse versions for, 29

JDK versions for, 18

no thread priorities in Oracle JVM for, 749

pop-up menus in, 678

setting paths in, 20, 189–191

setting up JDK in, 20

troubleshooting Java programs in, 26

list method (Collections), 555

List interface, 492

add method, 492, 505

addAll method, 505

get method, 492, 505

indexOf, lastIndexOf methods, 505

listIterator method, 505

of method, 532–533, 538, 540

remove method, 492, 505

replaceAll method, 549

set method, 492, 505

sort method, 545

subList method, 534, 540

Listener interfaces, 598

Listener objects, 598

Listeners. See Action listeners, Event listeners, Window listeners

ListIterator interface, 502

add method, 493, 499–501, 506

hasPrevious method, 499, 506

next/previousIndex methods, 506

previous method, 499, 506

remove method, 501

set method, 501, 506

listIterator method

of LinkedList, 499

of List, 505

Lists, 492

modifiable/resizable, 544

with given elements, 532

load method

of Properties, 555, 557

of ServiceLoader, 362

Local inner classes, 349

accessing final variables from outer methods in, 350–351

Local variables

annotating, 446

vs. instance fields, 148, 151, 171

LocalDate class, 135–137

extending, 292

getXxx methods, 137, 141

minusDays method, 141

now, of methods, 136, 141

plusDays method, 137, 141

processing arrays of, 463

Locales, 409

Localization, 132, 269–270, 409–410

Lock interface, 764

await method, 760–764

lock method, 758

newCondition method, 759, 763

signal method, 761–764

signalAll method, 760–764

tryLock method, 741

unlock method, 755, 758

vs. synchronization methods, 766

Locks, 755–758

client-side, 769

condition objects for, 758–764

deadlocks, 760, 775, 779

fair, 758

hold count for, 756

in synchronized blocks, 768–770

inconsistent state and, 779

intrinsic, 764, 770

not with try-with-resources statement, 755

reentrant, 756

log, log10 methods (Math), 55

Logger class

add/removeHandler methods, 422

entering, exiting methods, 406, 421

get/setFilter methods, 415, 422

get/setParent methods, 422

get/setUseParentHandlers methods, 422

getGlobal method, 404, 427

getHandlers method, 422

getLevel method, 422

getLogger method, 405, 420

info method, 404

log method, 406–407, 421

logp method, 406, 421

logrb method, 422

setLevel method, 404, 422

severe, warning, info, config, fine, finer, finest methods, 406, 421

throwing method, 407, 421

Loggers

configuring, 407–409

default, 404, 406

hierarchical names of, 405

writing your own, 405–407

Logging, 403–425

advanced, 405–407

basic, 404

file pattern variables for, 413

file rotation for, 413

filters for, 414

formatters for, 415

handlers for, 410–414

configuring, 412

including class names in, 354

levels of, 405–406

changing, 408–409

localization of, 409–410

messages for, 243

recipe for, 415–425

resource bundles and, 409–410

Logging proxy, 427

logging/LoggingImageViewer.java, 417

logging.properties file, 407–409

Logical conditions, 48

Logical「and」,「or」, 59

LogManager class, 409

getLogManager method, 424

read/updateConfiguration methods, 408, 425

LogRecord class, methods of, 423–424

Long class

converting from long, 256

hashCode method, 241

long type, 43

platform-independent, 44

LongAccumulator class, methods of, 774

LongAdder class, 774, 792

add, increment, sum methods, 774

Look-and-feel

appearance of buttons in, 632

pluggable, 727

Loops break statements in, 102–105

continue statements in, 104

determinate (for), 95–99

「for each」, 110–111

while, 91–95

LotteryArray/LotteryArray.java, 122

LotteryDrawing/LotteryDrawing.java, 115

LotteryOdds/LotteryOdds.java, 98

lower method (NavigableSet), 516

Low-level events, 621–622

M

Mac OS X operating system Eclipse versions for, 29

executing JARs in, 195

JDK versions for, 18

setting up JDK in, 20

main method, 160–163

body of, 40

declared public, 39

declared static void, 40

loading classes from, 265

not defined, 141, 177

separate for each class, 426

String[] args parameter of, 112–113

tagged with throws, 85

make program (UNIX), 145

MANIFEST.MF (manifest file), 193–194

editing, 194

newline characters in, 195

Map interface, 492

compute, computeIfPresent/Absent methods, 524

containsKey/Value methods, 522

entry method, 533, 538

entrySet, keySet methods, 525–526

forEach method, 522

get, put methods, 492, 520, 522

getOrDefault method, 522

merge method, 524

of method, 532–533, 538, 540

ofEntries method, 533, 538

putAll method, 522

putIfAbsent method, 524

remove method, 520

replaceAll method, 524

values method, 525–526

map/MapTest.java, 521

Map.Entry interface, 525

getKey, get/setValue methods, 526

mappingCount method (ConcurrentHashMap), 789

Maps, 519–532

adding/retrieving objects to/from, 520

concurrent, 789–790

garbage collecting, 527

hash vs. tree, 520

implementations for, 519

keys for, 520

enumerating, 525

subranges of, 534

with given key/value pairs, 532

Marker interfaces, 317

Math class, 54–55

E, PI static constants, 55, 157–158

floorMod method, 54

log, log10 methods, 55

pow method, 54, 158

round method, 57

sqrt method, 54

trigonometric functions, 54

xxxExact methods, 55

Matisse, 691

max method (Collections), 548

Maximum value, computing, 436

menu/MenuFrame.java, 683

MenuListener interface, 682

menuXxx methods, 682–683

Menus, 671–690

accelerators for, 680–681

checkboxes and radio buttons in, 676–677

icons in, 675–676

keyboard mnemonics for, 679–681

menu bar in, 671–672

menu items in, 671–677

enabling/disabling, 682–686

pop-up, 677–679

submenus in, 671–672

merge method

of ConcurrentHashMap, 792

of Map, 524

Merge sort algorithm, 544

META-INF directory, 193

META-INF/versions directory, 195

Method class, 271

getDeclaringClass method, 276

getGenericXxx methods, 478

getModifiers, getName methods, 271, 276

getReturnType method, 276

getTypeParameters method, 478

getXxxTypes methods, 276

invoke method, 286–290

toString method, 271

Method parameters. See Parameters

Method pointers, 286–288

Method references, 328–332

this, super parameters in, 330

Method tables, 220

Methods, 127

abstract, 226

in functional interfaces, 326

accessor, 138–141, 152–153, 461

adding, in subclasses, 211

applying to objects, 133

asynchronous, 800

body of, 40–41

bridge, 444–445, 456

calling by reference vs. by value, 163–170

casting, 223–225

concrete, 226

consistent, 235

default, 307–308

deprecated, 137–138

destructor, 180

documentation comments for, 199–202

do-nothing, 606

dynamic binding for, 213, 218–221

error checking in, 152

exception specification in, 376

factory, 159

final, 220–222, 271, 303

generic, 437–438, 443–445, 489–492

helper, 155, 465

inlining, 7, 222

invoking, 41

arbitrary, 286–290

mutator, 138–141, 152, 461

names of, 206

overloading, 171

overriding, 210–211, 237, 292

exceptions and, 378

return type and, 443

package scope of, 187

passing objects to, 133

private, 155, 220, 271, 306

protected, 199, 231, 291, 319

public, 199, 271, 298

reflexive, 235

resolving conflicts in, 308–310

return type of, 171, 219

signature of, 171, 219

static, 158–159, 183, 220, 452

adding to interfaces, 306

symmetric, 235

tracing, 364

transitive, 235

utility, 306

varargs, 260–261

passing generic types to, 448–449

visibility of, in subclasses, 221

methods/MethodTableTest.java, 288

Micro Edition (Java ME), 4, 12, 19

Microsoft

.NET platform, 6

ActiveX, 5, 15

C#, 8, 12, 222

Internet Explorer, 10, 15

J#, J++, 8

Visual Basic, 3, 132, 598

Visual Studio, 23

min method (Collections), 548

Minimum value, computing, 436

minimumLayoutSize method (LayoutManager), 706

minusDays method (LocalDate), 141

mod method (BigDecimal/BigInteger), 107

Modality, 707, 713

Model-view-controller design pattern, 632–636

classes in, 632

multiple views in, 634

Modifier class

isXxx methods, 271, 277

toString method, 276

Module path, 192

Modules, 12, 188

unnamed, 278

Modulus, 52

Monitor concept, 770–771

Mosaic browser, 11

Mouse events, 614–620

mouse/MouseComponent.java, 617

MouseAdapter class, 617

MouseEvent class, 622

getClickCount method, 614, 620, 623

getPoint method, 620, 623

getX/Y methods, 614, 620, 623

isPopupTrigger method, 678

translatePoint method, 623

MouseHandler class, 617

MouseListener interface, 615

mouseClicked method, 614, 617, 623

mouseDragged method, 616

mouseEntered/Exited methods, 617, 623

mousePressed/Released methods, 614, 623

MouseMotionHandler class, 617

MouseMotionListener interface, 615–617

mouseDragged method, 623

mouseMoved method, 615–617, 623

MouseWheelEvent class, 622

getScrollAmount, getWheelRotation methods, 623

MouseWheelListener interface, mouseWheelMoved method, 623

Multidimensional arrays, 116–121

printing, 243

ragged, 120–123

Multiple inheritance, 305

not supported in Java, 217

Multiple selections, 99–101

Multiplication operator, 52

multiply method (BigDecimal/BigInteger), 107

multiplyExact method (Math), 55

Multi-release JARs, 195–197

Multitasking, 733

Multithreading, 8, 733–838

deadlocks in, 760, 775–778

deferred execution in, 336

performance and, 758, 774, 783

preemptive vs. cooperative scheduling for, 740

synchronization in, 750–781

using pools for, 800–805

Mutator methods, 138, 461

error checking in, 152

N

\n (linefeed escape sequence), 46

NaN (not a number), 45

naturalOrder method (Comparator), 340

Naughton, Patrick, 10–11

NavigableMap interface, 494

subMap, headMap, tailMap methods, 541

NavigableSet interface, 494, 513, 534

ceiling, floor methods, 516

descendingIterator method, 516

higher, lower methods, 516

pollFirst/Last methods, 516

subSet, headSet, tailSet methods, 534, 541

nCopies method (Collections), 533, 539

negateExact method (Math), 55

Negation operator, 59

Negative infinity, 45

.NET platform, 6

NetBeans IDE, 20, 24, 425

Matisse, 691

Netscape, 11

IFC library, 566

LiveScript/JavaScript, 15

Navigator browser, 10

Networking, 4

new operator, 61, 68, 132, 147

not for interfaces, 303

return value of, 134

with arrays, 108

with generic classes, 248

with threads, 740

new keyword, in constructor references, 332

newCachedThreadPool method (Executors), 803–804

newCondition method (Lock), 759, 763

newFixedThreadPool method (Executors), 803–804

newInstance method

of Array, 283, 286

of Class, 266, 468

of Constructor, 267, 469

newKeySet method (ConcurrentHashMap), 796

newProxyInstance method (Proxy), 363, 368–369

newScheduledThreadPool method (Executors), 803–805

newSingleThreadExecutor method (Executors), 803–804

newSingleThreadScheduledExecutor method (Executors), 803–805

next method

of Iterator, 485–488, 492

of Scanner, 77

nextDouble method (Scanner), 76–77

nextElement method (Enumeration), 487, 553–554

nextIndex method

of LinkedList, 503

of ListIterator, 506

nextInt method

of Random, 180

of Scanner, 76–77

nextLine method (Scanner), 76–77

No-argument constructors, 172, 212, 361

NoClassDefFoundError, 26

node method (Preferences), 625, 629

noneOf method (EnumSet), 531

NoSuchElementException, 486, 492, 506, 517

Notepad text editor, 26

notHelloWorld/NotHelloWorld.java, 578

notify, notifyAll methods (Objects), 765, 768

now method (LocalDate), 136, 141

null value, 134

equality testing to, 235

nullFirst/Last methods (Comparator), 340

NullPointerException, 149–150, 163, 258, 330, 375, 398

Number class, 256

NumberFormat class

factory methods, 159

parse method, 260

NumberFormatException, 398

Numbers

generated random, 180, 778

rounding, 107

unsigned, 44

Numeric types casting, 57

comparing, 59, 340

converting:

to other numeric types, 56–57

to strings, 258

default initialization of, 171

fixed sizes for, 6

precision of, 105

printing, 78

O

Oak programming language, 10

Object class, 128, 232–247

clone method, 153, 314–321, 326

equals method, 233–238, 247, 310, 536

getClass method, 247

hashCode method, 239–240, 511

no redefining for methods of, 310

notify, notifyAll methods, 765, 768

toString method, 241–247, 310, 326

wait method, 741, 765, 768

Object references as method parameters, 164

converting, 223

default initialization of, 171

modifying, 164

Object traversal algorithms, 530

Object variables, 227

in predefined classes, 132–135

initializing, 134

setting to null, 134

vs. C++ object pointers, 135

vs. objects, 133

objectAnalyzer/ObjectAnalyzer.java, 280

objectAnalyzer/ObjectAnalyzerTest.java, 280

Object-oriented programming (OOP), 4, 126–131, 207

passing objects in, 310

time measurement in, 136

vs. procedural, 126–131

Objects, 126–129

analyzing at runtime, 277–283

applying methods to, 133

behavior of, 128

cloning, 314–321

comparing, 303

concatenating with strings, 242

constructing, 127, 170–180

damaged, 779–780

default hash codes of, 239

destruction of, 180

equality testing for, 233–238, 266

finalize method of, 180

identity of, 128

implementing an interface, 304

in predefined classes, 132–135

initializing, 132

intrinsic locks of, 764

passing to methods, 133

references to, 134

runtime type identification of, 264

serializing, 530

sorting, 297

state of, 127–128, 341–345

vs. object variables, 133

Objects class

hash, hashCode methods, 240

requireNonNull, requireNonNullElse methods, 149, 163

Octal numbers

formatting output for, 79

prefix for, 43

octonions, 48, 67

of method

of EnumSet, 531

of List, Map, Set, 532–533, 538, 540

of LocalDate, 136, 141

of Path, 83, 85–86, 306

of ProcessHandle, 835, 838

ofEntries method (Map), 533, 538

offer method

of BlockingQueue, 782–783, 788

of Queue, 516

offerFirst/Last methods

of BlockingDeque, 788

of Deque, 517

offsetByCodePoints method (String), 67, 69

onExit method (Process), 838

Online documentation, 68, 71–73, 198, 203

Operators

arithmetic, 52–53

bitwise, 60

boolean, 59

hierarchy of, 61–62

increment/decrement, 58

no overloading for, 105

relational, 59

Option dialogs, 707–712

Optional operations, 537

or method (BitSet), 560

Oracle, 12, 20

Ordered collections, 492, 498

ordinal method (Enum), 263

org.omg.CORBA package, 259

OSGi platform, 360

Output statements, 63

Output, formatting, 78–83

Overloading resolution, 170–171, 219

@Override annotation, 237

overview.html, 204

Owner frame, 713

P

p (exponent), in hexadecimal numbers, 45

pack method (Window), 577, 579

package statement, 181, 184

package.html, 202

package-info.java, 203

Packages, 180–192

accessing, 187–188

adding classes into, 184–187

documentation comments for, 199, 202

importing, 181

names of, 181, 265

unnamed, 184, 187, 203, 400

PackageTest/com/horstmann/corejava/Employee.java, 186

PackageTest/PackageTest.java, 185

paintComponent method (JComponent), 575–577, 579, 592, 597, 780

overriding, 621

pair1/PairTest1.java, 436

pair2/PairTest2.java, 440

pair3/PairTest3.java, 466

Parallelism threshold, 795

parallelXxx methods (Arrays), 797–798

Parameterized types. See Type parameters

ParameterizedType interface, 470

getXxx methods, 479

Parameters, 41, 163–170

checking, with assertions, 401–402

documentation comments for, 200

explicit, 150–151

implicit, 150–151, 158, 426

modifying, 164–167

names of, 174

string, 41

using collection interfaces in, 552

variable number of, 260–261

passing generic types to, 448–449

ParamTest/ParamTest.java, 168

Parent classes. See Superclasses

parse method (NumberFormat), 260

parseInt method (Integer), 258–259

Pascal programming language, 10

architecture-neutral object file format of, 6

passing parameters in, 165

Password fields, 647

PasswordChooser class, 716

Passwords

dialog box for, 717

reading from console, 77

PATH environment variable, 20

Path interface, of method, 83, 85–86, 306

Paths class, get method, 306

Payne, Jonathan, 11

peek method

of BlockingQueue, 782–783

of Queue, 517

of Stack, 559

peekFirst/Last methods (Deque), 517

Performance, 7

computations and, 53, 55

JAR files and, 189

measuring, 560–563

multithreading and, 758, 774, 783

of collections, 493–494, 509, 789

of Java vs. C++, 561

of simple tests vs. catching exceptions, 396

Physical limitations, 373

PI constant (Math), 55, 157–158

pid method (ProcessHandle), 838

plusDays method (LocalDate), 137, 141

Point class, 582

Point size (in typesetting), 590–591

Point2D class, 582

Point2D.Double class, 582, 587

Point2D.Float class, 582

poll method

of BlockingQueue, 782–783, 788

of ExecutorCompletionService, 811

of Queue, 517

pollFirst/Last methods

of Deque, 517, 788

of NavigableSet, 516

Polymorphism, 213, 217–218, 292

pop method (Stack), 559

Pop-up menus, 677–679

Positive infinity, 45

pow method (Math), 54, 158

Precision, of numbers, 79

Preconditions, 402

Predefined action table names, 609

Predefined classes, 131–141

mutator and accessor methods in, 138–141

objects and object variables in, 132–135

Predicate interface, 327, 337

Preemptive scheduling, 740

Preferences

accessing, 625

enumerating keys in, 626

importing/exporting, 626

Preferences class, 624–630

exportXxx methods, 626, 630

get, getDataType methods, 625, 630

importPreferences method, 626, 630

keys method, 626, 629

node method, 625, 629

platform-independency of, 624

put, putDataType methods, 625, 630

system/userNodeForPackage methods, 625, 629

system/userRoot methods, 625, 629

preferences/ImageViewer.java, 627

preferredLayoutSize method (LayoutManager), 706

previous method (ListIterator), 499, 506

previousIndex method

of LinkedList, 503

of ListIterator, 506

Prime numbers, 560

Primitive types, 42–48

as method parameters, 164

comparing, 340

converting to objects, 256

final fields of, 155

not for type parameters, 447

transforming hash map values to, 796

values of, not object, 233

Princeton University, 5

print method (System.out), 41, 78

printf method (System.out), 79–83

conversion characters for, 79

flags for, 80

for date and time, 81–82

parameters of, 260

println method (System.out), 41, 75, 328, 403

printStackTrace method (Throwable), 267, 391, 427

PrintWriter class, 84–85

Priority queues, 518

PriorityBlockingQueue class, 783, 787

PriorityQueue class, 519

as a concrete collection type, 495

priorityQueue/PriorityQueueTest.java, 518

private access modifier, 146, 187–188, 344

checking, 271

for fields, in superclasses, 210

for methods, 155

Procedures, 126

process method (SwingWorker), 825–827, 831

Process class, 831–838

destroy, destroyForcibly methods, 834, 837

exitValue method, 834, 837

getXxxStream methods, 832–833, 837

isAlive method, 834, 837

onExit method, 838

supportsNormalTermination method, 837

toHandle method, 835, 837

waitFor method, 834, 837

ProcessBuilder class, 831–838

directory method, 832, 836

environment method, 837

inheritIO method, 836

redirectXxx methods, 833, 836

start method, 834, 837

startPipeline method, 833, 837

Processes, 831–838

building, 832–834

killing, 834

running, 834–835

vs. threads, 734

ProcessHandle interface

allProcesses method, 835, 838

children, descendants methods, 835, 838

current method, 835, 838

info method, 838

of method, 835, 838

pid method, 838

ProcessHandle.Info, methods of, 838

Producer threads, 781

Programs. See Applications

Properties, 572

permitted to retrieve, 558

Properties class, 552

getProperty method, 556–557

load, store methods, 555, 557

setProperty method, 557

Property maps, 555–558

reading/writing, 555

PropertyChangeListener interface, 729

protected access modifier, 231–232, 290–291, 319

Proxies, 362–369

properties of, 368–369

purposes of, 364

Proxy class, 368–369

get/isProxyClass methods, 368–369

newProxyInstance method, 363, 368–369

proxy/ProxyTest.java, 366

public access modifier, 38, 52, 143–146, 187–188, 298

checking, 271

for fields in interfaces, 304

for main method, 39

for only one class in source file, 143

not specified for interfaces, 297

publish method

of Handler, 414, 422

of SwingWorker, 825–826, 831

Pure virtual functions (C++), 227

push method (Stack), 559

put method

of BlockingQueue, 782–783, 788

of ConcurrentHashMap, 791

of Map, 492, 520, 522

of Preferences, 625, 630

putAll method (Map), 522

putDataType methods (Preferences), 625, 630

putFirst/Last methods (BlockingDeque), 788

putIfAbsent method

of ConcurrentHashMap, 791

of Map, 524

putValue method (Action), 608, 613

Q

Queue interface, 516–518

implementing, 483–485

methods of, 516–517

Queues, 482–485, 516–518

blocking, 781–788

concurrent, 789–790

double-ended. See Deques

QuickSort algorithm, 113, 544

R

\r (carriage return escape sequence), 46

Race conditions, 750–754

and atomic operations, 773

Radio buttons, 654–658

in menus, 676–677

radioButton/RadioButtonFrame.java, 656

Ragged arrays, 120–123

Random class, 180

nextInt method, 180

thread-safe, 778

RandomAccess interface, 494, 544, 547

range method (EnumSet), 531

Raw types, 441–442

converting type parameters to, 458

type inquiring at runtime, 447

readConfiguration method (LogManager), 408, 425

readLine/Password methods (Console), 78

Rectangle class, 513, 582

Rectangle2D class, 580–583

Rectangle2D.Double class, 581, 587

Rectangle2D.Float class, 581

Rectangles, 580

comparing, 513

drawing, 580

filling with color, 588

RectangularShape class, 582

getCenterX/Y methods, 582, 586

getHeight/Width methods, 582, 587

getMaxX/Y, getMinX/Y methods, 586

getX/Y methods, 587

Recursive computations, 812

RecursiveAction, RecursiveTask classes, 812

Red-black trees, 512

redirectXxx methods (ProcessBuilder), 833, 836

reduce, reduceXxx methods (ConcurrentHashMap), 794–796

Redundant keywords, 304

Reentrant locks, 756

ReentrantLock class, 755–758

Reflection, 208, 264–290

accessing nonpublic features with, 278

analyzing:

classes, 271–277

objects, at runtime, 277–283

generics and, 283–286, 467–479

overusing, 293

reflection/ReflectionTest.java, 273

Reinhold, Mark, 12

Relational operators, 59, 61

Relative resource names, 269

remove method

of ArrayList, 253–254

of BlockingQueue, 782–783

of Collection, 489, 491

of Iterator, 485, 487–488, 492

of JMenu, 674

of List, 492, 505

of ListIterator, 501

of Map, 520

of Queue, 517

of ThreadLocal, 779

removeAll method

of Collection, 489, 491

of LinkedList, 503

removeEldestEntry method (LinkedHashMap), 528, 531

removeFirst/Last methods

of Deque, 517

of LinkedList, 506

removeHandler method (Logger), 422

removeIf method

of ArrayList, 328

of Collection, 491, 549

removeLayoutComponent method (LayoutManager), 706

removePropertyChangeListener method (Action), 608–609

removeXxx methods (JComboBox), 662, 664

repaint method

of Component, 576

of JComponent, 579

repeat method (String), 63, 70

REPL (read-evaluate-print loop), 32

replace method

of ConcurrentHashMap, 791

of String, 70

replaceAll method

of Collections, 548

of List, 549

of Map, 524

requireNonNull, requireNonNullElse methods (Objects), 149, 163

Reserved words, 38

forbidden for variable names, 49

not used, 52

resetChoosableFilters method (JFileChooser), 727, 731

Resource bundles, 409–410

ResourceBundle class, 410

Resources, 268–271

exhaustion of, 374

localization of, 269

names of, 269

resources/ResourceTest.java, 270

Restricted views, 537

resume method (Thread), 743

retain method (Collection), 489

retainAll method (Collection), 491

Retirement/Retirement.java, 93

Retirement2/Retirement2.java, 94

return statement

in finally blocks, 388

in lambda expressions, 324

@return comment (javadoc), 200

Return types, 219

covariant, 445

documentation comments for, 200

for overridden methods, 443

Return values, 134

revalidate method (JComponent), 644–645

reverse method (Collections), 548

reversed, reverseOrder methods (Comparator), 340, 543, 546

rotate method (Collections), 549

round method (Math), 57

RoundingMode class, 107

rt.jar file, 192

run method (Thread), 736, 739

runAfterXxx methods (CompletableFuture), 819–820

runFinalizersOnExit method (System), 180

Runnable interface, 337, 734

lambdas and, 326

run method, 336, 739

Runtime

adding shutdown hooks at, 180

analyzing objects at, 277–283

creating classes at, 363

exec method, 832

setting the size of an array at, 248

type identification at, 224, 264, 447

RuntimeException, 374, 394, 397

@SafeVarargs annotation, 449

S

Scala programming language, default methods in, 308

Scanner class, 75–78, 83–85

hasNext method, 77

hasNextXxx methods, 77–78

next method, 77

nextXxx methods, 76–77

Scheduled execution, 804

ScheduledExecutorService class, methods of, 805

Scroll panes, 647–651

search, searchXxx methods (ConcurrentHashMap), 794–796

Security, 5, 15

@see comment (javadoc), 201–202

Semantic events, 621–622

Serialization, 530

Service loaders, 360–362

ServiceLoader class, 360

iterator, load methods, 362

stream method, 361–362

ServiceLoader.Provider interface, methods of, 361–362

Services, 360–362

ServletException, 384

Servlets, 384

Set interface

add, equals, hashCode, methods of, 494

of method, 532–533, 538, 540

set method

of Array, 286

of ArrayList, 251, 254

of BitSet, 560

of Field, 283

of List, 492, 505

of ListIterator, 501, 506

of ThreadLocal, 779

of Vector, 769

set/SetTest.java, 510

setAccelerator method (JMenuItem), 680–681

setAcceptAllFileFilterUsed method (JFileChooser), 726, 730

setAccessible method (AccessibleObject), 278, 282

setAccessory method (JFileChooser), 731

setAction method (AbstractButton), 674

setActionCommand method (AbstractButton), 658

setBackground method (Component), 588–589

setBoolean, setByte, setChar methods (Array), 286

setBorder method (JComponent), 659, 661

setBounds method (Component), 570, 573

coordinates in, 572

setCharAt method (StringBuilder), 75

setClassAssertionStatus method (ClassLoader), 403

setColumns method

of JTextArea, 647, 650

of JTextField, 644–645

setComponentPopupMenu method (JComponent), 678–679

setCurrentDirectory method (JFileChooser), 724, 730

setCursor method (Component), 620

setDaemon method (Thread), 746–747

setDefaultAssertionStatus method (ClassLoader), 403

setDefaultButton method (JRootPane), 718, 723

setDefaultCloseOperation method (JDialog), 714

setDefaultUncaughtExceptionHandler method (Thread), 428, 747–748

setDisplayedMnemonicIndex method (AbstractButton), 680–681

setDouble method (Array), 286

setEchoChar method (JPasswordField), 647

setEditable method

of JComboBox, 662, 664

of JTextComponent, 643

setEnabled method

of Action, 608, 613

of JMenuItem, 682–683

setFileFilter method (JFileChooser), 726, 730

setFileSelectionMode method (JFileChooser), 725, 730

setFileView method (JFileChooser), 727–728, 731

setFilter method

of Handler, 423

of Logger, 415, 422

setFloat method (Array), 286

setFont method (JComponent), 645

setForeground method (Component), 588–589

setFormatter method (Handler), 415, 423

setFrameFromCenter method (Ellipse2D), 583

setHorizontalTextPosition method (AbstractButton), 675

setIcon method

of JLabel, 646

of JMenuItem, 675

setIconImage method (Frame), 570, 574

setInheritsPopupMenu method (JComponent), 678–679

setInt method (Array), 286

setInverted method (JSlider), 667

setJMenuBar method (JFrame), 672, 674

setLabelTable method (JSlider), 445, 667, 671

setLayout method (Container), 639

setLevel method

of Handler, 423

of Logger, 404, 422

setLineWrap method (JTextArea), 648, 650

setLocation method (Component), 570, 573

coordinates in, 572

setLocationByPlatform method (Window), 573

setLong method (Array), 286

setMnemonic method (AbstractButton), 680–681

setModel method (JComboBox), 662

setMultiSelectionEnabled method (JFileChooser), 725, 730

setOut method (System), 158

setPackageAssertionStatus method (ClassLoader), 403

setPaint method (Graphics2D), 587–589

setPaintLabels method (JSlider), 666, 671

setPaintTicks method (JSlider), 666–667, 671

setPaintTrack method (JSlider), 671

setParent method (Logger), 422

setPriority method (Thread), 749

setProperty method

of Properties, 557

of System, 408

setResizable method (Frame), 570, 573

setRows method (JTextArea), 647, 650

Sets, 509

concurrent, 789–790

intersecting, 549

mutating elements of, 510

subranges of, 534

thread-safe, 796–797

with given elements, 532

setSelected method

of AbstractButton, 677

of JCheckBox, 652, 654

setSelectedFile/Files methods (JFileChooser), 725, 730

setShort method (Array), 286

setSize method (Component), 573

setSnapToTicks method (JSlider), 666, 671

setTabSize method (JTextArea), 651

setText method

of JLabel, 646

of JTextComponent, 643–644

setTime method (Calendar), 222

setTitle method (JFrame), 570, 573

setToolTipText method (JComponent), 690

setUncaughtExceptionHandler method (Thread), 748

setUseParentHandlers method (Logger), 422

setValue method (Map.Entry), 526

setVisible method

of Component, 570, 573

of JDialog, 714, 716–717

setWrapStyleWord method (JTextArea), 651

setXxxTickSpacing methods (JSlider), 671

severe method (Logger), 406, 421

Shallow copies, 316–318

Shape interface, 580

Shell

redirection syntax of, 85

scripts in, 191

Shift operators, 60

short type, 43

Short class

converting from short, 256

hashCode method, 241

show method (JPopupMenu), 678

showConfirmDialog method (JOptionPane), 707–711

showDialog method (JFileChooser), 718, 725, 730

showInputDialog method (JOptionPane), 707–709, 712

showInternalConfirmDialog method (JOptionPane), 711

showInternalInputDialog method (JOptionPane), 712

showInternalMessageDialog method (JOptionPane), 710

showInternalOptionDialog method (JOptionPane), 711

showMessageDialog method (JOptionPane), 312, 707–710

showOptionDialog method (JOptionPane), 707–709, 711

showXxxDialog methods (JFileChooser), 718, 723, 725, 730

shuffle method (Collections), 544–545

shuffle/ShuffleTest.java, 545

Shuffling, 544

Shutdown hooks, 180

shutdown method (ExecutorService), 804–805

shutdownNow method (ExecutorService), 804, 806

Sieve of Eratosthenes benchmark, 560–563

sieve/sieve.cpp, 562

sieve/Sieve.java, 561

signal method (Condition), 761–764, 775

signalAll method (Condition), 760–764, 775

Signatures (of methods), 171, 219

simpleframe/SimpleFrameTest.java, 568

sin method (Math), 54

singleton, singletonXxx methods (Collections), 533, 540

size method

of ArrayList, 250–251

of Collection, 489–490

of concurrent collections, 789

sleep method (Thread), 735, 739, 744

slider/SliderFrame.java, 667

Sliders, 665–671

ticks on, 666–667

vertical, 665

SoftBevelBorder class, 659–660

Software Development Kit (SDK), 19

Solaris operating system

Eclipse versions for, 29

JDK versions for, 18

sort method

of Arrays, 113–116, 297, 300, 302, 322, 326

of Collections, 543–546

of List, 545

SortedMap interface, 494

comparator, first/lastKey methods, 523

subMap, headMap, tailMap methods, 534, 541

SortedSet interface, 494, 534

comparator, first, last methods, 515

subSet, headSet, tailSet methods, 534, 540

Sorting

algorithms for, 113, 543–546

arrays, 113–116, 300

assertions for, 401

in reverse order, 543

people, by name, 339–340

strings by length, 314, 322–324

Source files, 191

editing in Eclipse, 31

installing, 22–23

Special characters, 46

Splash screen, 265

Spring layout, 691

sqrt method (Math), 54

of BigDecimal, BigInteger, 107

src.zip file, 22

Stack interface, 482, 552, 558

methods of, 559

Stack trace, 391–395, 775

StackFrame class getClassName method, 394

getDeclaringClass method, 394

getFileName method, 394

getLineNumber method, 394

getMethodName method, 395

isNativeMethod method, 395

toString method, 391, 395

Stacks, 558

stackTrace/StackTraceTest.java, 392

StackTraceElement class, methods of, 395

StackWalker class, 391

forEach method, 394

getInstance method, 391, 394

walk method, 391, 394

Standard Edition (Java SE), 12, 19

Standard Java library

companion classes in, 306

online API documentation for, 68, 71–73, 198, 203

Standard Template Library (STL), 482, 487

start method

of ProcessBuilder, 834, 837

of Thread, 736, 739–740

of Timer, 313

Starting directory, for a launched program, 84

startInstant method (ProcessHandle.Info), 838

startPipeline method (ProcessBuilder), 833, 837

startsWith method (String), 69

stateChanged method (ChangeListener), 666

Statements, 41

compound. See Blocks

static access modifier, 156–163

for fields in interfaces, 304

for main method, 40

Static binding, 220

Static constants, 157–158

documentation comments for, 201

Static fields, 156–157

accessing, in static methods, 158

importing, 183

initializing, 177

no type variables in, 452

static final access modifier, 51

Static imports, 183

Static inner classes, 341, 356–359

Static methods, 158–159

accessing static fields in, 158

adding to interfaces, 306

importing, 183

no type variables in, 452

Static variables, 157

staticInnerClass/StaticInnerClassTest.java, 358

StaticTest/StaticTest.java, 161

stop method

of Thread (deprecated), 743, 779–781

of Timer, 313

store method (Properties), 555, 557

stream method

of Collection, 308

of ServiceLoader, 361–362

Stream interface, toArray method, 332

StreamHandler class, 413–414

strictfp keyword, 53

StrictMath class, 54–55

String class, 62–75

blank method, 69

charAt method, 67–68

codePointAt, codePoints methods, 69

codePointCount method, 67, 70

compareTo method, 69

empty method, 69

endsWith method, 69

equals, equalsIgnoreCase methods, 65, 69

format, formatTo methods, 80

hashCode method, 238, 507

immutability of, 63, 155, 222

indexOf method, 69, 171

join method, 70

lastIndexOf method, 70

length method, 66–67, 70

offsetByCodePoints method, 67, 69

repeat method, 63, 70

replace method, 70

startsWith method, 69

strip method, 70

substring method, 62, 70, 534

toLowerCase, toUpperCase methods, 70

trim method, 70, 644

StringBuilder class, 74–75

append method, 74–75

appendCodePoint method, 75

delete method, 75

insert method, 75

length method, 74

setCharAt method, 75

toString method, 74–75

Strings, 62–75

building, 74–75

code points/code units of, 66

comparing, 314

concatenating, 63

with objects, 242

converting to numbers, 258

empty, 66, 69

equality of, 65

formatting output for, 78–83

immutability of, 63

length of, 62, 66

null, 66

shared, in compiler, 64–65

sorting by length, 314, 322–324

substrings of, 62

using ". . ." for, 41

strip method (String), 70

Strongly typed languages, 42, 299

Subclasses, 208–232

adding fields/methods to, 211

anonymous, 354, 433

cloning, 319

comparing objects from, 303

constructors for, 211

defining, 208

method visibility in, 221

no access to private fields of superclass, 231

overriding superclass methods in, 211

subList method (List), 534, 540

subMap method

of NavigableMap, 541

of SortedMap, 534, 541

Submenus, 671–672

submit method

of ExecutorCompletionService, 811

of ExecutorService, 803–805

Subranges, 534

subSet method

of NavigableSet, 534, 541

of SortedSet, 534, 540

Substitution principle, 217

substring method (String), 62, 70, 534

subtract method (BigDecimal/BigInteger), 107

subtractExact method (Math), 55

Subtraction operator, 52

sum method (LongAdder), 774

Sun Microsystems, 2, 5–12, 14, 566

HotJava browser, 11

super keyword, 210, 461

in method references, 330

vs. this, 211–212

Superclass wins rule, 308

Superclasses, 208–232

accessing private fields of, 210

common fields and methods in, 227, 290

overriding methods of, 237

throws specifiers in, 378, 383

Supertype bounds, 461–464

Supplementary characters, 47

Supplier interface, 337

supportsNormalTermination method (Process), 837

@SuppressWarnings annotation, 101, 256, 446, 449, 454–455

Surrogates area (Unicode), 47

suspend method (Thread, deprecated), 743, 779–781

swap method (Collections), 548

Swing toolkit, 565–630, 824

building GUI with, 631–732

model-view-controller analysis of, 634, 636

starting, 569

SwingConstants interface, 304, 646

SwingUtilities class, getAncestorOfClass method, 718, 723

SwingWorker class, 824

doInBackground method, 825–826, 831

execute method, 826, 831

getState method, 831

process method, 825–827, 831

publish method, 825–826, 831

swingWorker/SwingWorkerTest.java, 827

switch statement, 99–101

enumerated constants in, 101

synch/Bank.java, 762

synch2/Bank.java, 766

Synchronization, 750–781

condition objects, 758–764

final variables, 772

in Vector, 507

lock objects, 755–758

monitor concept, 770–771

race conditions, 750–754, 773

volatile fields, 771–772

Synchronization wrappers, 799–800

Synchronized blocks, 768–770

synchronized keyword, 755, 764–770

Synchronized views, 536

synchronizedCollection methods (Collections), 536, 539, 800

System class

console method, 78

exit method, 40

getProperties method, 556, 558

getProperty method, 84, 558

identityHashCode method, 530, 532

runFinalizersOnExit method, 180

setOut method, 158

setProperty method, 408

System.err class, 427

System.in class, 75

System.out class, 41, 157, 427

print method, 78

printf method, 79–83, 260

println method, 75, 403

systemNodeForPackage, systemRoot methods (Preferences), 625, 629

T

T type variable, 435

\t (tab escape sequence), 46

Tab completion, 34

Tagging interfaces, 317, 442, 494

tailMap method

of NavigableMap, 541

of SortedMap, 534, 541

tailSet method

of NavigableSet, 534, 541

of SortedSet, 534, 540

take method

of BlockingQueue, 782–783, 788

of ExecutorCompletionService, 811

takeFirst/Last methods (BlockingDeque), 788

tan method (Math), 54

tar command, 192

Tasks

controlling groups of, 806–811

decoupling from mechanism of running, 736

long-running, 823–831

multiple, 733

running asynchronously, 800

scheduled, 804

work stealing for, 813

Template code bloat, 442

Terminal window, 25

Text

centering, 591

displaying, 577

fonts for, 589–596

typesetting properties of, 591

Text areas, 647–648

formatted text in, 649

preferred size of, 648

Text fields, 643–645

columns in, 643

creating blank, 644

preferred size of, 643

Text input, 643–651

labels for, 645–646

password fields, 647

scroll panes, 647

text/TextComponentFrame.java, 649

thenAccept, thenAcceptBoth, thenCombine methods (CompletableFuture), 819

thenAccept, thenAcceptBoth, thenCombine, thenRun methods (CompletableFuture), 819

thenApply, thenApplyAsync methods (CompletableFuture), 817, 819

thenComparing method (Comparator), 339–340

thenCompose method (CompletableFuture), 818–819

this keyword, 150, 174

in first statement of constructor, 175

in inner classes, 346

in lambda expressions, 335

in method references, 330

vs. super, 211–212

Thread class

currentThread method, 743–746

extending, 736

get/setUncaughtExceptionHandler methods, 748

getDefaultUncaughtExceptionHandler method, 748

getState method, 743

interrupt, isInterrupted methods, 743–746

interrupted method, 745–746

join method, 741–743

methods with timeout, 741

resumes method, 743

run method, 736, 739

setDaemon method, 746–747

setDefaultUncaughtExceptionHandler method, 428, 747–748

setPriority method, 749

sleep method, 735, 739, 744

start method, 736, 739–740

stop method (deprecated), 743, 779–781

suspend method (deprecated), 743, 779–781

yield method, 741

Thread dump, 775

Thread groups, 748

Thread pools, 800–805

of fixed size, 802

Thread.UncaughtExceptionHandler interface, 747–749

ThreadDeath error, 742, 749, 780

ThreadGroup class, 748

uncaughtException method, 748–749

ThreadLocal class, methods of, 779

ThreadLocalRandom class, current method, 779

ThreadPoolExecutor class, 802, 804

getLargestPoolSize method, 805

Threads

accessing collections from, 536, 781–800

blocked, 741–742, 744

condition objects for, 758–764

daemon, 746

defined, 734–739

executing code in, 336

idle, 811

interrupting, 743–746

listing all, 775

locking, 768–770

new, 740

preemptive vs. cooperative scheduling for, 740

priorities of, 749

producer/customer, 781

runnable, 740–741

states of, 739–743

synchronizing, 750–781

terminated, 735, 742–743

thread-local variables in, 778–779

timed waiting, 741–742

unblocking, 761

uncaught exceptions in, 747–749

vs. processes, 734

waiting, 741–742, 760

work stealing for, 813

worker, 823–831

threads/Bank.java, 738

threads/ThreadTest.java, 736

Thread-safe collections, 781–800

callables and futures, 800–802

concurrent, 789–790

copy on write arrays, 797

synchronization wrappers, 799–800

throw keyword, 378–379

Throwable class, 374, 397

add/getSuppressed methods, 390, 393

get/initCause methods, 393

getMessage method, 380

getStackTrace method, 391, 393

printStackTrace method, 267, 391, 427

toString method, 380

throwing method (Logger), 407, 421

throws keyword, 268, 375–378

for main method, 85

@throws comment (javadoc), 200

Ticks, 666

icons for, 667

labeling, 666

snapping to, 666

Time measurement vs. calendars, 136

Timed waiting threads, 741–742

TimeoutException, 801

Timer class, 310, 322, 622

start, stop methods, 313

timer/TimerTest.java, 312

toArray method

of ArrayList, 452

of Collection, 252, 489, 491

of Stream, 332

toHandle method (Process), 835, 837

toLowerCase method (String), 70

Toolbars, 687–689

detaching, 688

dragging, 687

title of, 689

vertical, 689

Toolkit class

beep method, 313

getDefaultToolkit method, 313, 572, 574

getScreenSize method, 572, 574

Tooltips, 689–690

toString method

adding to all classes, 243

Formattable and, 80

of Arrays, 111, 116

of Date, 133

of Enum, 262–263

of Integer, 259

of Modifier, 271, 276

of Object, 241–247, 310

of proxy classes, 368

of StackFrame, 391, 395

of StackTraceElement, 395

of StringBuilder, 74–75

of Throwable, 380

redeclaring, 326

working with any class, 279

Total ordering, 513

totalCpuDuration method (ProcessHandle.Info), 838

toUnsignedInt method (Byte), 44

toUpperCase method (String), 70

TraceHandler class, 364

Tracing execution flow, 406

TransferQueue interface, 783

transfer, tryTransfer methods, 788

translatePoint method (MouseEvent), 623

Tree maps, 520

Tree sets, 511–516

adding elements to, 512

red-black, 512

total ordering of, 513

vs. priority queues, 518

TreeMap class, 494, 519, 523

as a concrete collection type, 495

vs. HashMap, 520

TreeSet class, 494, 511–516

as a concrete collection type, 495

treeSet/Item.java, 514

treeSet/TreeSetTest.java, 513

Trigonometric functions, 54

trim method (String), 70, 644

trimToSize method (ArrayList), 250–251

Troubleshooting. See Debugging

Truncated computations, 53

try/catch statement, 381–386

generics and, 453

wrapping entire task in try block, 397

try/finally statement, 386–389

tryLock method (Lock), 741

trySetAccessible method (AccessibleObject), 282

try-with-resources statement, 389–391

effectively final variables in, 390

no locks with, 755

Two-dimensional arrays, 116–121

Type erasure, 441–447

clashes after, 455–456

Type interface, 470

type method (ServiceLoader.Provider), 361–362

Type parameters, 248

converting to raw types, 458

not for arrays, 448, 458

not instantiated with primitive types, 447

vs. inheritance, 432

Type variables

bounds for, 438–441

in exceptions, 453

in static fields or methods, 452

matching in generic methods, 469

names of, 435

no instantiating for, 450

replacing with bound types, 441–442

Typesetting terms, 592

TypeVariable interface, 470

getBounds, getName methods, 478

U

UCSD Pascal system, 6

UML (Unified Modeling Language) notation, 130–131

UnaryOperator interface, 337

uncaughtException method (ThreadGroup), 748–749

UncaughtExceptionHandler interface, 747–749

uncaughtException method, 748

Unchecked exceptions, 268, 375–377

applicability of, 397

Unequality operator, 59

Unicode standard, 6, 47–48, 62

in char type, 46

Unit testing, 160

University of Illinois, 11

UNIX operating system Eclipse versions for, 29

setting paths in, 20, 189–191

setting up JDK in, 20

troubleshooting Java programs in, 26

unlock method (Lock), 755, 758

Unmodifiable views, 534–536

unmodifiableCollection methods (Collections), 535–536, 539

Unnamed modules, 278

Unnamed packages, 184, 187, 203, 400

UnsupportedOperationException, 526, 533, 535, 537, 539

unsynch/UnsynchBankTest.java, 752

updateAndGet method (AtomicType), 773

updateConfiguration method (LogManager), 408, 425

user method (ProcessHandle.Info), 838

User input, 644

errors in, 373

User Interface. See Graphical User Interface

userNodeForPackage, userRoot methods (Preferences), 625, 629

「Uses–a」relationship, 129–131

UTC (Coordinated Universal Time), 136

UTF-8 standard, 84

Utility classes/methods, 306–307

V

V type variable, 435

validate method (Component), 645

valueOf method

of BigDecimal, BigInteger, 105–107

of Enum, 262–263

of Integer, 259

values method (Map), 525–526

Values, captured by lambda expressions, 334

Varargs, 260–261

passing generic types to, 448–449

VarHandle class, 279

Variable handles, 279

Variables, 48–50

accessing in lambdas, 333–335

annotating, 446

copying, 314

declarations of, 48

effectively final, 335, 390

final, accessing from outer methods, 350–351

initializing, 50, 204

local, 446

mutating in lambda expressions, 334

names of, 48–50

package scope of, 187

printing/logging values of, 426

static, 157

thread-local, 778–779

Vector class, 482, 552–553, 769, 799–800

for dynamic arrays, 249

get, set methods, 769

synchronization in, 507

@version comment (javadoc), 201, 203

Views, 532, 632

bulk operations for, 550

checked, 536

restricted, 537

subranges of, 534

synchronized, 536

unmodifiable, 534–536

Visual Basic programming language

built-in date type in, 132

event handling in, 598

syntax of, 3

Visual Studio, 23

void keyword, 40

Volatile fields, 771–772

volatile keyword, 771–773

von der Ahé, Peter, 438

W

wait method (Object), 741, 765, 768

Wait sets, 760

waitFor method (Process), 834, 837

walk method (StackWalker), 391, 394

warning method (Logger), 406, 421

Warnings

fallthrough behavior, 101

generic types, 256, 446, 449, 454–455

suppressing, 449, 454–455

when using reflection, 278

Weak hash maps, 526–527

Weak references, 527

WeakHashMap class, 526–527, 530

as a concrete collection type, 495

Weakly consistent iterators, 789

WeakReference object, 527

Web pages

dynamic, 9

extracting links from, 817

reading, 818, 824

Welcome/Welcome.java, 25

whenComplete method (CompletableFuture), 819

while loop, 91–95

Whitespace, irrelevant to compiler, 40

Wildcard types, 434, 459–467

arrays of, 448

capturing, 465–467

supertype bounds for, 461–464

unbounded, 464

WildcardType interface, 470

getLowerBounds, getUpperBounds methods, 479

Window class, 623

pack method, 577, 579

setLocationByPlatform method, 573

Window listeners, 605–607

WindowClosing event, 681

WindowEvent class, 598, 606, 622

getNewState, getOldState methods, 624

getWindow, getOppositeWindow, getScrollAmount methods, 623

WindowFocusListener interface, methods of, 624

WindowListener interface, methods of, 606–607, 623

Windows. See Dialogs

Windows operating system

Alt+F4 keyboard shortcut in, 681

default location in, 411

Eclipse versions for, 29

executing JARs in, 195

JDK versions for, 18

pop-up menus in, 678

registry in, 624, 626

setting paths in, 20–22, 189, 191

setting up JDK in, 20

thread priority levels in, 749

WindowStateListener interface, windowStateChanged method, 607, 624

Wirth, Niklaus, 6, 10, 126

withInitial method (ThreadLocal), 779

Work stealing, 813

Worker threads, 823–831

Working directory, for a process, 832

Wrappers, 256–260

equality testing for, 257

immutability of, 256

X

XML (Extensible Markup Language), 12, 14

xor method (BitSet), 560

Y

yield method (Thread), 741

Z

ZIP format, 189, 192

Credits

Chapter 1:「As a computer language . . . existing code sets in」」, Cay S. Horstmann.

Chapter 1:「Simple, Object-Oriented . . . Dynamic」,「The Java Language Environment: Contents, A White Paper, May 1996, James Gosling, Henry McGilton.

Chapter 1:「Simple We wanted to build a . . . very good job making it manageable」, Java: an Overview, James Gosling, February 1995.

Chapter 1, Figure 1.1: Screenshot of Jmol © Jmol.

Chapter 1:「All along, the language was a tool, not the end.」Interview with Java's creators in the July 1995 issue of SunWorld's online magazine.

Chapter 1:「We could build a real . . . we built a browser」. Interview with Java's creators in the July 1995 issue of SunWorld's online magazine.

Chapter 2, Figure 2.1: Screenshot of Windows 10 © Microsoft 2018.

Chapter 2, Figure 2.2: Screenshot of Windows 10 © Microsoft 2018.

Chapter 2, Figure 2.5: Screenshot of Eclipse © Eclipse Foundation.

Chapter 2, Figure 2.6: Screenshot of Eclipse © Eclipse Foundation.

Chapter 2, Figure 2.7: Screenshot of Eclipse © Eclipse Foundation.

Chapter 2, Figure 2.8: Screenshot of Eclipse © Eclipse Foundation.

Chapter 2, Figure 2.9: Screenshot of Jshell © Oracle Corporation.

Chapter 3, Figure 3.2: Screenshot of Java © Oracle Corporation.

Chapter 3, Figure 3.3: Screenshot of Java © Oracle Corporation.

Chapter 3, Figure 3.4: Screenshot of Java © Oracle Corporation.

Chapter 3, Figure 3.5: Screenshot of Java © Oracle Corporation.

Chapter 4, Figure 4.2: Screenshot of Java © Oracle Corporation.

Chapter 4, Figure 4.11: Screenshot of Java © Oracle Corporation.

Chapter 5, Figure 5.3: Screenshot of Java © Oracle Corporation.

Chapter 7, Figure 7.3: Screenshot of Java © Oracle Corporation.

Chapter 10, Figure 10.1: Screenshot of Java © Oracle Corporation.

Chapter 10, Figure 10.3: Screenshot of Java © Oracle Corporation.

Chapter 10, Figure 10.8: Screenshot of Java © Oracle Corporation.

Chapter 10, Figure 10.11: Screenshot of Java © Oracle Corporation.

Chapter 10, Figure 10.14: Screenshot of Java © Oracle Corporation.

Chapter 10, Figure 10.15: Screenshot of Java © Oracle Corporation.

Chapter 10, Figure 10.16: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.4: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.5: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.8: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.9: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.10: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.11: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.12: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.13: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.14: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.15: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.16: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.17: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.18: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.19: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.20: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.21: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.22: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.23: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.24: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.25: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.26: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.27: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.29: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.30: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.31: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.32: Screenshot of Java © Oracle Corporation.

Chapter 11, Figure 11.34: Screenshot of Java © Oracle Corporation.

Chapter 12:「It is astounding . . . has no merit」, Java's Insecure Parallelism, ACM SIGPLAN Notices 34:38–45, April 1999.

Chapter 12, Figure 12.5: Screenshot of Java © Oracle Corporation.

Chapter 12, Figure 12.6: Screenshot of Java © Oracle Corporation. Page 902: Photo by izusek/gettyimages.

Code Snippets

Many titles include programming code or configuration examples. To optimize the presentation of these elements, view the eBook in single-column, landscape mode and adjust the font size to the smallest setting. In addition to presenting code and configurations in the reflowable text format, we have included images of the code that mimic the presentation found in the print book; therefore, where the reflowable format may compromise the presentation of the code listing, you will see a「Click here to view code image」link. Click the link to view the print-fidelity code image. To return to the previous page viewed, click the Back button on your device or app.

