#include <iostream>
#include <fstream>
using namespace std;

struct Student {
    int rollNo;
    string name;
    int marks1, marks2, marks3;
    int total;
    float percentage;
    char grade;
};

// Function to calculate grade
char calculateGrade(float percentage) {
    if (percentage >= 80)
        return 'A';
    else if (percentage >= 60)
        return 'B';
    else if (percentage >= 40)
        return 'C';
    else
        return 'F';
}

// Function to add student record
void addStudent() {
    Student s;
    ofstream file("results.txt", ios::app);

    cout << "\nEnter Roll Number: ";
    cin >> s.rollNo;

    cout << "Enter Name: ";
    cin.ignore();
    getline(cin, s.name);

    cout << "Enter Marks of Subject 1: ";
    cin >> s.marks1;
    cout << "Enter Marks of Subject 2: ";
    cin >> s.marks2;
    cout << "Enter Marks of Subject 3: ";
    cin >> s.marks3;

    s.total = s.marks1 + s.marks2 + s.marks3;
    s.percentage = s.total / 3.0;
    s.grade = calculateGrade(s.percentage);

    file << s.rollNo << " " << s.name << " "
         << s.marks1 << " " << s.marks2 << " " << s.marks3 << " "
         << s.total << " " << s.percentage << " " << s.grade << endl;

    file.close();
    cout << "\nStudent record added successfully!\n";
}

// Function to display all records
void displayStudents() {
    Student s;
    ifstream file("results.txt");

    cout << "\n----- Student Results -----\n";

    while (file >> s.rollNo >> s.name >> s.marks1 >> s.marks2 >> s.marks3
           >> s.total >> s.percentage >> s.grade) {

        cout << "\nRoll No: " << s.rollNo;
        cout << "\nName: " << s.name;
        cout << "\nMarks: " << s.marks1 << ", " << s.marks2 << ", " << s.marks3;
        cout << "\nTotal: " << s.total;
        cout << "\nPercentage: " << s.percentage;
        cout << "\nGrade: " << s.grade << endl;
        cout << "----------------------------";
    }

    file.close();
}

// Main function
int main() {
    int choice;

    do {
        cout << "\n\n===== Student Result Management System =====";
        cout << "\n1. Add Student Record";
        cout << "\n2. View Student Records";
        cout << "\n3. Exit";
        cout << "\nEnter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                addStudent();
                break;
            case 2:
                displayStudents();
                break;
            case 3:
                cout << "\nExiting program. Goodbye!\n";
                break;
            default:
                cout << "\nInvalid choice! Try again.\n";
        }
    } while (choice != 3);

    return 0;
}
