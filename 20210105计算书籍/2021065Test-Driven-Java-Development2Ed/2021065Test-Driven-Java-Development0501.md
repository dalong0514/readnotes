– Leonardo da Vinci

In the past, the software industry was focused on developing software at high speed, with nothing in mind but cost and time. Quality was a secondary goal, with the false feeling that customers were not interested in it.

Nowadays, with the increasing connectivity of all kinds of platforms and devices, quality has become a first-class citizen in customer's requirements. Good applications offer a good service with a reasonable response-time, without being affected by a multitude of concurrent requests from many users.

Good applications in terms of quality are those that have been well designed. A good design means scalability, security, maintainability, and many other desired attributes.

In this chapter, we will explore how TDD leads developers to good design and best practices by implementing the same application using both the traditional and TDD

approaches.

The following topics will be covered in this chapter:

Why should we care about design?

Design considerations and principles

The traditional development process

The TDD approach using Hamcrest

Design – If It's Not Testable, It's Not Designed Well Chapter 5

Why should we care about design?

In software development, whether you are an expert or a beginner, there are some situations where code seems to be unnatural. You can't avoid the feeling that something is wrong with that code when reading it. Occasionally, you even wonder why the previous programmer implemented a specific method or a class in such a twisted manner. This is because the same functionality can be implemented in a vast number of different ways, each of them unique. With this huge number of possibilities, which is the best one? What defines a good solution? Why is one better than the others? The fact is, all of them are valid so long as the goal is achieved. However, it is true that some aspects should be considered when choosing the right solution. This is where the design of the solution becomes relevant.

Design principles

A software design principle is a rule or set of rules that work as a guide for software developers and push them towards smart and maintainable solutions. In other words, design principles are conditions that code must fulfill to be considered objectively well designed.

Most senior developers and experienced programmers know about software design principles and it's very likely that, independently of whether they practice TDD, they are applying them to their daily work. The TDD philosophy encourages programmers—even beginners—to follow some principles and good practices that make code cleaner and more readable. Those practices are enforced by the Red-Green-Refactor cycle.

The Red-Green-Refactor cycle advocates for small feature increments by introducing one test that fails at a time. Programmers add code fragments, as concise and short as possible, so neither the new test or the old ones do not fail anymore. And ultimately, they refactor the code, which consists of cleanup and improvement tasks such as duplication removal or code optimization.

As a result of the process, the code becomes easier to understand and safer to modify in the future. Let's take a look at some of the most popular software design principles.

You Ain't Gonna Need It

YAGNI is the acronym for the You Ain't Gonna Need It principle. It aims to erase all unnecessary code and focuses on the current functionalities, not the future ones. The less code you have, the less code you're going to maintain and the lower the probability that bugs will be introduced.

[ 114 ]

Design – If It's Not Testable, It's Not Designed Well Chapter 5

For more information on YAGNI, visit Martin Fowler's article available

at http://martinfowler.com/bliki/Yagni.html.

Don't Repeat Yourself

The idea behind the Don't Repeat Yourself (DRY) principle is to reuse the code you previously wrote instead of repeating it. The benefits are less code to maintain and the use of code that you know that already works, which is a great thing. It helps you to discover new abstraction levels inside your code.

For additional information, visit

http://en.wikipedia.org/wiki/Don%27t_repeat_yourself.

Keep it simple, stupid

This principle has the confusing acronym of keep it simple, stupid (KISS) and states that things perform their function better if they are kept simple rather than complicated. It was coined by Kelly Johnson.

To read about the story behind this principle, visit

http://en.wikipedia.org/wiki/KISS_principle.

Occam's razor

Although Occam's razor is a philosophical principle, not a software engineering one, it is still applicable to what we do. It is very similar to the previous principle, with the main statement being as follows:

"When you have two competing solutions to the same problem, the simpler one is the better."

– William of Ockham

For more information on Occam's razor, visit

http://en.wikipedia.org/wiki/Occam%27s_razor.

[ 115 ]

Design – If It's Not Testable, It's Not Designed Well Chapter 5

SOLID principles

The word SOLID is an acronym invented by Robert C. Martin for the five basic principles of object-oriented programming. By following these five principles, a developer is more likely to create a great, durable, and maintainable application:

Single Responsibility Principle: A class should have only a single reason to change.

Open-Closed Principle: A class should be open for extension and closed for modification. This is attributed to Bertrand Meyer.

Liskov Substitution Principle: This was created by Barbara Liskov, and she says a class should be replaceable by others that extend that class.

Interface Segregation Principle: A few specific interfaces are preferable to one general-purpose interface.

Dependency Inversion Principle: A class should depend on abstraction instead of implementation. This means that class dependencies must be focused on what is done and forget about how it is done.

For further information on SOLID or other related principles,

visit http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod.

The first four principles are part of the core of TDD thinking, since they aim to simplify the code we write. The last one is focused on classes construction and dependency relationships in the application assembly process.

All of these principles are applicable and desirable in both test and non-test driven development, because, apart from other benefits, they make our code more maintainable.

The proper practical application of them is worth a whole book by itself. While we won't have time to go deep into it, we encourage you to investigate further.

In this chapter, we will see how TDD induces developers to put some of these principles into practice effortlessly. We will implement a small but fully functional version of the famous game Connect 4 with both the TDD and non-TDD approaches. Note that repetitive parts, such as Gradle project creation and so on, are omitted, as they are not considered relevant for the purpose of this chapter.

[ 116 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

Connect 4

Connect 4 is a popular, very easy-to-play board game. The rules are limited and simple.

Connect 4 is a two-player connection game in which the players first

choose a color and then take turns dropping colored discs from the top

into a seven column, six row, vertically suspended grid. The pieces fall straight down, occupying the next available space within the column. The objective of the game is to connect four of your own discs of the same

color next to one another vertically, horizontally, or diagonally, before your opponent connects four of theirs.

For further information on the game, visit Wikipedia

(http://en.wikipedia.org/wiki/Connect_Four).

Requirements

To code the two implementations of Connect 4, the game rules are transcribed as follows in the form of requirements. These requirements are the starting point for both the developments. We will go through the code with some explanations and compare both implementations at the end:

1. The board is composed of seven columns and six rows; all positions are empty.

2. Players introduce discs on the top of the columns. The introduced disc drops down the board if the column is empty. Future discs introduced in the same column will stack over the previous ones.

3. It is a two-person game, so there is one color for each player. One player uses red ( R) and the other one uses green ( G). Players alternate turns, inserting one disc every time.

4. We want feedback when either an event or an error occurs within the game. The output shows the status of the board after every move.

5. When no more discs can be inserted, the game finishes, and it is considered a draw.

6. If a player inserts a disc and connects more than three discs of his color in a straight vertical line, then that player wins.

7. The same happens in a horizontal line direction.

8. The same happens in a diagonal line direction.

[ 117 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

Test-last implementation of Connect 4

This is the traditional approach, focusing on problem-solving code rather than tests. Some people and companies forget about the value of automated testing and rely on users in what are called user acceptance tests.

This kind of user acceptance test consists of recreating real-world scenarios in a controlled environment, ideally identical to production. Some users perform a lot of different tasks to verify the correctness of the application. If any of these actions fail, then the code is not accepted, as it is breaking some functionality or it is not working as expected.

Moreover, a great number of these companies also use unit testing as a way to perform early regression checks. These unit tests are created after the development process and they try to cover as much code as possible. Last of all, code coverage analysis is executed to get a trace of what is actually covered by those unit tests. These companies follow a single rule of thumb: the bigger the code coverage, the better the quality delivered.

The main problem of this approach is that writing tests afterwards does nothing but demonstrates that the code behaves the way it has been programmed, which is not necessarily the way code is expected to behave. Also, focusing on code coverage leads to bad tests that turn our production code into immutable entities. Every modification we may want to add may cause several tests from different, unrelated parts of the code to fail. That fact means the cost of introducing changes becomes really high and performing any slight modification could end up being a nightmare and very expensive.

To demonstrate some points described earlier, let's implement the Connect 4 game using a TDD and not-TDD approach. The relevant code for each of the identified requirements is presented as we proceed further. This code isn't written incrementally, so some code snippets might contain a few code lines unrelated to the mentioned requirement.

Requirement 1 – the game's board

Let us start with the first requirement.

The board is composed of seven horizontal and six vertical empty positions.

[ 118 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

The implementation of this requirement is pretty straightforward. We just need the representation of an empty position and the data structure to hold the game. Note that the colors used by the players are also defined:

public class Connect4 {

public enum Color {

RED('R'), GREEN('G'), EMPTY(' ');

private final char value;

Color(char value) { this.value = value; }

@Override

public String toString() {

return String.valueOf(value);

}

}

public static final int COLUMNS = 7;

public static final int ROWS = 6;

private Color[][] board = new Color[COLUMNS][ROWS];

public Connect4() {

for (Color[] column : board) {

Arrays.fill(column, Color.EMPTY);

}

}

}

Requirement 2 – introducing discs

This requirement introduces part of the logic of the game.

Players introduce discs on the top of the columns. The introduced disc

drops down the board if the column is empty. Future discs introduced in the same column will stack over the previous ones.

[ 119 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

In this part, board bounds become relevant. We need to mark what positions are already taken, using Color.RED to indicate them. Finally, the first private method is created. It is a helper method that calculates the number of discs introduced in a given column: public void putDisc(int column) {

if (column > 0 && column <= COLUMNS) {

int numOfDiscs = getNumberOfDiscsInColumn(column - 1);

if (numOfDiscs < ROWS) {

board[column - 1][numOfDiscs] = Color.RED;

}

}

}

private int getNumberOfDiscsInColumn(int column) {

if (column >= 0 && column < COLUMNS) {

int row;

for (row = 0; row < ROWS; row++) {

if (Color.EMPTY == board[column][row]) {

return row;

}

}

return row;

}

return -1;

}

Requirement 3 – player shifts

More game logic is introduced with this requirement.

It is a two-person game, so there is one colour for each player. One player uses red ( R) and the other one uses green ( G). Players alternate turns, inserting one disc every time.

We need to save the current player to determine which player is playing this turn. We also need a function to switch the players to recreate the logic of turns. Some lines of code become relevant in the putDisc function. Specifically, the board position assignment is made using the current player, and it is switched after every move, as the game rules say:

...

private Color currentPlayer = Color.RED;

private void switchPlayer() {

[ 120 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

if (Color.RED == currentPlayer) {

currentPlayer = Color.GREEN;

} else {

currentPlayer = Color.RED;

}

}

public void putDisc(int column) {

if (column > 0 && column <= COLUMNS) {

int numOfDiscs = getNumberOfDiscsInColumn(column - 1);

if (numOfDiscs < ROWS) {

board[column - 1][numOfDiscs] = currentPlayer;

switchPlayer();

}

}

}

...

Requirement 4 – the game's output

A few outputs should be added to let the players know the current status of the game.

We want feedback when either an event or an error occurs within the

game. The output shows the status of the board after every move.

No output channel is specified. To make it easier, we decided to use the system standard output to print an event when it occurs. A few lines have been added on every action to let the user know about the status of the game:

...

private static final String DELIMITER = "|";

private void switchPlayer() {

if (Color.RED == currentPlayer) {

currentPlayer = Color.GREEN;

} else {

currentPlayer = Color.RED;

}

System.out.println("Current turn: " + currentPlayer);

}

public void printBoard() {

for (int row = ROWS - 1; row >= 0; --row) {

[ 121 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

StringJoiner stringJoiner =

new StringJoiner(DELIMITER, DELIMITER, DELIMITER);

for (int col = 0; col < COLUMNS; ++col) {

stringJoiner.add(board[col][row].toString());

}

System.out.println(stringJoiner.toString());

}

}

public void putDisc(int column) {

if (column > 0 && column <= COLUMNS) {

int numOfDiscs = getNumberOfDiscsInColumn(column - 1);

if (numOfDiscs < ROWS) {

board[column - 1][numOfDiscs] = currentPlayer;

printBoard();

switchPlayer();

} else {

System.out.println(numOfDiscs);

System.out.println("There's no room " +

"for a new disc in this column");

printBoard();

}

} else {

System.out.println("Column out of bounds");

printBoard();

}

}

...

Requirement 5 – win conditions (I)

The first game has a finished condition.

When no more discs can be inserted, the game finishes and it is considered a draw.

The following code shows one of the possible implementations:

...

public boolean isFinished() {

int numOfDiscs = 0;

for (int col = 0; col < COLUMNS; ++col) {

numOfDiscs += getNumberOfDiscsInColumn(col);

[ 122 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

}

if (numOfDiscs >= COLUMNS * ROWS) {

System.out.println("It's a draw");

return true;

}

return false;

}

...

Requirement 6 – win condition (II)

The first win condition.

If a player inserts a disc and connects more than three discs of his colour in a straight vertical line, then that player wins.

The checkWinCondition private method implements this rule by scanning whether or not the last move is a winning one:

...

private Color winner;

public static final int DISCS_FOR_WIN = 4;

public void putDisc(int column) {

...

if (numOfDiscs < ROWS) {

board[column - 1][numOfDiscs] = currentPlayer;

printBoard();

checkWinCondition(column - 1, numOfDiscs);

switchPlayer();

...

}

private void checkWinCondition(int col, int row) {

Pattern winPattern = Pattern.compile(".*" +

currentPlayer + "{" + DISCS_FOR_WIN + "}.*");

// Vertical check

StringJoiner stringJoiner = new StringJoiner("");

for (int auxRow = 0; auxRow < ROWS; ++auxRow) {

stringJoiner.add(board[col][auxRow].toString());

}

[ 123 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

if (winPattern.matcher(stringJoiner.toString()).matches()) {

winner = currentPlayer;

System.out.println(currentPlayer + " wins");

}

}

public boolean isFinished() {

if (winner != null) return true;

...

}

...

Requirement 7 – win condition (III)

This is the same win condition, but in a different direction.

If a player inserts a disc and connects more than three discs of his color in a straight horizontal line, then that player wins.

A few lines to implement this rule are as follows:

...

private void checkWinCondition(int col, int row) {

...

// Horizontal check

stringJoiner = new StringJoiner("");

for (int column = 0; column < COLUMNS; ++column) {

stringJoiner.add(board[column][row].toString());

}

if (winPattern.matcher(stringJoiner.toString()).matches()) {

winner = currentPlayer;

System.out.println(currentPlayer + " wins");

return;

}

...

}

...

[ 124 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

Requirement 8 – win condition (IV)

The last requirement is the last win condition. It is pretty similar to the last two; in this case, in a diagonal direction.

If a player inserts a disc and connects more than three discs of his color in a straight diagonal line, then that player wins.

This is a possible implementation for this last requirement. The code is very similar to the other win conditions because the same statement must be fulfilled:

...

private void checkWinCondition(int col, int row) {

...

// Diagonal checks

int startOffset = Math.min(col, row);

int column = col - startOffset, auxRow = row - startOffset;

stringJoiner = new StringJoiner("");

do {

stringJoiner.add(board[column++][auxRow++].toString());

} while (column < COLUMNS && auxRow < ROWS);

if (winPattern.matcher(stringJoiner.toString()).matches()) {

winner = currentPlayer;

System.out.println(currentPlayer + " wins");

return;

}

startOffset = Math.min(col, ROWS - 1 - row);

column = col - startOffset;

auxRow = row + startOffset;

stringJoiner = new StringJoiner("");

do {

stringJoiner.add(board[column++][auxRow--].toString());

} while (column < COLUMNS && auxRow >= 0);

if (winPattern.matcher(stringJoiner.toString()).matches()) {

winner = currentPlayer;

System.out.println(currentPlayer + " wins");

}

}

...

[ 125 ]

Design – If It's Not Testable, It's Not Designed Well Chapter 5

What we have got is a class with one constructor, three public methods, and three private methods. The logic of the application is distributed among all methods. The biggest flaw here is that this class is very difficult to maintain. The crucial methods, such as checkWinCondition, are non-trivial, with potential for bug entries in future modifications.

If you want to take a look at the full code, you can find it in the

https://bitbucket.org/vfarcic/tdd-java-ch05-design.git repository.

We made this small example to demonstrate the common problems with this approach.

Topics such as the SOLID principle requires a bigger project to become more illustrative.

In large projects with hundreds of classes, the problems become hours wasted in a sort of surgical development. Developers spend a lot of their time investigating tricky code and understanding how it works, instead of creating new features.

The TDD or test-first implementation

At this time, we know how TDD works—writing tests before, implementation after tests, and refactoring later on. We are going to pass through the process and only show the final result for each requirement. It is left to you to figure out the iterative Red-Green-Refactor process. Let's make this more interesting, if possible, by using a Hamcrest framework in our tests.

Hamcrest

As described in Chapter 2, Tools, Frameworks, and Environment, Hamcrest improves our test's readability. It makes assertions more semantic and comprehensive when complexity is reduced by using matchers. When a test fails, the error shown becomes more expressive by interpreting the matchers used in the assertion. A message could also be added by the developer.

The Hamcrest library is full of different matchers for different object types and collections.

Let's start coding and get a taste of it.

[ 126 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

Requirement 1 – the game's board

We will start with the first requirement.

The board is composed of seven horizontal and six vertical empty

positions.

There is no big challenge with this requirement. The board bounds are specified, but there's no described behavior in it; just the consideration of an empty board when the game starts.

That means zero discs when the game begins. However, this requirement must be taken into account later on.

This is how the test class looks for this requirement. There's a method to initialize the tested class to use a completely fresh object in each test. There's also the first test to verify that there's no disc when we start the game, meaning that all board positions are empty: public class Connect4TDDSpec {

private Connect4TDD tested;

@Before

public void beforeEachTest() {

tested = new Connect4TDD();

}

@Test

public void whenTheGameIsStartedTheBoardIsEmpty() {

assertThat(tested.getNumberOfDiscs(), is(0));

}

}

This is the TDD implementation of the previous specification. Observe the simplicity of the given solution for this first requirement; a simple method returning the result in a single line:

public class Connect4TDD {

public int getNumberOfDiscs() {

return 0;

}

}

[ 127 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

Requirement 2 – introducing discs

This is the implementation for the second requirement.

Players introduce discs on the top of the columns. An introduced disc

drops down the board if the column is empty. Future discs introduced in the same column will stack over the previous ones.

We can split this requirement into the following tests:

When a disc is inserted into an empty column, its position is 0

When a second disc is inserted into the same column, its position is 1

When a disc is inserted into the board, the total number of discs increases When a disc is put outside the boundaries, a Runtime Exception is thrown When a disc is inserted into a column and there's no room available for it, then a Runtime Exception is thrown

Also, these other tests are derived from the first requirement. They are related to the board limits or board behavior.

The Java implementation of the aforementioned tests is as follows:

@Test

public void whenDiscOutsideBoardThenRuntimeException() {

int column = -1;

exception.expect(RuntimeException.class);

exception.expectMessage("Invalid column " + column);

tested.putDiscInColumn(column);

}

@Test

public void whenFirstDiscInsertedInColumnThenPositionIsZero() {

int column = 1;

assertThat(tested.putDiscInColumn(column), is(0));

}

@Test

public void whenSecondDiscInsertedInColumnThenPositionIsOne() {

int column = 1;

tested.putDiscInColumn(column);

assertThat(tested.putDiscInColumn(column), is(1));

}

[ 128 ]

Design – If It's Not Testable, It's Not Designed Well Chapter 5

@Test

public void whenDiscInsertedThenNumberOfDiscsIncreases() {

int column = 1;

tested.putDiscInColumn(column);

assertThat(tested.getNumberOfDiscs(), is(1));

}

@Test

public void whenNoMoreRoomInColumnThenRuntimeException() {

int column = 1;

int maxDiscsInColumn = 6; // the number of rows

for (int times = 0; times < maxDiscsInColumn; ++times) {

tested.putDiscInColumn(column);

}

exception.expect(RuntimeException.class);

exception.expectMessage("No more room in column " + column);

tested.putDiscInColumn(column);

}

This is the necessary code to satisfy the tests:

private static final int ROWS = 6;

private static final int COLUMNS = 7;

private static final String EMPTY = " ";

private String[][] board = new String[ROWS][COLUMNS];

public Connect4TDD() {

for (String[] row : board) Arrays.fill(row, EMPTY);

}

public int getNumberOfDiscs() {

return IntStream

.range(0, COLUMNS)

.map(this::getNumberOfDiscsInColumn)

.sum();

}

private int getNumberOfDiscsInColumn(int column) {

return (int) IntStream

.range(0, ROWS)

.filter(row -> !EMPTY.equals(board[row][column]))

.count();

}

public int putDiscInColumn(int column) {

[ 129 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

checkColumn(column);

int row = getNumberOfDiscsInColumn(column);

checkPositionToInsert(row, column);

board[row][column] = "X";

return row;

}

private void checkColumn(int column) {

if (column < 0 || column >= COLUMNS)

throw new RuntimeException("Invalid column " + column);

}

private void checkPositionToInsert(int row, int column) {

if (row == ROWS)

throw new RuntimeException("No more room in column " + column);

}

Requirement 3 – player shifts

The third requirement relates to the game logic.

It is a two-person game, so there is one colour for each player. One player uses red ( R) and the other one uses green ( G). Players alternate turns, inserting one disc every time.

These tests cover the verification of the new functionality. For the sake of simplicity, the red player will always start the game:

@Test

public void whenFirstPlayerPlaysThenDiscColorIsRed() {

assertThat(tested.getCurrentPlayer(), is("R"));

}

@Test

public void whenSecondPlayerPlaysThenDiscColorIsRed() {

int column = 1;

tested.putDiscInColumn(column);

assertThat(tested.getCurrentPlayer(), is("G"));

}

[ 130 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

A couple of methods need to be created to cover this functionality. The switchPlayer method is called before returning the row in the putDiscInColumn method: private static final String RED = "R";

private static final String GREEN = "G";

private String currentPlayer = RED;

public Connect4TDD() {

for (String[] row : board) Arrays.fill(row, EMPTY);

}

public String getCurrentPlayer() {

return currentPlayer;

}

private void switchPlayer() {

if (RED.equals(currentPlayer)) currentPlayer = GREEN;

else currentPlayer = RED;

}

public int putDiscInColumn(int column) {

...

switchPlayer();

return row;

}

Requirement 4 – the game's output

Next, we should let the player know the status of the game.

We want feedback when either an event or an error occurs within the

game. The output shows the status of the board on every move.

As we are throwing exceptions when an error occurs, this is already covered, so we only need to implement these two tests. Furthermore, for the sake of testability, we need to introduce a parameter within the constructor. By introducing this parameter, the output becomes easier to test:

private OutputStream output;

@Before

[ 131 ]

Design – If It's Not Testable, It's Not Designed Well Chapter 5

public void beforeEachTest() {

output = new ByteArrayOutputStream();

tested = new Connect4TDD(new PrintStream(output));

}

@Test

public void whenAskedForCurrentPlayerTheOutputNotice() {

tested.getCurrentPlayer();

assertThat(output.toString(), containsString("Player R turn"));

}

@Test

public void whenADiscIsIntroducedTheBoardIsPrinted() {

int column = 1;

tested.putDiscInColumn(column);

assertThat(output.toString(), containsString("| |R| | | | | |"));

}

One possible implementation is to pass the preceding tests. As you can see, the class constructor now has one parameter. This parameter is used in several methods to print the event or action description:

private static final String DELIMITER = "|";

public Connect4TDD(PrintStream out) {

outputChannel = out;

for (String[] row : board) Arrays.fill(row, EMPTY);

}

public String getCurrentPlayer() {

outputChannel.printf("Player %s turn%n", currentPlayer);

return currentPlayer;

}

private void printBoard() {

for (int row = ROWS - 1; row >= 0; row--) {

StringJoiner stringJoiner = new StringJoiner(DELIMITER,

DELIMITER, DELIMITER);

Stream.of(board[row]).forEachOrdered(stringJoiner::add);

outputChannel.println(stringJoiner.toString());

}

}

public int putDiscInColumn(int column) {

...

printBoard();

switchPlayer();

[ 132 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

return row;

}

Requirement 5 – win condition (I)

This requirement tells the system whether the game is finished.

When no more discs can be inserted, the game finishes and it is considered a draw.

There are two conditions to test. The first condition is that new game must be unfinished; the second condition is that full board games must be finished:

@Test

public void whenTheGameStartsItIsNotFinished() {

assertFalse("The game must not be finished",

tested.isFinished());

}

@Test

public void whenNoDiscCanBeIntroducedTheGamesIsFinished() {

for (int row = 0; row < 6; row++)

for (int column = 0; column < 7; column++)

tested.putDiscInColumn(column);

assertTrue("The game must be finished", tested.isFinished());

}

An easy and simple solution to these two tests is as follows:

public boolean isFinished() {

return getNumberOfDiscs() == ROWS * COLUMNS;

}

Requirement 6 – win condition (II)

This is the first win condition requirement for players.

If a player inserts a disc and connects more than three discs of his color in a straight vertical line, then that player wins.

[ 133 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

In fact, this requires one single check. If the current inserted disc connects other three discs in a vertical line, the current player wins the game:

@Test

public void when4VerticalDiscsAreConnectedThenPlayerWins() {

for (int row = 0; row < 3; row++) {

tested.putDiscInColumn(1); // R

tested.putDiscInColumn(2); // G

}

assertThat(tested.getWinner(), isEmptyString());

tested.putDiscInColumn(1); // R

assertThat(tested.getWinner(), is("R"));

}

There are a couple of changes to the putDiscInColumn method. Also, a new method called checkWinner has been created:

private static final int DISCS_TO_WIN = 4;

private String winner = "";

private void checkWinner(int row, int column) {

if (winner.isEmpty()) {

String colour = board[row][column];

Pattern winPattern =

Pattern.compile(".*" + colour + "{" +

DISCS_TO_WIN + "}.*");

String vertical = IntStream

.range(0, ROWS)

.mapToObj(r -> board[r][column])

.reduce(String::concat).get();

if (winPattern.matcher(vertical).matches())

winner = colour;

}

}

Requirement 7 – win condition (III)

This is the second win condition, which is pretty similar to the previous one.

If a player inserts a disc and connects more than three discs of his color in a straight horizontal line, then that player wins.

[ 134 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

This time, we are trying to win the game by inserting discs into adjacent columns:

@Test

public void when4HorizontalDiscsAreConnectedThenPlayerWins() {

int column;

for (column = 0; column < 3; column++) {

tested.putDiscInColumn(column); // R

tested.putDiscInColumn(column); // G

}

assertThat(tested.getWinner(), isEmptyString());

tested.putDiscInColumn(column); // R

assertThat(tested.getWinner(), is("R"));

}

The code to pass this test is put into the checkWinners method:

if (winner.isEmpty()) {

String horizontal = Stream

.of(board[row])

.reduce(String::concat).get();

if (winPattern.matcher(horizontal).matches())

winner = colour;

}

Requirement 8 – win condition (IV)

The last requirement is the last win condition.

If a player inserts a disc and connects more than three discs of his color in a straight diagonal line, then that player wins.

We need to perform valid game movements to achieve the condition. In this case, we need to test both diagonals across the board: from top-right to bottom-left and from bottom-right to top-left. The following tests use a list of columns to recreate a full game to reproduce the scenario under test:

@Test

public void when4Diagonal1DiscsAreConnectedThenThatPlayerWins() {

int[] gameplay = new int[] {1, 2, 2, 3, 4, 3, 3, 4, 4, 5, 4};

for (int column : gameplay) {

tested.putDiscInColumn(column);

}

assertThat(tested.getWinner(), is("R"));

[ 135 ]

Design – If It's Not Testable, It's Not Designed Well Chapter 5

}

@Test

public void when4Diagonal2DiscsAreConnectedThenThatPlayerWins() {

int[] gameplay = new int[] {3, 4, 2, 3, 2, 2, 1, 1, 1, 1};

for (int column : gameplay) {

tested.putDiscInColumn(column);

}

assertThat(tested.getWinner(), is("G"));

}

Again, the checkWinner method needs to be modified, adding new board verifications: if (winner.isEmpty()) {

int startOffset = Math.min(column, row);

int myColumn = column - startOffset,

myRow = row - startOffset;

StringJoiner stringJoiner = new StringJoiner("");

do {

stringJoiner .add(board[myRow++][myColumn++]);

} while (myColumn < COLUMNS && myRow < ROWS);

if (winPattern .matcher(stringJoiner.toString()).matches())

winner = currentPlayer;

}

if (winner.isEmpty()) {

int startOffset = Math.min(column, ROWS - 1 - row);

int myColumn = column - startOffset,

myRow = row + startOffset;

StringJoiner stringJoiner = new StringJoiner("");

do {

stringJoiner.add(board[myRow--][myColumn++]);

} while (myColumn < COLUMNS && myRow >= 0);

if (winPattern.matcher(stringJoiner.toString()).matches())

winner = currentPlayer;

}

Final considerations

Using TDD, we got a class with a constructor, five public methods, and six private methods.

In general, all methods look pretty simple and easy to understand. In this approach, we also got a big method to check winner conditions: checkWinner. The advantage is that with this approach we got a bunch of useful tests to guarantee that future modifications do not alter the behavior of the method accidentally, allowing for the introduction of new changes painlessly. Code coverage wasn't the goal, but we got a really high percentage.

[ 136 ]

Design – If It's Not Testable, It's Not Designed Well

Chapter 5

Additionally, for testing purposes, we refactored the constructor of the class to accept the output channel as a parameter (dependency injection). If we need to modify the way the game status is printed, it will be easier that way than replacing all the uses in the traditional approach. Hence, it is more extensible. In the test-last approach, we have been abusing the System.println method and it will be really tedious task if we decide to change all the occurrences for any other thing.

In large projects, when you detect that a great number of tests must be created for a single class, this enables you to split the class following the Single Responsibility Principle. As the output printing was delegated to an external class passed in a parameter in initialization, a more elegant solution would be to create a class with high-level printing methods. That would keep the printing logic separated from the game logic. Like the huge code coverage shown in the following image, these are a few examples of the benefits of good design using TDD:

The code of this approach is available

at https://bitbucket.org/vfarcic/tdd-java-ch05-design.git.

Summary

In this chapter, we briefly talked about software design and a few basic design principles.

We implemented a fully functional version of the board game Connect 4 using two approaches—traditional and TDD.

[ 137 ]

Design – If It's Not Testable, It's Not Designed Well Chapter 5

We analyzed both solutions in terms of pros and cons, and used a Hamcrest framework to empower our tests.

Finally, we concluded that good design and good practices can be performed by both approaches, but TDD is a better approach.

For further information about the topics that this chapter covers, refer to two highly recommended books written by Robert C. Martin: Clean Code: A Handbook of Agile Software Craftsmanship and Agile Software Development: Principles, Patterns, and Practices.

[ 138 ]

6

Mocking – Removing External

Dependencies

"Talk is cheap. Show me the code."

