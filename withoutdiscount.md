import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        // Item prices
        int hotdogPrice = 15;
        int siomaiPrice = 20;
        int waterPrice = 10;

        // Quantities for each item
        int hotdogQty = 0;
        int siomaiQty = 0;
        int waterQty = 0;

        System.out.println("CAFETERIA MENU:");
        System.out.println("[1] Hotdog - P15");
        System.out.println("[2] Siomai - P20");
        System.out.println("[3] Water  - P10");

        String addMore = "yes";

        while (addMore.equals("yes")) {
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

            // Ask for quantity and add to the correct item
            System.out.print("Enter quantity: ");
            int qty = input.nextInt();

            if (choice == 1) {
                hotdogQty += qty;
            } else if (choice == 2) {
                siomaiQty += qty;
            } else if (choice == 3) {
                waterQty += qty;
            }

            input.nextLine(); // clear buffer

            // Ask if user wants to add more items
            addMore = "";
            while (!addMore.equals("yes") && !addMore.equals("no")) {
                System.out.print("Do you want to add more items? (yes/no): ");
                addMore = input.nextLine().trim().toLowerCase();
                if (!addMore.equals("yes") && !addMore.equals("no")) {
                    System.out.println("Invalid input. Please type 'yes' or 'no'.");
                }
            }
        }

        // Calculate and display order summary
        int total = 0;
        System.out.println("\n--- ORDER SUMMARY ---");
        if (hotdogQty > 0) {
            int hotdogTotal = hotdogQty * hotdogPrice;
            total += hotdogTotal;
            System.out.println("Hotdog x " + hotdogQty + " = P" + hotdogTotal);
        }
        if (siomaiQty > 0) {
            int siomaiTotal = siomaiQty * siomaiPrice;
            total += siomaiTotal;
            System.out.println("Siomai x " + siomaiQty + " = P" + siomaiTotal);
        }
        if (waterQty > 0) {
            int waterTotal = waterQty * waterPrice;
            total += waterTotal;
            System.out.println("Water x " + waterQty + " = P" + waterTotal);
        }

        System.out.println("Total: P" + total);

        // Ask for cash until it's enough
        int cash = -1;
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
        System.out.println("Change: P" + change);
        System.out.println("Thank you for your order!");
    }
}
