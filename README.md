# task-tracker
import csv
import os

FILE_NAME = "grades.csv"

def initialize_file():
    if not os.path.exists(FILE_NAME):
        with open(FILE_NAME, "w", newline="") as file:
            writer = csv.writer(file)
            writer.writerow(["ID", "Name", "Subject", "Grade"])

def add_student(student_id, name, subject, grade):
    with open(FILE_NAME, "a", newline="") as file:
        writer = csv.writer(file)
        writer.writerow([student_id, name, subject, grade])
    print("Student record added successfully!")

def list_students():
    with open(FILE_NAME, "r") as file:
        reader = csv.reader(file)
        for row in reader:
            print(row)

def update_grade(student_id, new_grade):
    rows = []
    with open(FILE_NAME, "r") as file:
        reader = csv.reader(file)
        rows = [row for row in reader]
    
    for row in rows:
        if row[0] == student_id:
            row[3] = new_grade
            break
    
    with open(FILE_NAME, "w", newline="") as file:
        writer = csv.writer(file)
        writer.writerows(rows)
    print("Grade updated successfully!")

def delete_student(student_id):
    rows = []
    with open(FILE_NAME, "r") as file:
        reader = csv.reader(file)
        rows = [row for row in reader if row[0] != student_id]
    
    with open(FILE_NAME, "w", newline="") as file:
        writer = csv.writer(file)
        writer.writerows(rows)
    print("Student record deleted successfully!")

if __name__ == "__main__":
    initialize_file()
    while True:
        print("\nStudent Grade Management System")
        print("1. Add Student")
        print("2. List Students")
        print("3. Update Grade")
        print("4. Delete Student")
        print("5. Exit")
        choice = input("Enter choice: ")
        if choice == "1":
            sid = input("Enter Student ID: ")
            name = input("Enter Name: ")
            subject = input("Enter Subject: ")
            grade = input("Enter Grade: ")
            add_student(sid, name, subject, grade)
        elif choice == "2":
            list_students()
        elif choice == "3":
            sid = input("Enter Student ID: ")
            grade = input("Enter New Grade: ")
            update_grade(sid, grade)
        elif choice == "4":
            sid = input("Enter Student ID: ")
            delete_student(sid)
        elif choice == "5":
            break
        else:
            print("Invalid choice, try again!")

