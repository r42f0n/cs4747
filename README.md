java cCoursework 3
In this coursework, you are required to write several Python functions, by filling in code into the
template below. Submit your Python script via upload on Blackboard before the deadline on
Friday, 13th December 2024 at 1pm.
I suggest aiming to submit at least one hour earlier, to avoid any last-minute computer problems.
Working independently
As with all assessed work in this unit, you must complete this coursework independently on
your own. You must not take code from elsewhere, even if it is referenced. You are however
allowed to use the lecture notes and exercise solutions freely, and the lecture notes contain all
that is required to solve the problems. You are not allowed to ask others for help, and in
particular, you are not allowed to send, give, or receive Python code to/from classmates and
others.
See the University Guidelines for Academic Malpractice.
Instructions
1. Copy the code out of the template below and save it as a .py fi le in Spyder (or another
Python editor of your choice).
2. Add your name, university ID number and university email address in the
docstring at top of the file, where indicated
3. Write code to replace the pass statements in the functions initial_state,
parse_move, validate_move, apply_move, game_won for questions 1 C5. For
questions 1 C5, do not alter the existing play_game function.
4. For questions 6 C8, modify only the parse_move and play_game functions as requested.
5. Do not alter the names or parameters of any functions. Do not create any further
functions with the same names. Ensure that these functions can be called with the
parameters precisely as specifi ed, and that they return (not print) values of the correct
data types.
 Coursework 3
_un   1/16
6. Submit your work on Blackboard as a .py Python file. Do not submit a screenshot,
PDF, Word document, iPython notebook, or file in any other format.
Aspects of this coursework will be marked automatically and failure to follow the
problem description or any of the instructions above will result in loss of marks.
To check that your code is working correctly, you may wish to add some of your own tests
in a new function  C these will not be marked.
If you wish, you can also add other functions to the code, and call them from the required
functions. Make sure all code (other than module import statements) is within a function.
Do not create any further functions with the same name as any of the required functions.
Do not use the input function anywhere in your code. The only use of input allowed is
my existing line of code in the play_game function.
Make sure your functions return the value they should return, not just print the value
to screen.
As this is part of the course assessment, we will not be able to help you solving these
problems. If you are unsure what any question is asking for, please ask on the Blackboard
Discussion Forum.
If you provided a valid email address in the docstring at the beginning of your .py fi le, you
will receive a feedback report with your score for each function.
Template code
The template that you should use for your coursework is below. Two functions are provided:
display_state is a function that displays the state of the game on the screen, using
fancy colours!
play_game is a pre-written basic framework for the game. You must not modify this
function for questions 1 C5, but it is modifi ed in questions 6 C8.
"""
MATH20621 - Coursework 3
Student name: add your name
Student id: add your id number
Student mail: your.name@student.manchester.ac.uk
"""
 Coursework 3
_un   2/16
def display_state(s, *, clear=False):
"""
Display the state s
If 'clear' is set to True, erase previous displayed state
"""
def colored(r, g, b, text):
rb,gb,bb=(r+2)/3,(g+2)/3,(b+2)/3
rd,gd,bd=(r)/1.5,(g)/1.5,(b)/1.5
return f"\033[38;2;{int(rb*255)};{int(gb*255)};{int(b
def inverse(text):
rb,gb,bb=.2,.2,.2
rd,gd,bd=.8,.8,.8
return f"\033[38;2;{int(rb*255)};{int(gb*255)};{int(b
colours = [(1.0, 0.349, 0.369),
(1.0, 0.573, 0.298),
(1.0, 0.792, 0.227),
(0.773, 0.792, 0.188),
(0.541, 0.788, 0.149),
(0.322, 0.651, 0.459),
(0.098, 0.509, 0.769),
(0.259, 0.404, 0.675),
(0.416, 0.298, 0.576)]
n_columns = len(s['stacks'])
if clear:
print(chr(27) + "[2J")
print('\n')
row = 0
numrows = max(len(stack) for stack in s['stacks'])
for row in range(numrows-1,-1,-1):
for i in range(n_columns):
num_in_col = len(s['stacks'][i])
if num_in_col > row:
val = s['stacks'][i][row]
if num_in_col == row+1 and s['blocked'][i]:
print(inverse(' '+str(val)+' '),end=' ')
else:
if s['complete'][i]:
print(colored(*colours[val-1],' '),
else:
print(colored(*colours[val-1],' '+str
else:
print(' ',end='')
 Coursework 3
_un   3/16
print()
print(' A B C D E F')
# Q1
def initial_state():
pass
# Q2
def parse_move(input_str):
pass
# Q3
def validate_move(state, move):
pass
# Q4
def apply_move(state, move):
pass
# Q5
def game_won(state):
pass
# For questions 1-5, DO NOT edit the play_game function.
# For the tasks in questions 1-5 initial_state, parse_move,
# validate_move, apply_move, and game_won must work with the
# the unmodified play_game function.
# For questions 6, 7 and 8, you should modify the play_game
# function
def play_game():
# When we start the game,
board = initial_state()
try:
while True:
# Display the current game state
display_state(board, clear=False)
# Read input from the user.
# (Do not alter this line, even in questions 6, 7
move_str = input()
# Parse the text typed by the user and convert it
move = parse_move(move_str)
 Coursework 3
_un   4/16
# If the move was valid...
if validate_move(board, move):
apply_move(board, move) # ... alter the board
# If we've won, end the game
if game_won(board):
break
except KeyboardInterrupt: # If the user presses Ctrl-C, q
pass
play_game()
Solitaire
This coursework implements a game of solitaire.
Solitaire, or Patience, is a name given to a single-player game, usually a game played with a pack
of cards. The game originated in Europe in around 1800, and numerous variations have been
developed since.
During this coursework, you will write Python program to simulate a particular variation of
solitaire.
The game works as follows. When played as a tabletop game, we start with a standard 52-card
deck, but only the numerical cards 1, 2, 3, 4, 5, 6, 7, 8, 9 are dealt  C the court cards (King, Queen
Jack) are omitted. The suit of the cards (?, ?, ?, ?) plays no role in the game. As a result, there
are 36 cards in play, four copies of each of the numbers 1 C9. We  ll refer to the ace as 1, rather
than A.
These cards are shuffl ed and dealt into six stacks, which we  ll name A through F, each containing
six cards, for example:
 Coursework 3
_un   5/16
A B C D E F
The aim of the game is to rearrange these cards into four complete stacks of nine ordered cards.
Here,   ordered   means in decreasing order going down the stack, i.e.
A B C D E F
A B C D E F
This is one of several moves we could have made: we could alternatively have moved the 2 in
stack C onto the 3 in stack A, the 3 in stack A onto the 4 in stack B, or the 7 in stack D onto the
8 of stack F.
Moving multiple cards
We can move more than one of the top cards on a stack at once, so long as those cards are
ordered. For example, after our first move there is a pair of ordered cards at the top of stack C:

A B C D E F
Just as before, we can move this pair to another stack if the top number in the destination stack
is one larger than the bottom card of those to be moved. In our game, the only stack that satisfi es
this is stack A, and we can move two cards from stack C to stack A:
 Coursework 3
_un   7/16

A B C D E F
You may have noticed that there is another pair of ordered cards, an 8 and a 9, at the top of stack
F. We cannot move this pair currently, as there is nowhere for it to go. The rule for moving a 9
card (or multiple cards with 9 the largest) is that a 9 can only move into an empty stack.
We can however move the new stack of 1, 2, 3 formed on stack A onto stack B:
A B C D E F
Our available moves are now a bit limited. While we can move the single 8 on stack F onto stack
E, that doesn  t really help us progress, as it only reveals a 9. Perhaps the best move is to move the
7 on stack D onto stack A:
 Coursework 3
_un   8/16
2
A B C D E F
At this point, there are still moves we can make, but it  s diffi cult to see how we can make enough
cards to completely re-order them into four complete stacks as required. However, we are
allowed to break the rules established above, in a very specifi c way.
Blocking moves
A single card at the top of a stack can be moved onto another stack, even if it is not one less than the
number at the top of the destination stack. However, in that case, the moved card blocks the
destination stack, here indicated with a black card. No further cards can be added to the
destination stack. The only way to unblock the stack is to move the single blocking card at the
top of the stack onto a valid location  C that is, onto an empty stack, or onto a stack whose top
card is one greater than the card being moved. So, we can move the 1 from stack C to stack E.
A B C D E F
This blocks stack E, really opens things up. We move the 3 from stack D to stack C, then the 2
from stack D to stack C. Then, we can then move the blocking 1 from stack E onto the 2 on the
top of stack C, thus unblocking stack E, as follows:
 Coursework 3
_un   9/16
1
A B C D E F
We  ll now take a succession of steps:
Move the top four cards from stack B (1, 2, 3, 4) onto stack D
Move the top five cards from stack D (1, 2, 3, 4, 5) onto stack B
Move the top six cards from stack B (1, 2, 3, 4, 5, 6) onto stack A
Move the to代 写program、Python
代做程序编程语言p card from stack D, now a 1, onto stack F. This blocks stack F.
Move the top card from stack D, now a 8, onto stack E.
Our stacks now look like
A B C D E F
Making a complete stack
 Coursework 3
_u   10/16
We  ve now got a complete run of numbers of 1, 2, 3, 4, 5, 6, 7, 8, 9 at the top of stack A. Moving
these to the empty stack D gives us the first complete stack that we are looking for. Here this
made by moving all nine cards to an empty stack all at once, but a complete stack can be formed
over more than one move too.
For example, we could have made the complete stack by first moving the top two cards of stack E (9 and
8) to stack D, then the top seven cards of stack A to stack D.
A B C D E F
Either way, once a complete stack is formed, the cards on it are turned over, and no cards can
added to or removed from that stack for the rest of the game. (This is indicated here by the
numbers begin removed from the cards.)
We now continue the game in the same way, except without being able to use stack D. Can you
see how in seven further moves, we could both complete a second stack and both unblock stack
F?
In terms of strategy, it is not always best to complete stacks as soon as possible, as this prevents that stack
from being used again, constraining what is possible in future moves.
Python implementation
The game state
 Coursework 3
_u   11/16
The most important part of this game is the representation of the game state    that is, which
cards are in which stacks, which stacks are blocked, and which are complete.
We represent the board state with a Python dictionary, (say, s), with three keys:
1. s['blocked'] is a list of six boolean values, corresponding to the six columns A CF.
The value is True if the column is blocked by a card, or False if it is not.
2. s['complete'] is a list of six boolean values, corresponding to the six columns A CF.
The value is True if the column is completed, or False if it is not.
3. s['stacks'] is a list of six lists of integers, corresponding to the cards in each stack.
The lists are ordered from bottom up, so for example s['stacks'][1][0] is the bottom
card on stack B.
So, for example, the game state
1
A B C D E F
could be created in Python with the statement:
s = { 'blocked': [False, False, False, False, False, True],
'complete': [False, False, False, True, False, False],
'stacks': [[2, 7, 4],
[1, 6, 5, 3],
[7, 8, 9, 4, 3, 2, 1],
[9, 8, 7, 6, 5, 4, 3, 2, 1],
[5, 7, 6, 4, 9, 8],
[1, 3, 5, 2, 9, 8, 1]]}
For any one column, blocked and complete should never both be True. An empty stack is
indicated by the corresponding element of s['stacks'] being an empty list []. Note that even
though the cards in the completed stack are not shown, the representation in 'stacks' shows
 Coursework 3
_u   12/16
the nine cards in order. Thus, at all times, the lists in 'stacks' should together contain 36
elements, four of each of the digits.
Describing a move
The other key part of the game is the idea of a move. A move is uniquely described by the source
stack, the destination stack, and the number of cards to be moved. We  ll represent a move as a
tuple of three integers,
m = (source_stack, destination_stack, number_of_cards)
The stacks are numbered from the left, starting with zero, so stack A is 0, stack B is 1 and so on.
For example, the move (0, 4, 3) represents a move of three cards from stack A onto stack E,
while a move (1, 2, 1) represents a move of one card from stack B onto stack C.
The assessed questions:
This coursework is worth 70 marks, and 70% of the course overall.
30 marks are allocated for the correctness of the functions defi ned in problems 1 C5. These
will be tested in an automated way, as in the previous courseworks.
15 additional marks are allocated based on number of perfect scores for core problems 1 C
5.
15 marks are allocated for problems 6 C8.
10 marks are for the quality of all the code.
Question 1: The initial state (6 marks)
Write a function initial_state that returns a dict corresponding to the game state at the
start of a new game. The cards should be randomly shuffl ed, allocated six to each stack, and no
stack should be marked complete or blocked.
Question 2: Interpreting user input (6 marks)
 Coursework 3
_u   13/16
At each turn, the user is asked for their input. The user should enter a string of two letters and
an integer, e.g. AB3 to indicate that they wish to move three cards from stack A onto stack B, or
FD1 to indicate that they wish to move one card from stack F onto stack D.
Write a function parse_move(input_str) which takes a string of this form and converts it
into a move tuple of the format described above, which it then returns. For example
parse_move('AB3') should return the tuple (0, 1, 3).
If the number of cards is omitted, make it default to one, so that parse_move('FD') returns
(5, 3, 1), corresponding to the move of a single card from stack F to stack D.
In this problem 2, you can assume that the string given by the user is a valid one, namely two
letters in the range A CF, optionally followed by a positive integer.
Question 3: Determining if a move is valid (10 marks)
Write a function validate_move(state, move) which returns True if the move move can
be applied to a game in state state. You can assume that the parameter state is a dictionary
corresponding to a valid game state (as described above), and that the parameter move is a tuple
of three integers.
This function should contain all the logic for checking whether a move is valid, including all the
rules described above on moving single cards, multiple cards, card ordering, blocking moves,
blocked stacks and completed stacks. The function should also check for nonsensical moves
(moving more cards than there are in the stack, moving to a nonexistent stack, etc.)
Question 4: Moving the cards (6 marks)
Write a function apply_move(state, move) which takes a valid game state state and a
move tuple move. This function does not return anything, but modifi es in-place the state
parameter passed to it to apply the move described by the move tuple. You can assume that
state is a valid game state and that move is a valid move that could be played in this state. This
function should update the blocked and complete fi elds of the game state state, as well as
the stacks.
Question 5: Detecting a win (2 marks)
 Coursework 3
_u   14/16
Write a function game_won(state) which takes a valid game state and returns True if the
game has been won (that is, all cards are in a completed stack) and False otherwise.
The game
In the template, you are given the pre-written function play_game() which uses the five
functions you have just written (initial_state, parse_move, validate_move,
apply_move, game_won) to simulate a game. You can now run the play_game function to
play a working game. In questions 1 C5, you must not change the existing play_game()
function.
The preceding five questions are the core questions of this coursework, together worth 30
marks. To recognise functions that are completely correct, a bonus is awarded for each question
in questions 1 C5 that scores full marks:
1 bonus mark is awarded if one core question scores full marks
3 bonus marks are awarded if two core questions score full marks
6 bonus marks are awarded if three core questions score full marks
10 bonus marks are awarded if four core questions score full marks
15 bonus marks are awarded if five core questions score full marks
(Because an important part of the game is that all of these functions work together correctly, the
bonus grows more quickly as more questions score full marks.)
There are then three additional questions (6 C8, worth 15 marks in total), and an assessment of
code quality (10 marks), whose marks simply add to the 45 available in questions 1 C5 to make a
total of 70.
Question 6: Handling errors (4 marks)
Modify your parse_move function from problem 2 so that raises a ValueError exception if:
The string is not of the form of: two letters, optionally followed by a positive integer, or
The two starting letters are outside the range A CF
Modify the play_game function to catch this exception and immediately re-prompt the user for
another move.
 Coursework 3
_u   15/16
As a result of these modifi cations, your game should now not crash, regardless of what string the
user types in.
Question 7: Resetting the game (2 marks)
Modify the parse_move function so that if the input string is R (or r), the function returns the
integer 0, rather than the move tuple.
Modify the play_game function so that if parse_move returns this integer 0, then the game is
reset (that is, initial_state is called and the game begins again).
Question 8: Undoing moves (9 marks)
Modify the parse_move function so that if the input string is U (or u), the function returns the
integer -1, rather than the move tuple.
Modify the play_game function so that if parse_move returns this integer -1, then the most
recent move is undone. By repeatedly typing U or u), the user should be able to undo as many
moves of the game as they like, until they end up back at the initial state. Ensure that the user
cannot undo beyond this point
Code quality (10 marks)
Ten marks are available for the quality of the code that you write in questions 1 C8. This will be
assessed by humans reading your code, and will be based on:
Clarity and precision of docstrings for each function
Clarity of comments elsewhere in the code that describe what the code is doing
Code quality. Code should be clear, effi cient and easy to maintain. Marks may be lost for
 C Very ineffi cient algorithms
 C Code that is unnecessarily verbose or diffi cult to understand
 C Unnecessary duplication of code
Code quality marks do not contribute to the bonus marks for questions 1 C5.
 Coursework 3
_u   16/16

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
