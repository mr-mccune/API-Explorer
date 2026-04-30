# Day 4: Finish and Polish Your API Explorer App

## Python API Explorer Project

Welcome to Day 4!

Over the last few days, you learned how to:

- Send a request to an API
- Check the status code
- Convert a response into JSON
- Pull specific values from a dictionary
- Loop through lists inside nested JSON data
- Display Pokémon types, abilities, and stats

Today, you will turn your code into a more complete program.

Your goal is to make your API Explorer feel like a real app.

---

## Day 4 Goal

By the end of today, your program should:

- Ask the user for a Pokémon name or ID
- Get data from the PokéAPI
- Display clean Pokémon information
- Show types, abilities, and base stats
- Use at least one function
- Let the user search again or quit
- Handle invalid searches without crashing
- Include at least one bonus feature

---

## Review: What We Have So Far

Your program may currently look something like this:

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

This works, but today we are going to make it better.

---

# Step 1: Create Your Day 4 File

Create a new Python file named:

```text
api_day_4.py
```

You may copy your Day 3 code into this file as your starting point.

---

# Step 2: Add a Welcome Message

A real program should tell the user what it does.

At the start of your program, add:

```python
print("Welcome to the Python Pokédex!")
print("Search for Pokémon and view their information.")
```

Example output:

```text
Welcome to the Python Pokédex!
Search for Pokémon and view their information.
```

---

# Step 3: Add a Function to Get Pokémon Data

Functions help us organize our code.

Create a function named `get_pokemon_data`.

```python
def get_pokemon_data(pokemon_name):
    url = f"https://pokeapi.co/api/v2/pokemon/{pokemon_name.lower()}"
    response = requests.get(url)

    if response.status_code == 200:
        return response.json()
    else:
        return None
```

This function does three things:

1. Builds the API URL
2. Sends the request
3. Returns the data if the Pokémon is found

If the Pokémon is not found, it returns `None`.

---

## What Does `return None` Mean?

`None` means “nothing.”

If the API cannot find the Pokémon, we do not get useful data back.

So this:

```python
return None
```

means:

> The Pokémon was not found, so there is no data to display.

Later, we can check for that with an `if` statement.

---

# Step 4: Add a Function to Display Pokémon Data

Create a function named `display_pokemon`.

```python
def display_pokemon(data):
    print("\n========================")
    print("      Pokémon Info")
    print("========================")

    print("Name:", data["name"].title())
    print("ID:", data["id"])
    print("Height:", data["height"])
    print("Weight:", data["weight"])

    print("\nTypes:")
    for type_info in data["types"]:
        print("-", type_info["type"]["name"].title())

    print("\nAbilities:")
    for ability_info in data["abilities"]:
        print("-", ability_info["ability"]["name"].title())

    print("\nBase Stats:")
    for stat_info in data["stats"]:
        stat_name = stat_info["stat"]["name"]
        stat_value = stat_info["base_stat"]
        print(f"- {stat_name.title()}: {stat_value}")
```

This function takes the Pokémon data and displays it in a clean format.

---

# Step 5: Add a Replay Loop

Right now, your program probably only lets the user search once.

A better program lets the user keep searching until they choose to quit.

Add this loop:

```python
while True:
    pokemon_name = input("\nEnter a Pokémon name or ID, or type 'quit': ").lower()

    if pokemon_name == "quit":
        print("Goodbye!")
        break

    data = get_pokemon_data(pokemon_name)

    if data:
        display_pokemon(data)
    else:
        print("Pokémon not found. Please try again.")
```

This loop keeps the program running.

The program stops when the user types:

```text
quit
```

---

## How the Loop Works

```python
while True:
```

This creates a loop that keeps running.

```python
if pokemon_name == "quit":
```

This checks if the user wants to quit.

```python
break
```

This stops the loop.

```python
data = get_pokemon_data(pokemon_name)
```

This calls the function that gets data from the API.

```python
if data:
```

This checks if the API returned real data.

If data exists, we display it.

If data does not exist, we show an error message.

---

# Step 6: Put It All Together

Your program should now have:

1. An import statement
2. A function that gets data
3. A function that displays data
4. A welcome message
5. A loop that lets the user search again
6. Error handling for invalid searches

---

# Step 7: Test Your Program

Test your program with at least 5 real Pokémon.

Try these:

```text
pikachu
charizard
bulbasaur
squirtle
mewtwo
eevee
snorlax
lucario
gengar
dragonite
```

Also test with at least 2 invalid searches.

Try:

```text
notapokemon
abc123
```

Your program should not crash.

It should show a helpful message.

---

# Step 8: Add One Bonus Feature

Choose at least one bonus feature from the list below.

You may choose an easier, medium, or advanced feature.

---

## Bonus Feature Option 1: Show Base Experience

Add this line inside the `display_pokemon` function:

```python
print("Base Experience:", data["base_experience"])
```

This displays another value from the API.

---

## Bonus Feature Option 2: Show the Pokémon’s Strongest Stat

Create a variable to track the strongest stat.

Add this inside the `display_pokemon` function after the base stats loop, or create a new function for it.

```python
strongest_stat = ""
strongest_value = 0

for stat_info in data["stats"]:
    stat_name = stat_info["stat"]["name"]
    stat_value = stat_info["base_stat"]

    if stat_value > strongest_value:
        strongest_value = stat_value
        strongest_stat = stat_name

print("\nStrongest Stat:")
print(f"{strongest_stat.title()}: {strongest_value}")
```

Example output:

```text
Strongest Stat:
Speed: 100
```

---

## Bonus Feature Option 3: Calculate a Battle Score

Create a simple battle score using attack, defense, and speed.

```python
battle_score = 0

for stat_info in data["stats"]:
    stat_name = stat_info["stat"]["name"]
    stat_value = stat_info["base_stat"]

    if stat_name == "attack" or stat_name == "defense" or stat_name == "speed":
        battle_score += stat_value

print("\nBattle Score:", battle_score)
```

This is not an official Pokémon score.

It is just a score your program creates.

---

## Bonus Feature Option 4: Save Favorite Pokémon to a File

Ask the user if they want to save the Pokémon to a favorites file.

```python
save = input("Save this Pokémon to favorites? yes/no: ").lower()

if save == "yes":
    with open("favorites.txt", "a") as file:
        file.write(data["name"].title() + "\n")

    print("Saved to favorites.txt!")
```

This creates a file named:

```text
favorites.txt
```

The `"a"` means append.

Append means the program adds to the file instead of replacing the file.

---

## Bonus Feature Option 5: Compare Two Pokémon

This is more advanced.

The user enters two Pokémon.

The program gets data for both and compares their battle scores.

Example idea:

```python
first = input("Enter the first Pokémon: ")
second = input("Enter the second Pokémon: ")

first_data = get_pokemon_data(first)
second_data = get_pokemon_data(second)
```

You would need to create a function that calculates a score and returns it.

Example:

```python
def calculate_battle_score(data):
    battle_score = 0

    for stat_info in data["stats"]:
        stat_name = stat_info["stat"]["name"]
        stat_value = stat_info["base_stat"]

        if stat_name == "attack" or stat_name == "defense" or stat_name == "speed":
            battle_score += stat_value

    return battle_score
```

Then compare the scores.

---

# Step 9: Make Your Output Look Clean

Your program should be easy to read.

You may add:

- Blank lines
- Headings
- Separators
- Title case
- Clear labels

Example:

```python
print("\n========================")
print("      Pokémon Info")
print("========================")
```

Good output matters.

A program is better when users can understand it easily.

---

# Step 10: Add Comments

Add comments to explain your code.

Example:

```python
# This function gets Pokémon data from the API
def get_pokemon_data(pokemon_name):
    url = f"https://pokeapi.co/api/v2/pokemon/{pokemon_name.lower()}"
    response = requests.get(url)
```

You do not need a comment on every line.

Add comments for important sections.

---

# Final Project Requirements

Your final program must include:

- [ ] A file named `api_day_4.py`
- [ ] `import requests`
- [ ] User input for a Pokémon name or ID
- [ ] An API request using `requests.get()`
- [ ] A status code check
- [ ] JSON conversion using `response.json()`
- [ ] Clean output for the user
- [ ] Pokémon name
- [ ] Pokémon ID
- [ ] Height
- [ ] Weight
- [ ] Types
- [ ] Abilities
- [ ] Base stats
- [ ] At least one function
- [ ] A loop that lets the user search again
- [ ] Error handling for invalid searches
- [ ] At least one bonus feature
- [ ] Comments explaining important parts of the code

---

# Example Final Output

```text
Welcome to the Python Pokédex!
Search for Pokémon and view their information.

Enter a Pokémon name or ID, or type 'quit': charizard

========================
      Pokémon Info
========================
Name: Charizard
ID: 6
Height: 17
Weight: 905

Types:
- Fire
- Flying

Abilities:
- Blaze
- Solar-Power

Base Stats:
- Hp: 78
- Attack: 84
- Defense: 78
- Special-Attack: 109
- Special-Defense: 85
- Speed: 100

Enter a Pokémon name or ID, or type 'quit': notapokemon
Pokémon not found. Please try again.

Enter a Pokémon name or ID, or type 'quit': quit
Goodbye!
```

---

# Common Mistakes to Watch For

## Mistake 1: Forgetting to Call the Function

Incorrect:

```python
get_pokemon_data
```

Correct:

```python
data = get_pokemon_data(pokemon_name)
```

Functions need parentheses to run.

---

## Mistake 2: Forgetting to Return the Data

Incorrect:

```python
def get_pokemon_data(pokemon_name):
    url = f"https://pokeapi.co/api/v2/pokemon/{pokemon_name}"
    response = requests.get(url)
    response.json()
```

Correct:

```python
def get_pokemon_data(pokemon_name):
    url = f"https://pokeapi.co/api/v2/pokemon/{pokemon_name}"
    response = requests.get(url)

    if response.status_code == 200:
        return response.json()
```

If you do not use `return`, the function does not send the data back.

---

## Mistake 3: Putting the Loop in the Wrong Place

Make sure your functions are written before the main loop.

Good structure:

```python
import requests

def get_pokemon_data(pokemon_name):
    # function code here

def display_pokemon(data):
    # function code here

while True:
    # main program code here
```

---

## Mistake 4: Not Indenting Code Inside the Loop

Incorrect:

```python
while True:
pokemon_name = input("Enter a Pokémon: ")
```

Correct:

```python
while True:
    pokemon_name = input("Enter a Pokémon: ")
```

Python uses indentation to understand what belongs inside the loop.

---

## Mistake 5: Trying to Display Data That Does Not Exist

Incorrect:

```python
data = get_pokemon_data(pokemon_name)
display_pokemon(data)
```

This might crash if the Pokémon is not found.

Better:

```python
data = get_pokemon_data(pokemon_name)

if data:
    display_pokemon(data)
else:
    print("Pokémon not found.")
```

Always check that the data exists before using it.

---

# Reflection Questions

Answer these questions in a comment at the bottom of your Python file.

```python
# Reflection Questions:
# 1. Why are functions useful in this project?
# 2. What does return do inside a function?
# 3. Why did we use a while loop?
# 4. What happens when the user types quit?
# 5. What bonus feature did you add?
# 6. What was the hardest part of working with API data?
# 7. How could APIs be used in a real app, website, or game?
```

---

# 50-Point Rubric

| Category | Points |
|---|---:|
| Program successfully connects to the API | 8 |
| User can search by Pokémon name or ID | 6 |
| Program checks status code and handles invalid searches | 6 |
| Program displays name, ID, height, and weight | 6 |
| Program displays types, abilities, and base stats using loops | 8 |
| Program uses at least one function correctly | 6 |
| Program uses a loop to let the user search again | 4 |
| Output is clean and easy to read | 3 |
| Code includes helpful comments | 3 |
| **Total** | **50** |

---

# Bonus Points

You may earn up to 10 bonus points.

| Bonus Feature | Points |
|---|---:|
| Shows strongest stat | +3 |
| Adds battle score | +3 |
| Saves favorites to a file | +4 |
| Compares two Pokémon | +5 |
| Excellent design, formatting, or creativity | +3 |

Maximum bonus: 10 points.

---

# Final Submission Checklist

Before submitting, make sure:

- [ ] Your file is named `api_day_4.py`
- [ ] Your program runs without errors
- [ ] Your program works with real Pokémon
- [ ] Your program handles fake Pokémon
- [ ] Your program lets the user search more than once
- [ ] Your program quits when the user types `quit`
- [ ] Your program uses at least one function
- [ ] Your program displays clean information
- [ ] You added at least one bonus feature
- [ ] You answered the reflection questions

---

# Final Day 4 Goal

By the end of today, you should have a working Python Pokédex program.

Your program should feel like a small real app.

It should:

- Ask the user what they want
- Get live data from the internet
- Organize that data
- Display it clearly
- Handle mistakes
- Let the user keep using it

That is exactly what many real apps do with APIs.
