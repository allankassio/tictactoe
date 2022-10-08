# tictactoe

This project was created with the aim of presenting the concept of a game tree in Data Structure tutoring for students of UNDB technology courses.

The project has two files. One implements tic-tac-toe with a dumb, random AI:

```python
def random_move(state):
    """
    A function that choice a random move
    :param state: current state of the board
    :return: a list with [random row, randam col]
    """

    empyty_cells = empty_cells(state)
    random.shuffle(empyty_cells)

    return empyty_cells[0]
```

The second implements the MINIMAX algorithm:

```python
def minimax(state, depth, player):
    """
    AI function that choice the best move
    :param state: current state of the board
    :param depth: node index in the tree (0 <= depth <= 9),
    but never nine in this case (see iaturn() function)
    :param player: an human or a computer
    :return: a list with [the best row, best col, best score]
    """
    if player == COMP:
        best = [-1, -1, -infinity]
    else:
        best = [-1, -1, +infinity]

    if depth == 0 or game_over(state):
        score = evaluate(state)
        return [-1, -1, score]

    for cell in empty_cells(state):
        x, y = cell[0], cell[1]
        state[x][y] = player
        score = minimax(state, depth - 1, -player)
        state[x][y] = 0
        score[0], score[1] = x, y

        if player == COMP:
            if score[2] > best[2]:
                best = score  # max value
        else:
            if score[2] < best[2]:
                best = score  # min value

    return best
```

The main code was copied from the https://github.com/Cledersonbc/tic-tac-toe-minimax repository.
