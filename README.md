import random
max_lines = 3
min_bet = 1
max_bet = 100
rows = 3
cal = 3
symbol_coun = {'A':3,'B':6,'C':2,'D':5}
symbol_value = {'A':5,'B':2,'C':3,'D':6}
def deposit():
    while True:
        amount = input("enter how much amount you want to deposit?")
        if amount.isdigit():
            amount = int(amount)
            if amount > 0:
                break
            else:
                print("enter the amount greater than 0")
        else :
            print("please enter a number")
    return amount
def num_of_lines():
    while True:
        lines = input("enter no of lines you want to bet (1- "+ str(max_lines)+"):")
        if lines.isdigit():
            lines = int(lines)
            if 1 <= lines <= max_lines:
                break
            else:
                print("enter the lines between 1- " + str(max_lines))
        else :
            print("please enter a number")
    return lines

def get_bet():
    while True:
        bet_amount= input("How much u want to place your bet on lines?")
        if bet_amount.isdigit():
            bet_amount = int(bet_amount)
            if min_bet <= bet_amount <= max_bet:
                break
            else:
                print(f"enter the bet between {min_bet} and {max_bet} ")
        else :
            print("please enter a number")
    return bet_amount
 
def spin_machine(rows,cal,symbol_coun):
    all_symbol = []
    for i,sys in symbol_coun.items():
        for _ in range(sys):
            all_symbol.append(i)
    cols = []
    for i in range(cal):
        col = []
        current_symbol = all_symbol[:]
        for j in range(rows):
            value = random.choice(all_symbol)
            current_symbol.remove(value)
            col.append(value)
        cols.append(col)
    return cols

def print_spin_machine(cols):
    for row in range(len(cols[0])):
        for i,colm in enumerate(cols):
            if i != len(cols[0])- 1:
                print(colm[row],end = " | ")
            else:
                print(colm[row],end = "")
        print()
def check_winings(col,lines,bet,vlaues):
    winings = 0
    for line in range(lines):
        sym = col[0][line]
        for i in col:
            sym_to_check = col[line]
            if sym != sym_to_check:
                break
        else:
            winings += value[sym] * bet
    return winings
def spin():
     lines = num_of_lines()
     while True:
        amount = deposit()
        bet_amount = get_bet()
        total_bet = bet_amount*lines
        if total_bet > amount:
            print(f"you don't have much amount to bet, your balnce is: {deposit}")
        else:
            break
        print(f"your betting {bet_amount} on line {lines}.Total bet amount is :{total_bet}")
        spin = spin_machine(rows,cal,symbol_coun)
        print_spin_machine(spin)
        winings = check_winings(spin,lines,bet_amount,symbol_value)
        return winings - total_bet

def main():
    amount = deposit()
    while True:
        print(f"your current balance is {amount}")
        ans = input("press enter to play or Q to Quit.")
        if ans == "Q":
            break
        amount += spin()
main()
