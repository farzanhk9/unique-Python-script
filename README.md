import time
from datetime import datetime

# List to store tasks and their deadlines
tasks = []

# Function to add a task
def add_task(description, deadline):
    tasks.append({
        "description": description,
        "deadline": deadline,
        "status": "Not Done"
    })
    print(f"Task '{description}' added with deadline {deadline}")

# Function to display tasks
def display_tasks():
    if not tasks:
        print("No tasks available.")
        return

    print("\nYour Tasks:")
    for idx, task in enumerate(tasks, 1):
        print(f"{idx}. {task['description']} | Deadline: {task['deadline']} | Status: {task['status']}")

# Function to mark task as done
def mark_task_as_done(task_id):
    if task_id <= 0 or task_id > len(tasks):
        print("Invalid task ID.")
        return
    tasks[task_id - 1]["status"] = "Done"
    print(f"Task {task_id} marked as Done!")

# Function to check for overdue tasks
def check_overdue_tasks():
    now = datetime.now()
    for task in tasks:
        task_deadline = datetime.strptime(task["deadline"], "%Y-%m-%d %H:%M")
        if task_deadline < now and task["status"] == "Not Done":
            print(f"\n🚨 Overdue Task: {task['description']} | Deadline: {task['deadline']}")

# Function to remind user about upcoming tasks
def remind_upcoming_tasks():
    now = datetime.now()
    for task in tasks:
        task_deadline = datetime.strptime(task["deadline"], "%Y-%m-%d %H:%M")
        time_left = task_deadline - now
        if time_left.days == 0 and task["status"] == "Not Done":
            print(f"\n🔔 Reminder: Task '{task['description']}' is due today at {task['deadline']}.")

# Main task management loop
def task_manager():
    while True:
        print("\nTask Management System:")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Mark Task as Done")
        print("4. Check Overdue Tasks")
        print("5. Remind Upcoming Tasks")
        print("6. Exit")
        
        choice = input("\nEnter your choice (1-6): ")
        
        if choice == "1":
            description = input("Enter task description: ")
            deadline = input("Enter task deadline (YYYY-MM-DD HH:MM): ")
            add_task(description, deadline)
        elif choice == "2":
            display_tasks()
        elif choice == "3":
            task_id = int(input("Enter task ID to mark as done: "))
            mark_task_as_done(task_id)
        elif choice == "4":
            check_overdue_tasks()
        elif choice == "5":
            remind_upcoming_tasks()
        elif choice == "6":
            print("Exiting Task Manager...")
            break
        else:
            print("Invalid choice. Please enter a number between 1-6.")
        
        time.sleep(1)  # Adding delay for smoother UI interaction

# Start the task manager
task_manager()
