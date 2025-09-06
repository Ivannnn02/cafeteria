import java.util.Scanner;

public class cafeteria {

    public static void main(String args[]) {
        Scanner input = new Scanner(System.in);

        // Item prices
        int hotdog = 15;
        int siomai = 12;
        int water = 10;

        // Quantities for each item
        int hotdogquant = 0;
        int siomaiquant = 0;
        int waterquant = 0;

        System.out.println("CAFETERIA MENU:");
        System.out.println("[1] Hotdog - P15");
        System.out.println("[2] Siomai - P12");
        System.out.println("[3] Water  - P10");

        String add = "yes";

        while (add.equals("yes")) {
            int choice = 0;

            // Ask for item choice
            while (choice < 1 || choice > 3) {
                System.out.print("\nWhat do you want to buy? (Enter 1-3): ");
                if (input.hasNextInt()) {
                    choice = input.nextInt();
                    if (choice < 1 || choice > 3) {
                        System.out.println("Invalid choice. Please enter a number from 1 to 3.");
                    }
                } else {
                    System.out.println("Invalid input. Please enter a number.");
                    input.next(); // clear invalid input
                }
            }

            // Ask for quantity and validate input
            int quantity = 0;
            while (quantity <= 0) {
                System.out.print("Enter quantity: ");
                if (input.hasNextInt()) {
                    quantity = input.nextInt();
                    if (quantity <= 0) {
                        System.out.println("Quantity cannot be negative.");
                    }
                } else {
                    System.out.println("Invalid input. Please enter a valid number.");
                    input.next(); // clear invalid input
                }
            }
            // Add to correct item
            if (choice == 1) {
                hotdogquant += quantity;
            } else if (choice == 2) {
                siomaiquant += quantity;
            } else if (choice == 3) {
                waterquant += quantity;
            }

            input.nextLine(); // consume newline

            // Ask if user wants to add more items
            add = "";
            while (!add.equals("yes") && !add.equals("no")) {
                System.out.print("Do you want to add more items? (yes/no): ");
                add = input.nextLine().trim().toLowerCase();
                if (!add.equals("yes") && !add.equals("no")) {
                    System.out.println("Invalid input. Please type 'yes' or 'no'.");
                }
            }
        }
        // Calculate and display order summary
        int total = 0;
        System.out.println("\n--- ORDER SUMMARY ---");
        if (hotdogquant > 0) {
            int hotdogtotal = hotdogquant * hotdog;
            total += hotdogtotal;
            System.out.println("Hotdog x " + hotdogquant + " = P" + hotdogtotal);
        }
        if (siomaiquant > 0) {
            int siomaitotal = siomaiquant * siomai;
            total += siomaitotal;
            System.out.println("Siomai x " + siomaiquant + " = P" + siomaitotal);
        }
        if (waterquant > 0) {
            int watertotal = waterquant * water;
            total += watertotal;
            System.out.println("Water x " + waterquant + " = P" + watertotal);
        }

        System.out.println("Total: P" + total);
        
        // Ask for cash until it's enough
        int cash = 0;
        while (cash < total) {
            System.out.print("Enter your cash: ");
            if (input.hasNextInt()) {
                cash = input.nextInt();
                if (cash < total) {
                    System.out.println("Insufficient cash. Please enter at least P" + total);
                }
            } else {
                System.out.println("Invalid input. Please enter a number.");
                input.next(); // clear invalid input
            }
        }
        int change = cash - total;
        System.out.printf("Change: P" + change);
        System.out.println("Thank you for your order!");
    }
}
