# TicTacToe

This project is a true simulation of a famous game, namely; Tic Tac Toe. The actual code of the game was written by [xaviablaza-zz](https://gist.github.com/xaviablaza-zz/)
In this project, the main goal was to apply unit testing using JUnit Framework. Moreover, The code has been **modularized** to make it readeable, understable and reusable. 

# Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes:
- Download the project.
- Unzip the project.
- Run the project on a NetBeans IDE.

# Prerequisites

These are the tools and framewroks used in this project (MUST have):

- Netbeans IDE (one of the latest versions is preferred).
- JUnit Framework (should be available as a plugin in the IDE/otherwise, should be downloaded). 

# Running the tests

To run the tests:
1. Go to the Test Packages.
2. Open the tictactoe folder.
3. Select the TestRunner class.
4. Right Click >> Run File.

# Testing

Unit testing is the main type used to test the individual functions and methods of this project. To ensure conformance with user requirements and to find any possible defects, I have used the unit tesing.

**For Example:**
The following method should check the validity of a user input, knowing that only positive integer values from 1 to 9 are accepted:
```
public boolean checkInputRange(int userInput) {
        boolean correctness = true;
        if (!(userInput >= 1 && userInput <= 9)) {
            correctness = false;
        }
        return correctness;
    }
```
The following code tests the methods above with an input of 10, which should result in false:
```
@Test
    public void testCheckInputGreaterThanRange() {
        System.out.println("checkInput Test: checks that the entered value lies between 1 and 9, in this case the entered value is greater than the maximum allowed value.");
        int userInput = 10;
        boolean result = instance.checkInputRange(userInput);
        assertFalse(result);
    }
```
<hr>

In this project, I also have used the parameterized test to test the same method multiple times with different input sets without the need to create an individual test for each set of inputs:

**For Example:**
The method below should be called each time a player inputs a value, either X or O to define the winner, if available:

```
public String checkWinner(String[] board) {
        String winner = " ";
        for (int a = 0; a < 8; a++) {
            String line = null;
            switch (a) {
                case 0:
                    line = board[0] + board[1] + board[2];
                    break;
                case 1:
                    line = board[3] + board[4] + board[5];
                    break;
                case 2:
                    line = board[6] + board[7] + board[8];
                    break;
                case 3:
                    line = board[0] + board[3] + board[6];
                    break;
                case 4:
                    line = board[1] + board[4] + board[7];
                    break;
                case 5:
                    line = board[2] + board[5] + board[8];
                    break;
                case 6:
                    line = board[0] + board[4] + board[8];
                    break;
                case 7:
                    line = board[2] + board[4] + board[6];
                    break;
            }
            if (line.equals("XXX")) {
                winner = "X";
            } else if (line.equals("OOO")) {
                winner = "O";
            }
        }
```

Since it is a Tac Tic Toe game the winner can be defined in multiple ways, for instance, if one of the players forms a horizental, vertical or diagonal line of three consecutive cells of the same value (X or O), then we have a winner. Testing this function could be time consuming if we have used a seperate method for each possibility. On the other hand, using the parameterized test will make the process much more easier:

```
  @Parameters
    public static Collection input() {
        return Arrays.asList(new Object[][]{
            {new String[]{"X", "O", "3", "X", "O", "6", "7", "O", "X"}, "O"},
            {new String[]{"X", "O", "3", "X", "O", "6", "X", "8", "9"}, "X"},
            {new String[]{"X", "X", "X", "O", "O", "6", "7", "8", "9"}, "X"},
            {new String[]{"X", "X", "3", "O", "O", "O", "7", "8", "X"}, "O"}

        });
    }

   
    public void testGame() {
        System.out.println("The winer is: " + expectedResult);
        assertEquals(expectedResult, instance.checkWinner(board));
    }
```

<hr>
Also, the TestSuite class has been used to be able to use multiple test classes at once, and the Testrunner class is used to run all test classes at once by instaniating the TestSuite class.


# Acknowledgments
- The original code was written by: [xaviablaza-zz](https://gist.github.com/xaviablaza-zz/)
