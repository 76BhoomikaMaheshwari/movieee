#include <iostream>
#include <iomanip>
using namespace std;

const int Row = 5;
const int Col = 10;

// Function to display seating arrangement
void display(bool seats[Row][Col]) {
    cout << "  ";
    for (int i = 1; i <= Col; i++) {
        cout << setw(3) << i;
    }
    cout << endl;
    
    for (int i = 0; i < Row; i++) {
        cout << static_cast<char>('A' + i) << " "; // Display row labels
        for (int j = 0; j < Col; j++) {
            if (seats[i][j]) {
                cout << setw(3) << "X"; // Reserved seats
            } else {
                cout << setw(3) << "-"; // Available seats
            }
        }
        cout << endl;
    }
}

// Function to handle seat reservation
void reservation(bool seats[Row][Col], char row, int col) {
    int rowIndex = row - 'A'; // Convert row character to row index
    int colIndex = col - 1;   // Convert column number to 0-based index
    
    if (seats[rowIndex][colIndex]) {
        cout << "Seat is already reserved!" << endl;
    } else {
        seats[rowIndex][colIndex] = true;
        cout << "You have successfully reserved seat " << row << col << endl;
    }
}

int main() {
    bool seats[Row][Col] = { false }; // Initialize all seats to available
    char row;
    int col;

    display(seats); // Display initial seating arrangement

    while (true) {
        cout << "Enter Row (A-E): "; 
        cin >> row;
        cout << "Enter Column (1-10): "; 
        cin >> col;
        
        // Input validation for row and column
        if (row < 'A' || row > 'E' || col < 1 || col > 10) {
            cout << "Enter a valid Row (A-E) or Column (1-10)!" << endl;
            continue; // Prompt again if input is invalid
        }

        reservation(seats, row, col); // Reserve the seat
        display(seats);               // Refresh the seating chart
        
        char choice;
        cout << "Do you want to book more seats (Y/N)? "; 
        cin >> choice;

        if (choice != 'Y' && choice != 'y') {
            break; // Exit the loop if the user doesn't want to book more
        }
    }

    return 0;
}
