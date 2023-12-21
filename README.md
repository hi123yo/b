import java.util.Random;

class Character {
    private String name;
    private int health;
    private int attack;
    private int defense;

    // Constructor to initialize character attributes
    public Character(String name, int health, int attack, int defense) {
        this.name = name;
        this.health = health;
        this.attack = attack;
        this.defense = defense;
    }

    // Method to reduce health based on damage taken
    public void takeDamage(int damage) {
        health -= damage;
    }

    // Method to check if the character is still alive
    public boolean isAlive() {
        return health > 0;
    }

    // Method to provide a string representation of the character
    public String toString() {
        return name + " (Health: " + health + ")";
    }
}

// Function to simulate a battle between two characters
public void battle(Character character1, Character character2) {
    Random random = new Random(); // For introducing randomness in attacks

    int turn = 1;
    while (character1.isAlive() && character2.isAlive()) {
        System.out.println("Turn " + turn + ":");

        // Determine attacker and defender based on turn
        Character attacker = turn % 2 == 1 ? character1 : character2;
        Character defender = turn % 2 == 1 ? character2 : character1;

        // Calculate damage, ensuring it's not negative
        int damage = Math.max(0, attacker.attack - defender.defense);

        // Add randomness to damage for variation
        damage += random.nextInt(5); // Adjust the range for desired randomness

        // Apply damage to the defender
        defender.takeDamage(damage);

        System.out.println(attacker.name + " attacks " + defender.name + " for " + damage + " damage.");
        System.out.println(character1 + " " + character2);

        turn++;
    }

    // Declare the winner and loser
    Character winner = character1.isAlive() ? character1 : character2;
    Character loser = winner == character1 ? character2 : character1;

    System.out.println(winner.name + " wins!");
}

