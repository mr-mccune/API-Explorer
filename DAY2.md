# Day 2: Reading JSON Data from an API

## Python API Explorer Project

Yesterday, we learned that Python can request information from an API.

Today, we will learn how to pull specific pieces of information out of the API response.

Instead of printing the entire JSON response, we will display only the information we want the user to see.

---

## Day 2 Goal

By the end of today, you should be able to:

- Make a request to an API using Python
- Convert the response into JSON
- Access specific values from a dictionary
- Use user input to search for a Pokémon
- Display clean, readable output
- Handle a Pokémon that is not found

---

## Review from Day 1

On Day 1, we used code like this:

```python
import requests

url = "https://pokeapi.co/api/v2/pokemon/pikachu"

response = requests.get(url)

print(response.status_code)
print(response.json())
```

This worked, but it printed a lot of information.

Today, we want to make the output easier to read.

Instead of printing everything, we will choose specific pieces of data.

---

# Step 1: Create Your Day 2 File

Create a new Python file named:

```text
api_day_2.py
```

At the top of the file, import the `requests` library:

```python
import requests
```

The `requests` library lets Python get information from websites and APIs.

---

# Step 2: Ask the User for a Pokémon

Instead of always searching for Pikachu, we want the user to choose a Pokémon.

Add this code:

```python
pokemon_name = input("Enter a Pokémon name: ").lower()
```

This does two things:

1. It asks the user to type a Pokémon name.
2. It converts the name to lowercase.

Example:

```text
Enter a Pokémon name: Charizard
```

Python stores it as:

```text
charizard
```

This helps because the API expects lowercase names.

---

# Step 3: Build the API URL

Now we need to create the API URL using the Pokémon name the user typed.

Add this code:

```python
url = f"https://pokeapi.co/api/v2/pokemon/{pokemon_name}"
```

This is called an **f-string**.

An f-string lets us place a variable inside a string.

If the user types:

```text
pikachu
```

The URL becomes:

```text
https://pokeapi.co/api/v2/pokemon/pikachu
```

If the user types:

```text
charizard
```

The URL becomes:

```text
https://pokeapi.co/api/v2/pokemon/charizard
```

---

# Step 4: Send the API Request

Now we need Python to request information from the API.

Add this code:

```python
response = requests.get(url)
```

This sends a request to the PokéAPI.

The API will send back a response.

---

# Step 5: Check the Status Code

Before we use the data, we should check if the request worked.

Add this code:

```python
if response.status_code == 200:
    print("Pokémon found!")
else:
    print("Pokémon not found.")
```

A status code tells us what happened with the request.

| Status Code | Meaning |
|---|---|
| 200 | The request worked |
| 404 | The Pokémon was not found |
| 500 | Something went wrong on the server |

A status code of `200` means the API found the Pokémon.

A status code of `404` means the API could not find what we searched for.

---

# Step 6: Convert the Response to JSON

If the request worked, we need to convert the response into JSON data.

Update your `if` statement like this:

```python
if response.status_code == 200:
    data = response.json()
    print("Pokémon found!")
else:
    print("Pokémon not found.")
```

This line is important:

```python
data = response.json()
```

It takes the response from the API and converts it into data Python can work with.

Most API data works like dictionaries and lists.

---

# Step 7: Print the Pokémon’s Name

Now we can pull out one specific piece of information.

Add this inside the `if` statement:

```python
print("Name:", data["name"])
```

Your code should now look like this:

```python
import requests

pokemon_name = input("Enter a Pokémon name: ").lower()

url = f"https://pokeapi.co/api/v2/pokemon/{pokemon_name}"

response = requests.get(url)

if response.status_code == 200:
    data = response.json()

    print("Name:", data["name"])
else:
    print("Pokémon not found.")
```

Run your program and test it with:

```text
pikachu
```

You should see:

```text
Name: pikachu
```

---

# Step 8: Make the Name Look Better

The API gives us the Pokémon name in lowercase.

We can use `.title()` to make it look better.

Change this:

```python
print("Name:", data["name"])
```

To this:

```python
print("Name:", data["name"].title())
```

Now the output should look like this:

```text
Name: Pikachu
```

---

# Step 9: Print More Information

Now add more values from the API data.

Inside the `if` statement, add:

```python
print("ID:", data["id"])
print("Height:", data["height"])
print("Weight:", data["weight"])
```

Your code should now look like this:

```python
import requests

pokemon_name = input("Enter a Pokémon name: ").lower()

url = f"https://pokeapi.co/api/v2/pokemon/{pokemon_name}"

response = requests.get(url)

if response.status_code == 200:
    data = response.json()

    print("Name:", data["name"].title())
    print("ID:", data["id"])
    print("Height:", data["height"])
    print("Weight:", data["weight"])
else:
    print("Pokémon not found.")
```

---

# Step 10: Improve the Output

Right now the output works, but we can make it easier to read.

Update the print statements like this:

```python
print("\n--- Pokémon Info ---")
print("Name:", data["name"].title())
print("ID:", data["id"])
print("Height:", data["height"])
print("Weight:", data["weight"])
```

The `\n` adds a blank line before the heading.

Example output:

```text
Enter a Pokémon name: charizard

--- Pokémon Info ---
Name: Charizard
ID: 6
Height: 17
Weight: 905
```

---

# Step 11: Test With Multiple Pokémon

Test your program with at least 3 real Pokémon.

Try these:

```text
pikachu
charizard
bulbasaur
squirtle
eevee
snorlax
lucario
gengar
dragonite
mewtwo
```

Make sure your program works for each one.

---

# Step 12: Test With a Fake Pokémon

Now test your program with a fake Pokémon name.

Example:

```text
notapokemon
```

Your program should not crash.

It should display:

```text
Pokémon not found.
```

This is called **error handling**.

Good programs should handle mistakes without crashing.

---

# Final Day 2 Code

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

else:
    print("Pokémon not found.")
```

---

# What You Learned Today

Today you learned how to:

- Ask the user for input
- Use the input inside an API URL
- Send an API request with Python
- Check if the request worked
- Convert the response into JSON
- Use dictionary keys to access specific data
- Display clean output for the user
- Handle invalid searches

---

# Important Code Review

## Getting user input

```python
pokemon_name = input("Enter a Pokémon name: ").lower()
```

This asks the user for a Pokémon name.

---

## Building the URL

```python
url = f"https://pokeapi.co/api/v2/pokemon/{pokemon_name}"
```

This uses the user’s Pokémon name inside the API URL.

---

## Sending the request

```python
response = requests.get(url)
```

This asks the API for data.

---

## Checking if the request worked

```python
if response.status_code == 200:
```

This checks if the Pokémon was found.

---

## Converting the response to JSON

```python
data = response.json()
```

This turns the API response into data Python can use.

---

## Accessing dictionary values

```python
data["name"]
data["id"]
data["height"]
data["weight"]
```

These pull specific values out of the API data.

---

# Common Mistakes to Watch For

## Mistake 1: Forgetting quotation marks around dictionary keys

Incorrect:

```python
print(data[name])
```

Correct:

```python
print(data["name"])
```

Dictionary keys that are words need quotation marks.

---

## Mistake 2: Trying to use `response` instead of `data`

Incorrect:

```python
print(response["name"])
```

Correct:

```python
data = response.json()
print(data["name"])
```

The `response` is the package from the API.

The JSON data is what we get after opening the package.

---

## Mistake 3: Forgetting to indent

Incorrect:

```python
if response.status_code == 200:
data = response.json()
print(data["name"])
```

Correct:

```python
if response.status_code == 200:
    data = response.json()
    print(data["name"])
```

Python uses indentation to know what belongs inside the `if` statement.

---

## Mistake 4: Searching for Pokémon with spaces

Some Pokémon names may not work if they have spaces or special characters.

For today, use simple names like:

```text
pikachu
charizard
eevee
snorlax
mewtwo
```

---

# Student Task Checklist

Before you turn in your work, make sure you completed all of these:

- [ ] Created a file named `api_day_2.py`
- [ ] Imported `requests`
- [ ] Asked the user for a Pokémon name
- [ ] Used an f-string to build the API URL
- [ ] Sent a request using `requests.get()`
- [ ] Checked if the status code was `200`
- [ ] Converted the response to JSON
- [ ] Displayed the Pokémon’s name
- [ ] Displayed the Pokémon’s ID
- [ ] Displayed the Pokémon’s height
- [ ] Displayed the Pokémon’s weight
- [ ] Tested with at least 3 real Pokémon
- [ ] Tested with 1 fake Pokémon
- [ ] Made sure the program does not crash

---

# Reflection Questions

Answer these questions in a comment at the bottom of your Python file.

```python
# Reflection Questions:
# 1. What does response.json() do?
# 2. What does data["name"] mean?
# 3. Why do we check response.status_code before using the data?
# 4. What is the difference between printing the entire JSON response and printing specific values?
# 5. What other Pokémon information would you like to display later?
```

---

# Bonus Challenge 1: Add Base Experience

Add one more value from the API response.

Inside your `if` statement, add:

```python
print("Base Experience:", data["base_experience"])
```

Example output:

```text
Base Experience: 112
```

---

# Bonus Challenge 2: Make the Output Look Better

Add lines or spacing to make your output cleaner.

Example:

```python
print("====================")
print("  Pokémon Info")
print("====================")
```

Example output:

```text
====================
  Pokémon Info
====================
Name: Pikachu
ID: 25
Height: 4
Weight: 60
```

---

# Bonus Challenge 3: Let the User Search Again

Try adding a `while` loop so the user can search more than once.

Example idea:

```python
while True:
    pokemon_name = input("Enter a Pokémon name or type quit: ").lower()

    if pokemon_name == "quit":
        print("Goodbye!")
        break
```

This is more advanced, but it will make your program feel more like a real app.

---

# Bonus Challenge 4: Add a Function

Try creating a function to display the Pokémon information.

Example:

```python
def display_pokemon(data):
    print("\n--- Pokémon Info ---")
    print("Name:", data["name"].title())
    print("ID:", data["id"])
    print("Height:", data["height"])
    print("Weight:", data["weight"])
```

Then you can call the function like this:

```python
display_pokemon(data)
```

Functions help keep your code organized.

---

# Exit Ticket

Before you finish, answer these three questions:

```text
1. What is one key you used from the JSON data?
2. Why should we check the status code before using the data?
3. What is one thing you want your final Pokédex app to display?
```

---

# Day 2 Final Goal

By the end of today, your program should no longer print the entire JSON response.

Instead, it should ask the user for a Pokémon and display clean information like this:

```text
--- Pokémon Info ---
Name: Pikachu
ID: 25
Height: 4
Weight: 60
```

Tomorrow, we will learn how to work with more complicated API data, including lists inside dictionaries.
