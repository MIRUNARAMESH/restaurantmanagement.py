# restaurantmanagement.py
class MenuItem:
    def __init__(self, name, price):
        self.name = name
        self.price = price

    def __repr__(self):
        return f"{self.name}: ${self.price:.2f}"

class Menu:
    def __init__(self):
        self.items = []

    def add_item(self, name, price):
        item = MenuItem(name, price)
        self.items.append(item)
        print(f"Added {item}")

    def remove_item(self, name):
        self.items = [item for item in self.items if item.name != name]
        print(f"Removed {name}")

    def update_item(self, name, new_name, new_price):
        for item in self.items:
            if item.name == name:
                item.name = new_name
                item.price = new_price
                print(f"Updated {item}")
                return
        print(f"Item {name} not found")

    def show_menu(self):
        for item in self.items:
            print(item)
class Order:
    def __init__(self, table_number):
        self.table_number = table_number
        self.items = []

    def add_item(self, item):
        self.items.append(item)
        print(f"Added {item} to table {self.table_number}'s order")

    def calculate_total(self):
        total = sum(item.price for item in self.items)
        print(f"Total for table {self.table_number}: ${total:.2f}")
        return total

    def show_order(self):
        for item in self.items:
            print(item)
def main():
    menu = Menu()
    orders = {}

    while True:
        print("\n1. Add Menu Item")
        print("\n2. Remove Menu Item")
        print("\n3. Update Menu Item")
        print("\n4. Show Menu")
        print("\n5. Take Order")
        print("\n6. Show Order")
        print("\n7. Calculate Total")
        print("\n8. Exit")

        choice = int(input("Enter choice: "))

        if choice == 1:
            name = input("Enter item name: ")
            price = float(input("Enter item price: "))
            menu.add_item(name, price)

        elif choice == 2:
            name = input("Enter item name to remove: ")
            menu.remove_item(name)

        elif choice == 3:
            name = input("Enter item name to update: ")
            new_name = input("Enter new item name: ")
            new_price = float(input("Enter new item price: "))
            menu.update_item(name, new_name, new_price)

        elif choice == 4:
            menu.show_menu()

        elif choice == 5:
            table_number = int(input("Enter table number: "))
            if table_number not in orders:
                orders[table_number] = Order(table_number)
            while True:
                name = input("Enter item name to order (or 'done' to finish): ")
                if name == 'done':
                    break
                for item in menu.items:
                    if item.name == name:
                        orders[table_number].add_item(item)
                        break
                else:
                    print("Item not found on the menu")

        elif choice == 6:
            table_number = int(input("Enter table number: "))
            if table_number in orders:
                orders[table_number].show_order()
            else:
                print("No order for this table")

        elif choice == 7:
            table_number = int(input("Enter table number: "))
            if table_number in orders:
                orders[table_number].calculate_total()
            else:
                print("No order for this table")

        elif choice == 8:
            break

        else:
            print("Invalid choice")

if __name__ == "__main__":
    main()
