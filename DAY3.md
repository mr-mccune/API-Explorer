# Day 3: Working with Nested JSON Data

## Python API Explorer Project

Yesterday, you learned how to request data from the PokéAPI and display simple values like a Pokémon's name, ID, height, and weight.

Today, you will learn how to work with more complicated API data.

Many APIs do not just return simple values. They often return **lists inside dictionaries** and **dictionaries inside lists**.

This is called **nested data**.

By the end of today, your Pokédex program will be able to display:

- Pokémon name
- ID
- Height
- Weight
- Types
- Abilities
- Base stats

---

## Day 3 Goal

By the end of today, you should be able to:

- Understand that JSON data can be nested
- Access lists inside dictionaries
- Access dictionaries inside lists
- Use loops to display repeated API data
- Display a Pokémon's types
- Display a Pokémon's abilities
- Display a Pokémon's base stats
- Make your output cleaner and easier to read

---

## Review from Day 2

On Day 2, your code looked similar to this:

```python
import requests

pokemon_name = input("Enter a Pokémon name: ").lower()

url = f"https://pokeapi.co/api/v2/pokemon/{pokemon_name}"

response = requests.get(url)

if response.status_code == 200:
    data = response.json()

    print("\n--- Pokémon Info ---")
    print("Name:", data["name"].title())
    print("ID:", data["id"])
    print("Height:", data["height"])
    print("Weight:", data["weight"])

else:
    print("Pokémon not found.")
```

This works because these values are easy to access:

```python
data["name"]
data["id"]
data["height"]
data["weight"]
```

Today, we will work with more complex values like:

```python
data["types"]
data["abilities"]
data["stats"]
```

---

# Step 1: Create Your Day 3 File

Create a new Python file named:

```text
api_day_3.py
```

Copy your working Day 2 code into this new file.

This lets you keep your Day 2 work safe while building the next version of your program.

---

# Step 2: Print the Types Data

Inside your `if response.status_code == 200:` block, add this line:

```python
print(data["types"])
```

Run your program with:

```text
pikachu
```

You should see something that looks more complicated than a simple name or number.

It may look similar to this:

```text
[{'slot': 1, 'type': {'name': 'electric', 'url': 'https://pokeapi.co/api/v2/type/13/'}}]
```

Do not worry if this looks confusing at first.

The important idea is this:

> `data["types"]` is a list.

That means we can loop through it.

---

# Step 3: Loop Through the Types

Replace your temporary `print(data["types"])` line with this:

```python
print("\nTypes:")

for type_info in data["types"]:
    print("-", type_info["type"]["name"])
```

Test your program with:

```text
pikachu
```

You should see:

```text
Types:
- electric
```

Now test your program with:

```text
charizard
```

You should see:

```text
Types:
- fire
- flying
```

Some Pokémon have one type.

Some Pokémon have two types.

That is why a loop is useful.

---

# Step 4: Understand the Types Code

Look closely at this code:

```python
for type_info in data["types"]:
    print("-", type_info["type"]["name"])
```

This part:

```python
data["types"]
```

gets the list of types.

This part:

```python
for type_info in data["types"]:
```

loops through each item in the list.

This part:

```python
type_info["type"]["name"]
```

goes inside the nested dictionary to find the type name.

The path is:

```text
data → types → each item → type → name
```

---

# Step 5: Display the Abilities

Now we will do something similar for abilities.

First, try printing the full abilities data:

```python
print(data["abilities"])
```

You will see that abilities are also stored in a list.

Replace that test line with this:

```python
print("\nAbilities:")

for ability_info in data["abilities"]:
    print("-", ability_info["ability"]["name"])
```

Test your program.

Example output for Pikachu may look like this:

```text
Abilities:
- static
- lightning-rod
```

---

# Step 6: Display the Base Stats

The API also gives us base stats.

These include values like:

- hp
- attack
- defense
- special-attack
- special-defense
- speed

First, try printing the full stats data:

```python
print(data["stats"])
```

You will see that it is a list of dictionaries.

Now replace that test line with this:

```python
print("\nBase Stats:")

for stat_info in data["stats"]:
    stat_name = stat_info["stat"]["name"]
    stat_value = stat_info["base_stat"]
    print(f"- {stat_name}: {stat_value}")
```

Example output:

```text
Base Stats:
- hp: 35
- attack: 55
- defense: 40
- special-attack: 50
- special-defense: 50
- speed: 90
```

---

# Step 7: Understand the Stats Code

Look closely at this code:

```python
for stat_info in data["stats"]:
    stat_name = stat_info["stat"]["name"]
    stat_value = stat_info["base_stat"]
    print(f"- {stat_name}: {stat_value}")
```

This part loops through each stat:

```python
for stat_info in data["stats"]:
```

This line gets the stat name:

```python
stat_name = stat_info["stat"]["name"]
```

This line gets the stat number:

```python
stat_value = stat_info["base_stat"]
```

This line prints both values in a clean format:

```python
print(f"- {stat_name}: {stat_value}")
```

---

# Step 8: Combine Everything

Your program should now display simple values and nested values.

It should show:

- Name
- ID
- Height
- Weight
- Types
- Abilities
- Base stats

Your output should look similar to this:

```text
Enter a Pokémon name: charizard

--- Pokémon Info ---
Name: Charizard
ID: 6
Height: 17
Weight: 905

Types:
- fire
- flying

Abilities:
- blaze
- solar-power

Base Stats:
- hp: 78
- attack: 84
- defense: 78
- special-attack: 109
- special-defense: 85
- speed: 100
```

---

# Final Day 3 Code

By the end of today, your code should look similar to this:

```python
import requests

pokemon_name = input("Enter a Pokémon name: ").lower()

url = f"https://pokeapi.co/api/v2/pokemon/{pokemon_name}"

response = requests.get(url)

if response.status_code == 200:
    data = response.json()

    print("\n--- Pokémon Info ---")
    print("Name:", data["name"].title())
    print("ID:", data["id"])
    print("Height:", data["height"])
    print("Weight:", data["weight"])

    print("\nTypes:")
    for type_info in data["types"]:
        print("-", type_info["type"]["name"])

    print("\nAbilities:")
    for ability_info in data["abilities"]:
        print("-", ability_info["ability"]["name"])

    print("\nBase Stats:")
    for stat_info in data["stats"]:
        stat_name = stat_info["stat"]["name"]
        stat_value = stat_info["base_stat"]
        print(f"- {stat_name}: {stat_value}")

else:
    print("Pokémon not found.")
```

---

# What You Learned Today

Today you learned that API data can be nested.

Nested data means data can be stored inside other data.

For example:

- A dictionary can contain a list
- A list can contain dictionaries
- A dictionary can contain another dictionary

You also learned how to use loops to display multiple pieces of API data.

---

# Important Code Review

## Accessing a simple dictionary value

```python
data["name"]
```

This gets one simple value.

---

## Accessing a list inside a dictionary

```python
data["types"]
```

This gets the list of Pokémon types.

---

## Looping through a list

```python
for type_info in data["types"]:
```

This loops through each type in the list.

---

## Accessing a nested dictionary value

```python
type_info["type"]["name"]
```

This gets the name of the type from inside a nested dictionary.

---

## Using an f-string for clean output

```python
print(f"- {stat_name}: {stat_value}")
```

This lets you print variables inside a string.

---

# Common Mistakes to Watch For

## Mistake 1: Forgetting that some data is a list

Incorrect:

```python
print(data["types"]["name"])
```

Correct:

```python
for type_info in data["types"]:
    print(type_info["type"]["name"])
```

`data["types"]` is a list, so we need to loop through it.

---

## Mistake 2: Forgetting quotation marks around keys

Incorrect:

```python
print(type_info[type][name])
```

Correct:

```python
print(type_info["type"]["name"])
```

Dictionary keys need quotation marks when they are strings.

---

## Mistake 3: Indentation errors

Incorrect:

```python
for ability_info in data["abilities"]:
print(ability_info["ability"]["name"])
```

Correct:

```python
for ability_info in data["abilities"]:
    print(ability_info["ability"]["name"])
```

The code inside a loop must be indented.

---

## Mistake 4: Using the wrong variable name

Incorrect:

```python
for ability_info in data["abilities"]:
    print(type_info["ability"]["name"])
```

Correct:

```python
for ability_info in data["abilities"]:
    print(ability_info["ability"]["name"])
```

Make sure the variable inside the loop matches the variable you created in the loop line.

---

# Student Task Checklist

Before you turn in your work, make sure you completed all of these:

- [ ] Created a file named `api_day_3.py`
- [ ] Copied your working Day 2 code
- [ ] Displayed the Pokémon's name
- [ ] Displayed the Pokémon's ID
- [ ] Displayed the Pokémon's height
- [ ] Displayed the Pokémon's weight
- [ ] Used a loop to display all types
- [ ] Used a loop to display all abilities
- [ ] Used a loop to display all base stats
- [ ] Tested with at least 3 real Pokémon
- [ ] Tested with 1 fake Pokémon
- [ ] Made sure the program does not crash
- [ ] Made sure the output is clean and readable

---

# Reflection Questions

Answer these questions in a comment at the bottom of your Python file.

```python
# Reflection Questions:
# 1. What does nested data mean?
# 2. Why do we need a loop for data["types"]?
# 3. What does type_info["type"]["name"] do?
# 4. What was harder today: types, abilities, or stats? Why?
# 5. How do loops make API data easier to display?
```

---

# Bonus Challenge 1: Display Types on One Line

Instead of this:

```text
Types:
- fire
- flying
```

Try to display this:

```text
Types: fire, flying
```

Hint:

You can create an empty list, add each type, and then use `join()`.

```python
type_names = []

for type_info in data["types"]:
    type_names.append(type_info["type"]["name"])

print("Types:", ", ".join(type_names))
```

---

# Bonus Challenge 2: Find the Strongest Stat

Try to find which stat has the highest value.

Example output:

```text
Strongest Stat: speed with 90
```

Hint:

You will need variables to keep track of the highest stat name and highest stat value.

---

# Bonus Challenge 3: Clean Up the Stat Names

The API gives some stat names with hyphens.

Example:

```text
special-attack
special-defense
```

Try to make them look better:

```text
Special Attack
Special Defense
```

Hint:

You can use `.replace()` and `.title()`.

```python
clean_name = stat_name.replace("-", " ").title()
```

---

# Bonus Challenge 4: Add a Function

Create a function named `display_pokemon_info`.

Move your print statements into that function.

Example:

```python
def display_pokemon_info(data):
    print("\n--- Pokémon Info ---")
    print("Name:", data["name"].title())
    print("ID:", data["id"])
    print("Height:", data["height"])
    print("Weight:", data["weight"])
```

Then call the function after you get the JSON data:

```python
display_pokemon_info(data)
```

Functions help organize your code and make it easier to read.

---

# Exit Ticket

Before you finish, answer these three questions:

```text
1. What is one example of nested data from today's lesson?
2. Why did we use loops with types, abilities, and stats?
3. What is one feature you want to add to your Pokédex app tomorrow?
```

---

# Day 3 Final Goal

By the end of today, your program should display clean Pokémon information using both simple dictionary values and nested JSON data.

Your program should be able to turn complicated API data into readable output for a user.

Tomorrow, we will start organizing the program into functions and improving it into a more complete app.
