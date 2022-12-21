# Single-Resposibility-Principle
## Overview
Each class should have a single responsibility, and that responsibility should be encapsulated by the class.
## Example
For example, consider a Character class that represents a player character in the game. This class might have a number of responsibilities, such as keeping track of the character's stats (such as health and level), managing inventory and equipment, and handling character movement and actions. Instead of trying to include all of these responsibilities in a single class, it would be better to split them into separate classes, each with its own single responsibility.
```c#
// Incorrect implementation
public class Character
{
    public int Health { get; set; }
    public int Level { get; set; }
    public List<Item> Inventory { get; set; }
    public Equipment Equipment { get; set; }

    public void Move(int x, int y)
    {
        // code to move character
    }

    public void Attack(Character target)
    {
        // code to attack target
    }
}

// Corrected implementation
public class CharacterStats
{
    public int Health { get; set; }
    public int Level { get; set; }
}

public class CharacterInventory
{
    public List<Item> Inventory { get; set; }
    public Equipment Equipment { get; set; }
}

public class CharacterMovement
{
    public void Move(int x, int y)
    {
        // code to move character
    }
}

public class CharacterCombat
{
    public void Attack(Character target)
    {
        // code to attack target
    }
}
```
