# Liskov-substitution-principle
## Overview
The Liskov substitution principle is a software design principle that states that objects of a subclass should be able to be used in the same way as objects of the superclass, without causing any errors or unexpected behavior. In other words, it suggests that subclasses should be substitutable for their superclass, without changing the correctness of the program.
## Example without using the Liskov substitution principle:

```cs
// AdventureGame class that manages the game state and gameplay mechanics
public class AdventureGame
{
    private Player player;

    public AdventureGame()
    {
        this.player = new Player();
    }

    public void Start()
    {
        // Player performs actions during their turn
        player.TakeTurn();
    }
}

// Player class that represents the player character
public class Player
{
    public virtual void TakeTurn()
    {
        // Player performs actions during their turn
    }
}

// Wizard class that represents a wizard character
public class Wizard : Player
{
    public override void TakeTurn()
    {
        // Wizard casts a spell during their turn
        CastSpell();
    }

    private void CastSpell()
    {
        // Wizard casts a spell
    }
}
```
In this example, the Wizard class is a subclass of the Player class and overrides the TakeTurn() method. However, the Wizard class has additional behavior (casting a spell) that is not present in the Player class. This violates the Liskov substitution principle, because it means that we cannot use a Wizard object wherever a Player object is expected without potentially causing errors or unexpected behavior.

## Here is the fixed version using the Liskov substitution principle:
```cs
// ICharacter interface that defines the behavior of a character in the game
public interface ICharacter
{
    void TakeTurn();
}

// AdventureGame class that manages the game state and gameplay mechanics
public class AdventureGame
{
    private ICharacter player;

    public AdventureGame(ICharacter player)
    {
        this.player = player;
    }

    public void Start()
    {
        // Player performs actions during their turn
        player.TakeTurn();
    }
}

// Player class that represents the player character
public class Player : ICharacter
{
    public void TakeTurn()
    {
        // Player performs actions during their turn
    }
}

// Wizard class that represents a wizard character
public class Wizard : ICharacter
{
    public void TakeTurn()
    {
        // Wizard casts a spell during their turn
        CastSpell();
    }

    private void CastSpell()
    {
        // Wizard casts a spell
    }
}
```
In this revised version, both the Player and Wizard classes implement the ICharacter interface, which defines the behavior that is expected of a character in the game. This ensures that any class that implements the ICharacter interface can be used wherever an ICharacter object is expected, without causing errors or unexpected behavior. This makes the code more flexible and maintainable.
