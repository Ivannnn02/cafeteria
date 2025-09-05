import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        // Item prices
        int hotdogPrice = 15;
        int siomaiPrice = 20;
        int waterPrice = 10;

        // Quantities
        int hotdogQty = 0;
        int siomaiQty = 0;
        int waterQty = 0;

        System.out.println("CAFETERIA MENU:");
        System.out.println("[1] Hotdog - P15");
        System.out.println("[2] Siomai - P20");
        System.out.println("[3] Water  - P10");

        String addMore = "yes";

        // Order loop
        while (addMore.equals("yes")) {
            int choice = 0;

            // Valid item choice
            while (choice < 1 || choice > 3) {
                System.out.print("\nWhat do you want to buy? (Enter 1-3): ");
                if (input.hasNextInt()) {
                    choice = input.nextInt();
                    if (choice < 1 || choice > 3) {
                        System.out.println("Invalid choice. Please enter 1 to 3.");
                    }
                } else {
                    System.out.println("Invalid input. Please enter a number.");
                    input.next(); // Clear wrong input
                }
            }

            // Quantity
            System.out.print("Enter quantity: ");
            int qty = input.nextInt();

            // Update quantity based on item
            if (choice == 1) {
                hotdogQty += qty;
            } else if (choice == 2) {
                siomaiQty += qty;
            } else if (choice == 3) {
                waterQty += qty;
            }

            input.nextLine(); // Clear buffer

            // Ask to add more items
            addMore = "";
            while (!addMore.equals("yes") && !addMore.equals("no")) {
                System.out.print("Do you want to add more items? (yes/no): ");
                addMore = input.nextLine().trim().toLowerCase();
                if (!addMore.equals("yes") && !addMore.equals("no")) {
                    System.out.println("Invalid input. Please type 'yes' or 'no'.");
                }
            }
        }

        // --- Order Summary ---
        int hotdogTotal = hotdogQty * hotdogPrice;
        int siomaiTotal = siomaiQty * siomaiPrice;
        int waterTotal = waterQty * waterPrice;

        int subtotal = hotdogTotal + siomaiTotal + waterTotal;

        // Discount: 10% if subtotal is 100 or more
        double discount = 0;
        if (subtotal >= 100) {
            discount = subtotal * 0.10;
        }

        // Tax: 12% of (subtotal - discount)
        double tax = (subtotal - discount) * 0.12;

        // Final total
        double total = subtotal - discount + tax;

        // Show summary
        System.out.println("\n--- ORDER SUMMARY ---");
        if (hotdogQty > 0) {
            System.out.println("Hotdog x " + hotdogQty + " = P" + hotdogTotal);
        }
        if (siomaiQty > 0) {
            System.out.println("Siomai x " + siomaiQty + " = P" + siomaiTotal);
        }
        if (waterQty > 0) {
            System.out.println("Water x " + waterQty + " = P" + waterTotal);
        }

        System.out.printf("Subtotal: P%.2f%n", (double)subtotal);
        System.out.printf("Discount: -P%.2f%n", discount);
        System.out.printf("Tax (12%%): +P%.2f%n", tax);
        System.out.printf("Total to Pay: P%.2f%n", total);

        // Ask for cash
        double cash = 0;
        while (cash < total) {
            System.out.print("Enter your cash: ");
            if (input.hasNextDouble()) {
                cash = input.nextDouble();
                if (cash < total) {
                    System.out.printf("Insufficient cash. Please enter at least P%.2f%n", total);
                }
            } else {
                System.out.println("Invalid input. Please enter a number.");
                input.next(); // Clear invalid input
            }
        }

        double change = cash - total;
        System.out.printf("Change: P%.2f%n", change);
        System.out.println("Thank you for your order!");
    }
}
