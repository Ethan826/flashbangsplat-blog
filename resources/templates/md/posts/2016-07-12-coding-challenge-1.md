{:title "Tic-Tac-Toe Coding Challenge Part 1"
 :layout :post
 :tags ["tic-tac-toe", "coding challenge", "minimax"]}
 
In May, I completed a coding challenge from which I learned a lot. The
challenge was to adapt a badly implemented game of Tic-Tac-Toe into one
that followed SOLID design principles; permitted the human vs. human,
human vs. computer; and computer vs. computer; and could not be beaten.
The finished version is
[here](https://github.com/Ethan826/tic-tac-toe_coding_challenge).

I will post a series of blog articles describing some of the more
interesting things I learned about.

### Minimax algorithm

The unbeatable AI player uses a version of the minimax algorithm called
negamax. The minimax algorithm reflects the straightforward fact that
your goal in a game is to maximize how well you are doing in the game
while your opponent’s goal is to minimize how well you are doing. In a
more complicated game than tic-tac-toe, there might be ways of scoring a
game still in progress. But for present purposes, a game of tic-tac-toe
can only have three values: the value for winning, the value for a draw,
and the value for losing. The value of winning is positive n, drawing is
0, and losing is negative n. Let’s choose +1000.0, 0.0, and -1000.0 for
discussion purposes.

#### First, find all permutations of the game.

The minimax algorithm, in short, looks at all possible future game
states (or all possible future game states down to a specified level,
e.g., three moves ahead). It looks for the move that will maximize its
score on its turn (the “max” part), and assumes that its opponent will
look for the move that will minimize its score (the “mini” part). In
other words, it tries to avoid what makes me a terrible chess player:
noticing a desirable game state and make moves to bring game state
about, but fail to take into account that one’s opponent will not make
the bad move needed for that game state to come about (e.g., “If I move
my pawn here, and my opponent makes the suicidal decision to move her
knight here, I can take her queen”).

Imagine an empty 3x3 tic-tac-toe board, with the computer set to make
the first move. There are 9 possible moves. For each of those moves, the
opponent can make one of 8 responses. The computer then has its choice
of 7 counters. In other words, a 3x3 board, with its 9 spaces, has 9!
possible outcomes—except that some game states represent one or the
other players winning.

#### Then, evaluate the leaf nodes

The minimax algorithm examines each of these game states. What if I move
in the center? Then, the opponent could move to the upper left, upper
middle, … lower right. The minimax algorithm runs to the bottom of each
branch of the tree of possible game states.

Consider the following game state; the computer is `X` and it’s `O`’s
turn to move:

    O│X│
    ─┼─┼─
    X│X│O
    ─┼─┼─
    X│O│

Because it is the opponent’s move, the computer knows that it will seek
to minimize its score. If the opponent moves to the lower right, the
only possibility for the computer will be to move to the upper right.
That will result in the computer winning, which the computer scores as
being +1000.0. If the opponent moves to the upper right, the computer
can only move to the lower right. That is worth 0.0 to the computer
because it is a draw. On this “mini” round, the opponent will make the
move that results in 0.0 rather than the move that results in +1000.0.
The computer therefore knows to score this game state as being worth
0.0, *even though the opponent could make a move that would allow the
computer to win*. That’s what I meant when I said that minimax prevents
the computer from making moves out of an optimistic or foolish hope that
the opponent will make a move that advantages the computer.

#### Then, assign the parents whose only children are leaf nodes the appropriate value

The algorithm is of the so-called “depth first” variety. That means that
it runs all the way to the bottom of the game tree to see all possible
outcomes, scores all of the leaf nodes (those game states that are at
the end of their branches because someone has won or because the game
board is full), determines which leaf node the player of that round will
choose, and scores it accordingly.

So if a parent node has only leaf nodes, and those leaf nodes all occur
during a round played by the opponent, the computer will look for the
play that minimizes the score. That is, the computer assumes that the
opponent *would make that move*, and so can forget about all the other
moves and simply value the parent node at the value of lowest-scoring
leaf. The computer performs the same analysis on all siblings of that
node, but this time, that round of the game is the one the computer gets
to play. So it chooses the highest-scoring sibling node (all of the
sibling nodes have had their children nodes evaluated for the minimizing
score). And so on: the algorithm works back up from the leaf nodes of
the tree, consolidating the results into the play that minimizes the
score if it’s the opponent’s turn and that maximizes the score if it’s
the computer’s turn.

#### An example

A difficulty in thinking this algorithm through is that the computer
first has to come up with a huge number of possible game states, dive
all the way down the tree of possible moves, and then work backwards to
the top to come up with the single best move. But here is an example to
try to show how it works:

The computer moved second and is `O`. It is evaluating the possible
moves for `O` (it is `O`’s turn), given the following board state:

    X│X│
    ─┼─┼─
    O│X│
    ─┼─┼─
     │ │O

The only moves that prevent immediate defeat are as follows: 

    X│X│
    ─┼─┼─
    O│X│
    ─┼─┼─
     │O│O
    
    --or--
    
    X│X│O
    ─┼─┼─
    O│X│
    ─┼─┼─
     │ │O

Any other move actually give `X` the choice of how to win: vertically in the
middle, or diagonally from bottom right to top left. The maximizing move this
round requires one of the plays shown above.

But look carefully: each of these moves provides only a temporary reprieve. `X`
will definitely win next round. Thus, the value of the board state has a value
of -1000 because the opponent, during its “mini” move, will definitely play the
move that causes the computer to lose. 

Remember, however, that the computer starts at the bottom of the tree and works
its way up. So as the computer comes back up the tree of possible game states,
it will know not to choose whatever move led to _that game state_ (unless there
is no better move). That means that the computer won’t get itself into this
situation, because the computer assumes that `X`, during its “mini” move, will
move to top center:

    X│ │
    ─┼─┼─
    O│X│
    ─┼─┼─
     │ │O

So during its “max” move, the computer won’t choose this game state. The
round before looks like this:

    X│ │
    ─┼─┼─
    O│X│
    ─┼─┼─
     │ │ 

Here, unless `O` moves bottom right, `X` will win on the next round. So
the only plausible move is to the bottom right. But as we have just
seen, that leads to certain defeat two rounds later. So the computer
will not go there. When the board is like this:

     │ │
    ─┼─┼─
     │X│
    ─┼─┼─
     │ │ 

the computer will already have figured out that it will be checkmated by correct
play if it moves to any position but the corner. It is precisely this logic that
drives a minimax AI with full-depth search in a 3x3 game of tic-tac-toe never to
move to an outer middle spot if the opponent opens the game in the center.
