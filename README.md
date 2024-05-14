# CIS567-integrated-lab-2
This function takes a list of dice values (values) as input and calculates the highest possible score based on various scoring rules used in a game. It internally calls several helper functions to check for specific scoring conditions.
# Find highest score
def find_high_score(values):
    high_score = 0
    high_score = max(
        check_singles(values, 1),
        check_singles(values, 2),
        check_singles(values, 3),
        check_singles(values, 4),
        check_singles(values, 5),
        check_singles(values, 6),
        check_three_of_kind(values),
        check_four_of_kind(values),
        check_five_of_kind(values),
        check_full_house(values),
        check_straight(values)
    )
    return high_score

# Add all occurrences of goal value
def check_singles(dice, goal):
    score = 0
    score = sum(value for value in dice if value == goal)
    return score

# Check for three of a kind (score = 30)
def check_three_of_kind(dice):
    score = 0
    for i in range(len(dice) - 2):
        if dice[i] == dice[i + 1] == dice[i + 2]:
            score = 30
            break
    return score

# Check for four of a kind (score = 40)
def check_four_of_kind(dice):
    score = 0
    for i in range(len(dice) - 3):
        if dice[i] == dice[i + 1] == dice[i + 2] == dice[i + 3]:
            score = 40
            break
    return score

# Check for five of a kind (score = 50)
def check_five_of_kind(dice):
    score = 0
    if len(set(dice)) == 1:
        score = 50
    return score

# Check for full house (score = 35)
def check_full_house(dice):
    score = 0
    if len(set(dice)) == 2 and (dice.count(dice[0]) == 2 or dice.count(dice[0]) == 3):
        score = 35
    return score

# Check for straight (score = 45)
def check_straight(dice):
    score = 0
    if set(dice) == {1, 2, 3, 4, 5} or set(dice) == {2, 3, 4, 5, 6}:
        score = 45
    return score

if __name__ == '__main__':  
    dice = [int(val) for val in input().split()]
    dice.sort()
    high_score = find_high_score(dice)
    print(f'High score: {high_score}')
