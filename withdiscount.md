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
                        System.out.println("Quantity must be above 0.");
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

        // Calculate subtotal
        double subtotal = 0;
        System.out.println("\n--- ORDER SUMMARY ---");

        if (hotdogquant > 0) {
            double hotdogtotal = hotdogquant * hotdog;
            subtotal += hotdogtotal;
            System.out.printf("Hotdog x %d = P%.2f%n", hotdogquant, hotdogtotal);
        }

        if (siomaiquant > 0) {
            double siomaitotal = siomaiquant * siomai;
            subtotal += siomaitotal;
            System.out.printf("Siomai x %d = P%.2f%n", siomaiquant, siomaitotal);
        }

        if (waterquant > 0) {
            double watertotal = waterquant * water;
            subtotal += watertotal;
            System.out.printf("Water x %d = P%.2f%n", waterquant, watertotal);
        }

        // Apply discount
        double discount = 0;
        if (subtotal >= 100) {
            discount = subtotal * 0.10; // 10% discount
            System.out.printf("Discount (10%%): -P%.2f%n", discount);
        }

        double discountedTotal = subtotal - discount;

        // Apply tax
        double tax = discountedTotal * 0.12; // 12% VAT
        System.out.printf("VAT (12%%): +P%.2f%n", tax);

        // Final total
        double finalTotal = discountedTotal + tax;
        System.out.printf("Final Total: P%.2f%n", finalTotal);

        // Ask for cash until it's enough
        double cash = 0;
        while (cash < finalTotal) {
            System.out.print("Enter your cash: ");
            if (input.hasNextDouble()) {
                cash = input.nextDouble();
                if (cash < finalTotal) {
                    System.out.printf("Insufficient cash. Please enter at least P%.2f%n", finalTotal);
                }
            } else {
                System.out.println("Invalid input. Please enter a number.");
                input.next(); // clear invalid input
            }
        }

        double change = cash - finalTotal;
        System.out.printf("Change: P%.2f%n", change);
        System.out.println("Thank you for your order!");
    }
}
