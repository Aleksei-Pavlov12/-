# -def print_board(board):
    print("  0   1   2")
    for i, row in enumerate(board):
        print(f"{i} {' | '.join(row)}")
    print()

def check_winner(board):
    for i in range(3):
        if board[i][0] == board[i][1] == board[i][2] != " " or board[0][i] == board[1][i] == board[2][i] != " ":
            return board[i][i]
    if board[0][0] == board[1][1] == board[2][2] != " " or board[0][2] == board[1][1] == board[2][0] != " ":
        return board[1][1]
    if all(cell != " " for row in board for cell in row):
        return "Draw"
    return None

def main():
    board = [[" " for _ in range(3)] for _ in range(3)]
    player = "X"

    while True:
        print_board(board)
        row, col = map(int, input(f"Ход {player} (строка и столбец через пробел): ").split())
        if board[row][col] != " ":
            print("Клетка занята, попробуйте снова")
            continue
        board[row][col] = player
        result = check_winner(board)
        if result:
            print_board(board)
            print("Ничья!" if result == "Draw" else f"Победил {result}!")
            break
        player = "O" if player == "X" else "X"

if __name__ == "__main__":
    main()
