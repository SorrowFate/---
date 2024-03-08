field = [[" "] * 3 for i in range(3) ]


def show():
    print(f"  0 1 2")
    for i in range(3):
        print(f"{i} {field[i][0]} {field[i][1]} {field[i][2]}")


def ask():
    while True:
        coord = input("Для хода введите 2 координаты через пробел:").split()

        if len(coord) == 2:
            x, y = coord
            if x.isdigit() and y.isdigit():
                x, y = int(x), int(y)
                if 0 <= x <= 2 and 0 <= y <= 2:
                    if field[x][y] == " ":
                        return x, y
                    else:
                        print("Клетка занята")
                else:
                    print("Нужно ввести координаты от 0 до 2")
            else:
                print("Нужно вводить числа")
        else:
            print("Нужно ввести 2 координаты")

def win():
    win_coord = [((0, 0), (0, 1), (0, 2)), ((1, 0), (1, 1), (1, 2)), ((2, 0), (2, 1), (2, 2)),
                 ((0, 0), (1, 0), (2, 0)), ((0, 1), (1, 1), (2, 1)), ((0, 2), (1, 2), (2, 2)),
                 ((0, 0), (1, 1), (2, 2)), ((2, 0), (1, 1), (0, 2))]
    for coord in win_coord:
        a = coord[0]
        b = coord[1]
        c = coord[2]

        if field[a[0]][a[1]] == field[b[0]][b[1]] == field[c[0]][c[1]] != " ":
            print(f"Выиграл {field[a[0]][a[1]]}")
            return True
    return False

num_step = 0
while True:
    num_step += 1

    show()

    if num_step % 2 == 1:
        print("Ходит крестик")
    else:
        print("Ходит нолик")

    x, y = ask()

    if num_step % 2 == 1:
        field[x][y] = "X"
    else:
        field[x][y] = "0"

    if win():
        break

    if num_step == 9:
        print("Ничья")
        break
