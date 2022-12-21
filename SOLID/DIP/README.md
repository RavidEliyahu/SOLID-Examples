# Dependency-Inversion-Principle
## Overview
The dependency inversion principle is a software design principle that states that high-level modules should not depend on low-level modules, but rather should depend on abstractions. In other words, it suggests that software systems should be designed in a way that decouples the high-level components from the low-level components, so that the high-level components can be easily modified or extended without affecting the low-level components.

## Example without using the dependency inversion principle:
```cs
// Game class that manages the game state and gameplay mechanics
public class Game
{
    private Player player;
    private Enemy enemy;

    public Game()
    {
        this.player = new Player();
        this.enemy = new Enemy();
    }

    public void Start()
    {
        while (true)
        {
            // Player's turn
            player.TakeTurn();

            // Enemy's turn
            enemy.TakeTurn();
        }
    }
}

// Player class that represents the player character
public class Player
{
    public void TakeTurn()
    {
        // Player performs actions during their turn
    }
}

// Enemy class that represents an enemy character
public class Enemy
{
    public void TakeTurn()
    {
        // Enemy performs actions during their turn
    }
}
```
In this example, the Game class is tightly coupled to the Player and Enemy classes, as it directly instantiates them and calls their TakeTurn() method. This means that if we want to change the behavior of the Player or Enemy classes, we need to modify the Game class as well, which can lead to maintenance issues and make the code more difficult to understand and modify.

## Here is the fixed version using the dependency inversion principle:
```cs
// ICharacter interface that defines the behavior of a character in the game
public interface ICharacter
{
    void TakeTurn();
}

// Game class that manages the game state and gameplay mechanics
public class Game
{
    private ICharacter player;
    private ICharacter enemy;

    public Game(ICharacter player, ICharacter enemy)
    {
        this.player = player;
        this.enemy = enemy;
    }

    public void Start()
    {
        while (true)
        {
            // Player's turn
            player.TakeTurn();

            // Enemy's turn
            enemy.TakeTurn();
        }
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

// Enemy class that represents an enemy character
public class Enemy : ICharacter
{
    public void TakeTurn()
    {
        // Enemy performs actions during their turn
    }
}
```
In this revised version, the Game class depends on the ICharacter interface rather than the concrete Player and Enemy classes. This allows us to easily swap out different implementations of the ICharacter interface without affecting the Game class, making the code more flexible and maintainable.
