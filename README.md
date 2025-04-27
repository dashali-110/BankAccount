# BankAccount

import java.util.ArrayList;
import java.util.Scanner;

class BankAccount {
    private String accountNumber;
    private String accountHolder;
    private double balance;

    public BankAccount(String accountNumber, String accountHolder, double balance) {
        this.accountNumber = accountNumber;
        this.accountHolder = accountHolder;
        this.balance = balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println(amount + "The currency was successfully deposited.");
        } else {
            System.out.println("The deposit amount must be positive.");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println(amount + "The currency was withdrawn.");
        } else {
            System.out.println("Invalid amount or insufficient balance.");
        }
    }

    public void displayInfo() {
        System.out.println("number account:" + accountNumber);
        System.out.println("Name of the account holder:" + accountHolder);
        System.out.println("Account balance:" + balance);
    }

    public String getAccountNumber() {
        return accountNumber;
    }
}

public class BankSystem {
    private static ArrayList<BankAccount> accounts = new ArrayList<>();
    private static Scanner scanner = new Scanner(System.in);

    public static void addAccount() {
        System.out.print("please enter number account:");
        String accountNumber = scanner.nextLine();
        System.out.print("Enter the account owner's name:");
        String accountHolder = scanner.nextLine();
        System.out.print("Enter the initial balance:");
        double balance = scanner.nextDouble();
        scanner.nextLine();

        BankAccount newAccount = new BankAccount(accountNumber, accountHolder, balance);
        accounts.add(newAccount);
        System.out.println("Account created successfully!");
    }

    public static void depositToAccount() {
        System.out.print("Enter the destination account number:");
        String accountNumber = scanner.nextLine();
        for (BankAccount account : accounts) {
            if (account.getAccountNumber().equals(accountNumber)) {
                System.out.print("Enter the deposit amount:");
                double amount = scanner.nextDouble();
                scanner.nextLine(); 
                account.deposit(amount);
                return;
            }
        }
        System.out.println("The desired account was not found!");
    }

    public static void withdrawFromAccount() {
        System.out.print("Enter account number:");
        String accountNumber = scanner.nextLine();
        for (BankAccount account : accounts) {
            if (account.getAccountNumber().equals(accountNumber)) {
                System.out.print("Enter the withdrawal amount:");
                double amount = scanner.nextDouble();
                scanner.nextLine(); 
                account.withdraw(amount);
                return;
            }
        }
        System.out.println("The desired account was not found!");
    }

    public static void displayAccounts() {
        if (accounts.isEmpty()) {
            System.out.println("There is no account.");
        } else {
            for (BankAccount account : accounts) {
                account.displayInfo();
                System.out.println("----------------------------------------------");
            }
        }
    }

    public static void main(String[] args) {
        while (true) {
            System.out.println("\n1. Create an account");
            System.out.println("2. Deposit money");
            System.out.println("3. Withdraw funds");
            System.out.println("4. View accounts");
            System.out.println("5. Exit");
            System.out.print("Choose:");
            int choice = scanner.nextInt();
            scanner.nextLine(); 

            switch (choice) {
                case 1:
                    addAccount();
                    break;
                case 2:
                    depositToAccount();
                    break;
                case 3:
                    withdrawFromAccount();
                    break;
                case 4:
                    displayAccounts();
                    break;
                case 5:
                    System.out.println("Exit the app...");
                    return;
                default:
                    System.out.println("Invalid option, please select again.");
            }
        }
    }
}
    

