# Функция для отображения игрового поля
def print_board(board):
    for row in board:
        print(" | ".join(row))
        print("-" * 5)

# Функция для проверки победы
def check_winner(board, player):
    # Проверка строк
    for row in board:
        if row.count(player) == 3:
            return True

    # Проверка столбцов
    for col in range(3):
        if board[0][col] == board[1][col] == board[2][col] == player:
            return True

    # Проверка диагоналей
    if board[0][0] == board[1][1] == board[2][2] == player:
        return True
    if board[0][2] == board[1][1] == board[2][0] == player:
        return True

    return False

# Функция для проверки ничьей
def is_draw(board):
    for row in board:
        if " " in row:
            return False
    return True

# Главная функция игры
def play_game():
    # Инициализация пустого игрового поля
    board = [[" " for _ in range(3)] for _ in range(3)]
    current_player = "X"

    while True:
        print_board(board)
        print(f"Ход игрока {current_player}")
        
        # Ввод координат хода
        try:
            row, col = map(int, input("Введите строку и столбец (0, 1, 2): ").split())
            if board[row][col] != " ":
                print("Эта клетка уже занята, попробуйте снова.")
                continue
        except (ValueError, IndexError):
            print("Некорректный ввод. Введите два числа от 0 до 2 через пробел.")
            continue

        # Обновление игрового поля
        board[row][col] = current_player

        # Проверка на победу
        if check_winner(board, current_player):
            print_board(board)
            print(f"Игрок {current_player} победил!")
            break
        
        # Проверка на ничью
        if is_draw(board):
            print_board(board)
            print("Ничья!")
            break

        # Смена игрока
        current_player = "O" if current_player == "X" else "X"

# Запуск игры
if __name__ == "__main__":
    play_game()
