#include <iostream>
#include <vector>
#include <fstream>
#include <string>
#include <iomanip>
using namespace std;
struct student {
    string firstname;
    string surname;
    char gender{};
    int age{};
    int group{};
    string sport;
    vector<string> clubs;
};

// Function prototypes
void addStudent(vector<student>& students);
void viewStudents(const vector<student>& students);
void viewClubs();
void viewSports();
void viewGroupedStudents();
void saveToFile(const vector<student>& students);
int main() {
    vector<student> students;
    int choice;

    do {
        cout << "1. Add Student" << endl;
        cout << "2. View Students" << endl;
        cout << "3. View Clubs/Societies" << endl;
        cout << "4. View Sports" << endl;
        cout << "5. View Grouped Students" << endl;
        cout << "6. Save all Files" << endl;
        cout << "7. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                addStudent(students);
                break;
            case 2:
                viewStudents(students);
                break;
            case 3:
                viewClubs();
                break;
            case 4:
                viewSports();
                break;
            case 5:
                viewGroupedStudents();
                break;
            case 6:
                saveToFile(students);
                break;
            case 7:
                cout << "Exiting program." << endl;
                break;
            default:
                cout << "Invalid choice. Please try again." << endl;
        }
    } while (choice != 7);

    return 0;
}

void addStudent(vector<student>& students) {
    student newStudent;
    cout << "Enter student's first name: ";
    cin >> newStudent.firstname;
    cout << "Enter student's surname: ";
    cin >> newStudent.surname;
    cout << "Enter student's gender (M/F): ";
    cin >> newStudent.gender;
    cout << "Enter student's age: ";
    cin >> newStudent.age;
    cout << "Enter student's BBiT group: ";
    cin >> newStudent.group;

    // Activity selection
    cout << "Select student's sport (or type 'None'): ";
    cin.ignore(); // Ignore newline character
    getline(cin, newStudent.sport);
    if (newStudent.sport != "None") {
    }
    if (newStudent.sport == "None") {
        string club;
        cout << "Select student's club/society (or type 'None' to skip): ";
        getline(cin, club);
        while (club != "None") {
            newStudent.clubs.push_back(club);
            cout << "Select another club/society (or type 'None' to finish): ";
            getline(cin, club);
        }
    }

    students.push_back(newStudent);
    cout << "Student added successfully!" << endl;
}

void viewStudents(const vector<student>& students) {
    if (students.empty()) {
        cout << "No students to display." << endl;
        return;
    }

    cout << "Viewing all students:" << endl;
    cout << setw(15) << "First Name" << setw(15) << "Surname" << setw(8) << "Gender" << setw(5) << "Age" << setw(8) << "Group" << setw(15) << "Sport" << setw(20) << "Clubs/Societies" << endl;
    for (const auto& student : students) {
        cout << setw(15) << student.firstname << setw(15) << student.surname << setw(8) << student.gender << setw(5) << student.age << setw(8) << student.group << setw(15) << student.sport;
        for (const auto& club : student.clubs) {
            cout << club << " ";
        }
        cout << endl;
    }
}

void viewClubs() {
    cout << "Available Clubs/Societies:" << endl;
    // List available clubs and their capacities
}

void viewSports() {
    cout << "Available Sports:" << endl;
    // List available sports and their capacities
}

void viewGroupedStudents() {
    cout << "Viewing Grouped Students:" << endl;
    // Group students by activity and group, and display
}

void saveToFile(const vector<student>& students) {
    ofstream outFile("students.csv");
    if (!outFile) {
        cerr << "Error opening file." << endl;
        return;
    }

    // Write student data to CSV file
    outFile << "First Name,Surname,Gender,Age,BBiT Group,Sport,Clubs/Societies" << endl;
    for (const auto &student: students) {
        outFile << student.firstname << "," << student.surname << "," << student.gender << "," << student.age << ","
                << student.group << "," << student.sport << ",";
        for (const auto &club: student.clubs) {
            outFile << club << " ";
        }
        outFile << endl;
    }

    outFile.close();
    cout << "Data saved to students.csv" << endl;
}
