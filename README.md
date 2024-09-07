# Adventure-Game
Task # 3
print("Welcome to Game")
print("Collect all the items ('Key', 'Knife', 'Shield', 'Book', 'Ring') and win")
print("Use 'Collect' to pick up the items")

rooms = {
    'Entrance': {'North': 'Living Room', 'East': 'Kitchen', 'item': None},
    'Living Room': {'South': 'Entrance', 'East': 'Bedroom', 'item': 'Key'},
    'Kitchen': {'West': 'Entrance', 'item': 'Knife'},
    'Bedroom': {'West': 'Living Room', 'North': 'Bathroom', 'item': 'Shield'},
    'Bathroom': {'South': 'Bedroom', 'item': 'Ring'},
    'Drawing Room': {'item': 'Villain'},  # Encounter with the villain
}

required_items = ['Key', 'Knife', 'Shield', 'Ring']

current_room = 'Entrance'
collected_items = []


def show_status():
    print(f"\nYou are in the {current_room}.")
    if rooms[current_room]['item']:
        print(f"You see a {rooms[current_room]['item']}.")
    print(f"Inventory: {collected_items}")


def move(direction):
    global current_room
    if direction in rooms[current_room]:
        current_room = rooms[current_room][direction]
    else:
        print("You can't go that way!")


def collect_item():
    item = rooms[current_room].get('item')
    if item and item != 'Villain':
        collected_items.append(item)
        rooms[current_room]['item'] = None
        print(f"You picked up {item}.")
    elif item == 'Villain':
        print("Oh no! You've encountered the villain and lost the game.")
        return False
    return True


while True:
    show_status()
    command = input("\nEnter a direction (North, South, East, West) or 'Collect': ").capitalize()

    if command in ['North', 'South', 'East', 'West']:
        move(command)
    elif command == 'Collect':
        if not collect_item():
            break
    else:
        print("Invalid command.")

    if set(collected_items) == set(required_items):
        print("Congratulations! You've collected all the items and won the game!")
        break
