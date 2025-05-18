# ospracticle

#sheduling

def fcfs(processes):
    print("\n--- First-Come, First-Served (FCFS) Scheduling ---")
    processes.sort(key=lambda x: x[1])  # sort by arrival time
    current_time = 0
    print("PID\tAT\tBT\tWT\tTAT")
    for pid, at, bt, _ in processes:
        start_time = max(current_time, at)
        wt = start_time - at
        tat = wt + bt
        print(f"{pid}\t{at}\t{bt}\t{wt}\t{tat}")
        current_time = start_time + bt


def sjf(processes):
    print("\n--- Shortest Job First (SJF) Scheduling ---")
    n = len(processes)
    completed = []
    time = 0
    print("PID\tAT\tBT\tWT\tTAT")
    while len(completed) < n:
        ready = [p for p in processes if p[1] <= time and p not in completed]
        if ready:
            shortest = min(ready, key=lambda x: x[2])  # burst time
            wt = time - shortest[1]
            tat = wt + shortest[2]
            print(f"{shortest[0]}\t{shortest[1]}\t{shortest[2]}\t{wt}\t{tat}")
            time += shortest[2]
            completed.append(shortest)
        else:
            time += 1


def priority_scheduling(processes):
    print("\n--- Priority Scheduling ---")
    n = len(processes)
    completed = []
    time = 0
    print("PID\tAT\tBT\tPR\tWT\tTAT")
    while len(completed) < n:
        ready = [p for p in processes if p[1] <= time and p not in completed]
        if ready:
            highest_priority = min(ready, key=lambda x: x[3])  # lower number = higher priority
            wt = time - highest_priority[1]
            tat = wt + highest_priority[2]
            print(f"{highest_priority[0]}\t{highest_priority[1]}\t{highest_priority[2]}\t{highest_priority[3]}\t{wt}\t{tat}")
            time += highest_priority[2]
            completed.append(highest_priority)
        else:
            time += 1


# === Main Program ===
def main():
    processes = []
    n = int(input("Enter number of processes: "))
    for i in range(n):
        pid = i + 1
        at = int(input(f"Enter Arrival Time for P{pid}: "))
        bt = int(input(f"Enter Burst Time for P{pid}: "))
        pr = int(input(f"Enter Priority for P{pid} (lower number = higher priority): "))
        processes.append([pid, at, bt, pr])

    while True:
        print("\nSelect Scheduling Algorithm:")
        print("1. First-Come First-Served (FCFS)")
        print("2. Shortest Job First (SJF)")
        print("3. Priority Scheduling")
        print("4. Exit")
        choice = input("Enter choice (1-4): ")

        if choice == '1':
            fcfs(processes.copy())
        elif choice == '2':
            sjf(processes.copy())
        elif choice == '3':
            priority_scheduling(processes.copy())
        elif choice == '4':
            print("Exiting...")
            break
        else:
            print("Invalid choice. Try again.")


if __name__ == "__main__":
    main()

#producer consumer --------------------------------------------------------------------------------------------

def fcfs(processes):
    print("\n--- First-Come, First-Served (FCFS) Scheduling ---")
    processes.sort(key=lambda x: x[1])  # sort by arrival time
    current_time = 0
    print("PID\tAT\tBT\tWT\tTAT")
    for pid, at, bt, _ in processes:
        start_time = max(current_time, at)
        wt = start_time - at
        tat = wt + bt
        print(f"{pid}\t{at}\t{bt}\t{wt}\t{tat}")
        current_time = start_time + bt


def sjf(processes):
    print("\n--- Shortest Job First (SJF) Scheduling ---")
    n = len(processes)
    completed = []
    time = 0
    print("PID\tAT\tBT\tWT\tTAT")
    while len(completed) < n:
        ready = [p for p in processes if p[1] <= time and p not in completed]
        if ready:
            shortest = min(ready, key=lambda x: x[2])  # burst time
            wt = time - shortest[1]
            tat = wt + shortest[2]
            print(f"{shortest[0]}\t{shortest[1]}\t{shortest[2]}\t{wt}\t{tat}")
            time += shortest[2]
            completed.append(shortest)
        else:
            time += 1


def priority_scheduling(processes):
    print("\n--- Priority Scheduling ---")
    n = len(processes)
    completed = []
    time = 0
    print("PID\tAT\tBT\tPR\tWT\tTAT")
    while len(completed) < n:
        ready = [p for p in processes if p[1] <= time and p not in completed]
        if ready:
            highest_priority = min(ready, key=lambda x: x[3])  # lower number = higher priority
            wt = time - highest_priority[1]
            tat = wt + highest_priority[2]
            print(f"{highest_priority[0]}\t{highest_priority[1]}\t{highest_priority[2]}\t{highest_priority[3]}\t{wt}\t{tat}")
            time += highest_priority[2]
            completed.append(highest_priority)
        else:
            time += 1


# === Main Program ===
def main():
    processes = []
    n = int(input("Enter number of processes: "))
    for i in range(n):
        pid = i + 1
        at = int(input(f"Enter Arrival Time for P{pid}: "))
        bt = int(input(f"Enter Burst Time for P{pid}: "))
        pr = int(input(f"Enter Priority for P{pid} (lower number = higher priority): "))
        processes.append([pid, at, bt, pr])

    while True:
        print("\nSelect Scheduling Algorithm:")
        print("1. First-Come First-Served (FCFS)")
        print("2. Shortest Job First (SJF)")
        print("3. Priority Scheduling")
        print("4. Exit")
        choice = input("Enter choice (1-4): ")

        if choice == '1':
            fcfs(processes.copy())
        elif choice == '2':
            sjf(processes.copy())
        elif choice == '3':
            priority_scheduling(processes.copy())
        elif choice == '4':
            print("Exiting...")
            break
        else:
            print("Invalid choice. Try again.")


if __name__ == "__main__":
    main()
    
phone book ----------------------------------------------------------------------------------------------------

import re

address_book = []

def create_address_book():
    global address_book
    address_book = []
    print("Address book created.\n")

def view_address_book():
    if not address_book:
        print("Address book is empty.\n")
    else:
        print(f"{'No.':<4} {'Name':<20} {'Phone':<15} {'Email'}")
        for i, record in enumerate(address_book, 1):
            print(f"{i:<4} {record['name']:<20} {record['phone']:<15} {record['email']}")
        print()

def validate_phone(phone):
    return re.fullmatch(r'\d{10}', phone) is not None

def validate_email(email):
    return re.fullmatch(r"[^@]+@[^@]+\.[^@]+", email) is not None

def insert_record():
    name = input("Name: ").strip()
    phone = input("Phone (10 digits): ").strip()
    email = input("Email: ").strip()

    if not name or not validate_phone(phone):
        print("Invalid name or phone.\n")
        return
    if any(r['phone'] == phone for r in address_book):
        print("Phone number already exists.\n")
        return
    if email and not validate_email(email):
        print("Invalid email.\n")
        return

    address_book.append({'name': name, 'phone': phone, 'email': email})
    print("Record added.\n")

def delete_record():
    phone = input("Phone to delete: ").strip()
    for record in address_book:
        if record['phone'] == phone:
            address_book.remove(record)
            print("Record deleted.\n")
            return
    print("Record not found.\n")

def modify_record():
    phone = input("Phone to modify: ").strip()
    for record in address_book:
        if record['phone'] == phone:
            name = input(f"New name (current: {record['name']}): ").strip()
            new_phone = input(f"New phone (current: {record['phone']}): ").strip()
            email = input(f"New email (current: {record['email']}): ").strip()

            if new_phone and (not validate_phone(new_phone) or any(r['phone'] == new_phone and r != record for r in address_book)):
                print("Invalid or duplicate new phone.\n")
                return
            if email and not validate_email(email):
                print("Invalid email.\n")
                return

            if name: record['name'] = name
            if new_phone: record['phone'] = new_phone
            if email: record['email'] = email
            print("Record updated.\n")
            return
    print("Record not found.\n")

def main():
    while True:
        print("Menu: a)Create b)View c)Insert d)Delete e)Modify f)Exit")
        choice = input("Choice: ").lower()
        if choice == 'a':
            create_address_book()
        elif choice == 'b':
            view_address_book()
        elif choice == 'c':
            insert_record()
        elif choice == 'd':
            delete_record()
        elif choice == 'e':
            modify_record()
        elif choice == 'f':
            print("Exiting.")
            break
        else:
            print("Invalid choice.\n")

if __name__ == "__main__":
    main()

# Fork zombie ----------------------------------------------------------------------------------------------------

import os
import time

def demo_fork_and_wait():
    pid = os.fork()
    if pid == 0:
        print("[Child] My PID is", os.getpid())
        print("[Child] Exiting now.")
        os._exit(0)
    else:
        print("[Parent] Waiting for child to finish.")
        os.wait()
        print("[Parent] Child process finished.")

def demo_execve():
    pid = os.fork()
    if pid == 0:
        print("[Child] Replacing myself with 'ls -l'")
        os.execve("/bin/ls", ["ls", "-l"], os.environ)
    else:
        os.wait()
        print("[Parent] Child executed 'ls' command.")

def demo_zombie():
    pid = os.fork()
    if pid == 0:
        print("[Child] I am exiting immediately (PID:", os.getpid(), ")")
        os._exit(0)
    else:
        print("[Parent] I am sleeping. Child becomes zombie temporarily.")
        time.sleep(10)  # During this time, child is a zombie
        print("[Parent] Now I will call wait() to clean up zombie.")
        os.wait()

def demo_orphan():
    pid = os.fork()
    if pid == 0:
        # First child
        second_pid = os.fork()
        if second_pid == 0:
            # Grandchild that will become orphan
            time.sleep(5)
            print(f"[Orphan Child] My new parent PID is: {os.getppid()}")
            print("[Orphan Child] I am orphan now.")
            os._exit(0)
        else:
            print("[First Child] I am exiting. My child will become orphan.")
            os._exit(0)
    else:
        os.wait()

def menu():
    while True:
        print("\n==== Process Control System Calls Menu ====")
        print("1. Demonstrate fork() and wait()")
        print("2. Demonstrate execve()")
        print("3. Demonstrate Zombie Process")
        print("4. Demonstrate Orphan Process")
        print("5. Exit")
        try:
            choice = input("Enter your choice: ")
        except EOFError:
            break

        if choice == '1':
            demo_fork_and_wait()
        elif choice == '2':
            demo_execve()
        elif choice == '3':
            demo_zombie()
        elif choice == '4':
            demo_orphan()
        elif choice == '5':
            print("Exiting program.")
            break
        else:
            print("Invalid choice. Please enter 1–5.")

if _name_ == "_main_":
    menu()


#Thread Cycle------------------------------------------------------------------------------------------------------------------------

import threading
import time

# Define a simple function for the thread to run
def my_thread():
    print("Thread is starting...")
    time.sleep(2)  # Thread goes to sleep for 2 seconds
    print("Thread is running again...")
    time.sleep(1)
    print("Thread has finished.")

# Create a thread
t = threading.Thread(target=my_thread)

print("Main: Starting the thread")
t.start()  # Start the thread

print("Main: Waiting for the thread to finish")
t.join()  # Wait for the thread to complete

print("Main: Thread has completed")


# Multithreding-------------------------------------------------------------------------------------------------

import threading
import time
import random

class SharedResource:
    def __init__(self):
        self._data = 0
        self._lock = threading.Lock()

    def read(self):
        with self._lock:
            print(f"[Reader] Read data: {self._data}")

    def write(self, value):
        with self._lock:
            print(f"[Writer] Writing data: {value}")
            self._data = value
            print(f"[Writer] New data set to: {self._data}")

class ThreadBase(threading.Thread):
    def __init__(self, shared_resource):
        super().__init__()
        self.shared_resource = shared_resource

    def run(self):
        raise NotImplementedError("Subclasses must override run()")

class ReaderThread(ThreadBase):
    def run(self):
        for _ in range(3):
            self.shared_resource.read()
            time.sleep(random.uniform(0.5, 1.0))

class WriterThread(ThreadBase):
    def run(self):
        for _ in range(3):
            value = random.randint(1, 100)
            self.shared_resource.write(value)
            time.sleep(random.uniform(0.5, 1.0))

if __name__ == "__main__":
    shared_resource = SharedResource()

    threads = [
        ReaderThread(shared_resource),
        WriterThread(shared_resource),
        ReaderThread(shared_resource)
    ]

    for t in threads:
        t.start()

    for t in threads:
        t.join()

    print("All threads have finished execution.")


