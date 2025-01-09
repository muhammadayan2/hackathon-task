# hackathon-task
class BankAccount:
    def _init_(self, account_number, account_holder):
        self.account_number = account_number
        self.account_holder = account_holder
        self.balance = 0
        self.transactions = []

    def deposit(self, amount):
        self.balance += amount
        self.transactions.append(f"Deposited: {amount}")
        print(f"{amount} deposited successfully.")

    def withdraw(self, amount):
        if amount > self.balance:
            print("Insufficient balance!")
        else:
            self.balance -= amount
            self.transactions.append(f"Withdrew: {amount}")
            print(f"{amount} withdrawn successfully.")

    def check_balance(self):
        print(f"Current balance: {self.balance}")

    def add_transaction(self, description):
        self.transactions.append(description)

    def print_statement(self):
        print("Transaction Statement:")
        for transaction in self.transactions:
            print(transaction)
    class Bank:
    def _init_(self):
        self.accounts = {}
        self.next_account_number = 1001

    def open_account(self, account_holder):
        account = BankAccount(self.next_account_number, account_holder)
        self.accounts[self.next_account_number] = account
        print(f"Account created successfully! Account Number: {self.next_account_number}")
        self.next_account_number += 1

    def get_account(self, account_number):
        return self.accounts.get(account_number, None)

    def transfer(self, sender_account_number, receiver_account_number, amount):
        sender = self.get_account(sender_account_number)
        receiver = self.get_account(receiver_account_number)

        if sender and receiver:
            if sender.balance >= amount:
                sender.withdraw(amount)
                receiver.deposit(amount)
                print(f"Transferred {amount} from Account {sender_account_number} to {receiver_account_number}.")
            else:
                print("Insufficient balance for transfer.")
        else:
            print("One or both account numbers are invalid.")

    def admin_check_total_deposit(self):
        total = sum(account.balance for account in self.accounts.values())
        print(f"Total deposits in the bank: {total}")
    def admin_check_total_accounts(self):
        print(f"Total number of accounts in the bank: {len(self.accounts)}")


#Example Usage
bank = Bank()

# Open accounts
bank.open_account("Alice")
bank.open_account("Bob")

# Deposit money
account = bank.get_account(1001)
if account:
    account.deposit(500)

account = bank.get_account(1002)
if account:
    account.deposit(1000)

# Transfer money
bank.transfer(1001, 1002, 200)

# Admin Operations
bank.admin_check_total_deposit()
bank.admin_check_total_accounts()

# Print statement
account = bank.get_account(1001)
if account:
    account.print_statement()
