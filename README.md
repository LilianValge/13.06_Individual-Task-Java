# 13.06_Individual-Task-Java
## MAIN 
```java
import java.util.Scanner;

public class Main {
    private static Scanner scanner = new Scanner(System.in);
    private static CheeseService cheeseService = new CheeseService();

    public static void main(String[] args) {
        while (true) {
            System.out.println("Press 1, to add a cheese to the cart");
            System.out.println("Press 2, to remove a cheese from the cart");
            System.out.println("Press 3, to update a cheese in the cart");
            System.out.println("Press 4, to print all cheeses in the cart");
            System.out.println("Press 5, to exit");
            int action = scanner.nextInt();
            scanner.nextLine(); // Consume newline character after reading integer

            if (action == 1) {
                addCheese();
            } else if (action == 2) {
                removeCheese();
            } else if (action == 3) {
                updateCheese();
            } else if (action == 4) {
                printCheeses();
            } else if (action == 5) {
                System.out.println("Exiting...");
                break;
            } else {
                System.out.println("Invalid option. Please try again.");
            }
        }
    }

    public static void addCheese() {
        System.out.println("Provide a cheese name:");
        String name = scanner.nextLine();
        System.out.println("Provide a cheese price:");
        double price = Double.parseDouble(scanner.nextLine());
        System.out.println("Provide a cheese quantity:");
        int quantity = Integer.parseInt(scanner.nextLine());
        var cheese = new Cheese(name, price, quantity);
        cheeseService.addCheese(cheese);
        System.out.println("Cheese added successfully.");
    }

    public static void removeCheese() {
        System.out.println("Provide the cheese name to remove:");
        String name = scanner.nextLine();
        boolean result = cheeseService.removeCheese(name);
        if (result) {
            System.out.println("Cheese removed successfully.");
        } else {
            System.out.println("Cheese not found.");
        }
    }

    public static void updateCheese() {
        System.out.println("Provide the cheese name to update:");
        String name = scanner.nextLine();
        System.out.println("Provide the new cheese price:");
        double price = Double.parseDouble(scanner.nextLine());
        System.out.println("Provide the new cheese quantity:");
        int quantity = Integer.parseInt(scanner.nextLine());
        boolean result = cheeseService.updateCheese(name, price, quantity);
        if (result) {
            System.out.println("Cheese updated successfully.");
        } else {
            System.out.println("Cheese not found.");
        }
    }

    public static void printCheeses() {
        System.out.println("These are the cheeses in the cart:");
        var cheeses = cheeseService.getCheeses();
        for (var cheese : cheeses) {
            System.out.println("Name: " + cheese.getName() + ", Price: " + cheese.getPrice() + ", Quantity: " + cheese.getQuantity());
        }
    }
}

```
## CHEESE
```java
public class Cheese {
    private String name;
    private double price;
    private int quantity;

    public Cheese(String name, double price, int quantity) {
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }

    // Getters and setters
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    public int getQuantity() {
        return quantity;
    }

    public void setQuantity(int quantity) {
        this.quantity = quantity;
    }
}
```
## CHEESESHOP
```java
import java.util.ArrayList;

public class CheeseShop {
    private ArrayList<Cheese> cart = new ArrayList<>();

    public void addCheeseToCart(Cheese cheese) {
        cart.add(cheese);
    }

    public void removeCheeseFromCart(Cheese cheese) {
        cart.remove(cheese);
    }

    public double checkout() {
        double totalPrice = 0;
        for (Cheese cheese : cart) {
            totalPrice += cheese.getPrice() * cheese.getQuantity();
        }
        return totalPrice;
    }

    public ArrayList<Cheese> getCart() {
        return cart;
    }
}

```
## CHEESESERVICE
```java
import java.util.ArrayList;

public class CheeseService {
    private ArrayList<Cheese> cheeses = new ArrayList<>();

    public ArrayList<Cheese> getCheeses() {
        return cheeses;
    }

    public void addCheese(Cheese cheese) {
        cheeses.add(cheese);
    }

    public boolean removeCheese(String name) {
        for (Cheese cheese : cheeses) {
            if (cheese.getName().equals(name)) {
                cheeses.remove(cheese);
                return true;
            }
        }
        return false;
    }

    public boolean updateCheese(String name, double price, int quantity) {
        for (Cheese cheese : cheeses) {
            if (cheese.getName().equals(name)) {
                cheese.setPrice(price);
                cheese.setQuantity(quantity);
                return true;
            }
        }
        return false;
    }
}
```
