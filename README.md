# ATM-Interface-using-Java
Creating an ATM Machine Simulation program which should simulate the basic functions of an ATM Machine. Functions include Account Balance Inquiry,Cash Withdrawal, Cash Deposit, PIN Change, Tansaction History.Using JAVA for my implementation .


#Code for the Program

import java.util.ArrayList;
import java.util.Scanner;

public class ATMSimulator {

    private static double balance = 1000.00;
    private static String pin = "1234";
    private static ArrayList<String> transactionHistory = new ArrayList<>();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Welcome to the ATM Machine!");
        System.out.print("Please enter your PIN: ");
        String enteredPin = scanner.nextLine();

        if (authenticate(enteredPin)) {
            int choice;
            do {
                System.out.println("\nATM Menu:");
                System.out.println("1. Account Balance Inquiry");
                System.out.println("2. Cash Withdrawal");
                System.out.println("3. Cash Deposit");
                System.out.println("4. Change PIN");
                System.out.println("5. Transaction History");
                System.out.println("6. Exit");
                System.out.print("Choose an option: ");
                choice = scanner.nextInt();

                switch (choice) {
                    case 1:
                        checkBalance();
                        break;
                    case 2:
                        withdrawCash(scanner);
                        break;
                    case 3:
                        depositCash(scanner);
                        break;
                    case 4:
                        changePIN(scanner);
                        break;
                    case 5:
                        showTransactionHistory();
                        break;
                    case 6:
                        System.out.println("Thank you for using the ATM. Goodbye!");
                        break;
                    default:
                        System.out.println("Invalid choice. Please try again.");
                }
            } while (choice != 6);
        } else {
            System.out.println("Incorrect PIN. Access denied.");
        }
        scanner.close();
    }

    private static boolean authenticate(String enteredPin) {
        return enteredPin.equals(pin);
    }

    private static void checkBalance() {
        System.out.printf("Your current balance is: $%.2f%n", balance);
        transactionHistory.add("Checked balance: $" + balance);
    }

    private static void withdrawCash(Scanner scanner) {
        System.out.print("Enter amount to withdraw: ");
        double amount = scanner.nextDouble();
        if (amount <= balance) {
            balance -= amount;
            System.out.printf("You have withdrawn: $%.2f%n", amount);
            System.out.printf("Your new balance is: $%.2f%n", balance);
            transactionHistory.add("Withdrew: $" + amount);
        } else {
            System.out.println("Insufficient balance.");
        }
    }

    private static void depositCash(Scanner scanner) {
        System.out.print("Enter amount to deposit: ");
        double amount = scanner.nextDouble();
        balance += amount;
        System.out.printf("You have deposited: $%.2f%n", amount);
        System.out.printf("Your new balance is: $%.2f%n", balance);
        transactionHistory.add("Deposited: $" + amount);
    }

    private static void changePIN(Scanner scanner) {
        System.out.print("Enter your current PIN: ");
        String currentPin = scanner.next();
        if (authenticate(currentPin)) {
            System.out.print("Enter new PIN: ");
            String newPin = scanner.next();
            pin = newPin;
            System.out.println("PIN changed successfully.");
            transactionHistory.add("Changed PIN");
        } else {
            System.out.println("Incorrect current PIN.");
        }
    }

    private static void showTransactionHistory() {
        System.out.println("Transaction History:");
        if (transactionHistory.isEmpty()) {
            System.out.println("No transactions made yet.");
        } else {
            for (String transaction : transactionHistory) {
                System.out.println(transaction);
            }
        }
    }
}
