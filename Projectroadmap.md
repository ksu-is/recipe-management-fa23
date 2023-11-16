import json

def add_recipe():
    name = input("Enter recipe name: ")
    ingredients = input("Enter recipe ingredients (separated by commas): ")
    
 print("Enter recipe directions (type 'done' on a new line when finished):")
    directions = []
    while True:
        line = input()
        if line.lower() == "done":
            break
        directions.append(line)
    
   with open("recipes.json", "r") as f:
        data = json.load(f)
        data[name] = {"ingredients": ingredients.split(", "), "directions": directions}
    
  with open("recipes.json", "w") as f:
        json.dump(data, f)

def search_recipe():
    term = input("Enter search term: ")
    
 with open("recipes.json", "r") as f:
        data = json.load(f)
        for name, recipe in data.items():
            if term in name or term in recipe["ingredients"] or term in ' '.join(recipe["directions"]):
                print(f"Recipe: {name}")
                print(f"Ingredients: {', '.join(recipe['ingredients'])}")
                print("Directions:")
                for step in recipe['directions']:
                    print(step)
                print()

def main():
    while True:
        print("Select an option:")
        print("1. Add recipe")
        print("2. Search recipe")
        print("3. Quit")
        choice = input("> ")
        if choice == "1":
            add_recipe()
        elif choice == "2":
            search_recipe()
        elif choice == "3":
            break
        else:
            print("Invalid choice.")

if __name__ == "__main__":
    main()
