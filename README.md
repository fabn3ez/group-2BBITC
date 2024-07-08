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

