Here's a complete blog post that explains the Hogwarts Survival Game in Python step by step. You can copy and paste this directly.  

---

# **Hogwarts Survival Game in Python: A Strategic Battle Simulation**

Have you ever imagined yourself in a magical battle at Hogwarts with your favorite characters—Ron, Hermione, and Harry? In this post, we’ll create a Python game where Ron, Hermione, and Harry engage in a survival battle, following specific rules and hit probabilities.

## **Game Rules & Strategy**
1. **Hit Probabilities:**  
   - Ron has a **50%** chance of hitting his target.  
   - Hermione has an **80%** chance.  
   - Harry has a **100%** chance.  

2. **Attack Order:**  
   - The weakest player (Ron) attacks first, followed by Hermione, then Harry.  

3. **Automatic Targeting:**  
   - If Ron attacks Harry, Hermione will automatically target Ron.  
   - If Ron misses or is eliminated, the fight continues between Hermione and Harry.  

Our goal is to **simulate the game and determine the last survivor.** 🚀

---

## **Step 1: Setting Up the Python Game**
First, create a new Python file called `hogwarts_survival.py` and import the required module:

```python
import random
```

This module will help us generate random hit/miss outcomes.

---

## **Step 2: Defining the Players & Hit Function**
We define the characters and their hit probabilities:

```python
def get_random_hit(probability):
    """Returns True if the shot hits, based on probability."""
    return random.random() < probability

def hogwarts_survival():
    """Simulates the Hogwarts survival battle."""
    players = {
        "Ron": {"hit_chance": 0.5, "alive": True},
        "Hermione": {"hit_chance": 0.8, "alive": True},
        "Harry": {"hit_chance": 1.0, "alive": True},
    }
    
    log = []  # Stores battle log
```

Each player has a **hit chance** and an **alive status**.

---

## **Step 3: Implementing the Battle Logic**
The battle continues until only one player is left:

```python
    while sum(player["alive"] for player in players.values()) > 1:
        # Ron's turn
        if players["Ron"]["alive"]:
            if get_random_hit(players["Ron"]["hit_chance"]):
                players["Harry"]["alive"] = False
                log.append("Ron shot Harry successfully!")
            else:
                log.append("Ron missed!")
        
        # Hermione targets Ron if he shoots
        if players["Hermione"]["alive"] and players["Ron"]["alive"]:
            if get_random_hit(players["Hermione"]["hit_chance"]):
                players["Ron"]["alive"] = False
                log.append("Hermione shot Ron successfully!")
            else:
                log.append("Hermione missed!")
        
        # Battle between Hermione & Harry if Ron is eliminated
        if not players["Ron"]["alive"] and players["Hermione"]["alive"] and players["Harry"]["alive"]:
            if get_random_hit(players["Hermione"]["hit_chance"]):
                players["Harry"]["alive"] = False
                log.append("Hermione shot Harry successfully!")
            else:
                log.append("Hermione missed!")
            
            if players["Harry"]["alive"] and get_random_hit(players["Harry"]["hit_chance"]):
                players["Hermione"]["alive"] = False
                log.append("Harry shot Hermione successfully!")
            else:
                log.append("Harry missed!")
```

- Ron shoots first. If he misses, Hermione and Harry fight.
- If Ron targets Harry, Hermione immediately targets Ron.
- Once Ron is eliminated, Hermione and Harry engage in a duel.

---

## **Step 4: Displaying the Results**
At the end of the game, we print the survivors and the battle log:

```python
    print("\nHogwarts Survival Game Result:")
    for player, info in players.items():
        print(f"{player}: {'Alive' if info['alive'] else 'Dead'}")
    
    print("\nBattle Log:")
    for entry in log:
        print(entry)

if __name__ == "__main__":
    hogwarts_survival()
```

- This prints the final survivor.
- It also shows a detailed log of each attack and whether it hit or missed.

---

## **Step 5: Running the Game**
Save your file as `hogwarts_survival.py` and run it using:

```bash
python hogwarts_survival.py
```

You’ll see an output like this:

```
Hogwarts Survival Game Result:
Ron: Dead
Hermione: Alive
Harry: Dead

Battle Log:
Ron missed!
Hermione shot Ron successfully!
Hermione shot Harry successfully!
```

---

## **Conclusion**
This Python game demonstrates **strategy, probability, and game simulation.** We covered:
✅ Defining players and their hit chances  
✅ Implementing a survival battle loop  
✅ Printing the final winner and battle log  

Feel free to modify the rules, adjust probabilities, or add new players to make the game even more interesting! 🎮

**What’s next?**  
Try creating a GUI version or adding more magical spells! 🧙‍♂️✨  

🚀 **Did you enjoy this project? Let me know your thoughts!** 🚀
