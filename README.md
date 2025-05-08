#include <iostream>
#include <string>
using namespace std;

class Node {
public:
    string model;
    string company;
    int year;
    float price;
    Node* next;

    Node(string m, string c, int y, float p) {
        model = m;
        company = c;
        year = y;
        price = p;
        next = nullptr;
    }
};

Node* head = nullptr;

// Utility: Count total cars
int countCars() {
    int count = 0;
    Node* temp = head;
    while (temp) {
        count++;
        temp = temp->next;
    }
    return count;
}

// Add car with input validation
void addCar() {
    string model, company;
    int year;
    float price;

    cout << "Model: ";
    cin >> model;
    cout << "Company: ";
    cin >> company;

    // Input validation for year
    while (true) {
        cout << "Year (1950-2025): ";
        cin >> year;
        if (year >= 1950 && year <= 2025) break;
        cout << "Invalid year. Try again.\n";
    }

    cout << "Price: ";
    cin >> price;

    Node* newNode = new Node(model, company, year, price);

    if (!head) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next) temp = temp->next;
        temp->next = newNode;
    }

    cout << "Car added successfully!\n";
    cout << "Total Cars in Showroom: " << countCars() << "\n";
}

// Display all cars
void displayCars() {
    if (!head) {
        cout << "Showroom is empty.\n";
        return;
    }

    Node* temp = head;
    while (temp) {
        cout << "\nModel: " << temp->model
             << "\nCompany: " << temp->company
             << "\nYear: " << temp->year
             << "\nPrice: $" << temp->price
             << "\n-----------------------\n";
        temp = temp->next;
    }
    cout << "Total Cars in Showroom: " << countCars() << "\n";
}

// Search for a car by model
void searchCar() {
    if (!head) {
        cout << "Nothing to search.\n";
        return;
    }

    string model;
    cout << "Enter model: ";
    cin >> model;

    Node* temp = head;
    while (temp) {
        if (temp->model == model) {
            cout << "\nCar Found:\n"
                 << "Model: " << temp->model
                 << "\nCompany: " << temp->company
                 << "\nYear: " << temp->year
                 << "\nPrice: $" << temp->price << "\n";
            return;
        }
        temp = temp->next;
    }

    cout << "Car not found.\n";
}

// Delete a car by model
void deleteCar() {
    if (!head) {
        cout << "Nothing to delete.\n";
        return;
    }

    string model;
    cout << "Enter model: ";
    cin >> model;

    Node* temp = head;
    Node* prev = nullptr;

    while (temp && temp->model != model) {
        prev = temp;
        temp = temp->next;
    }

    if (!temp) {
        cout << "Car not found.\n";
        return;
    }

    if (!prev) {
        head = head->next;
    } else {
        prev->next = temp->next;
    }

    delete temp;
    cout << "Car deleted successfully.\n";
    cout << "Total Cars in Showroom: " << countCars() << "\n";
}

// FCFS Scheduling Function
void processCarsFCFS() {
    if (!head) {
        cout << "No cars to process.\n";
        return;
    }

    cout << "\nProcessing Cars in FCFS Order:\n";

    Node* temp = head;
    int count = 1;
    while (temp) {
        cout << "\nProcessing Car #" << count << ":\n"
             << "Model: " << temp->model
             << "\nCompany: " << temp->company
             << "\nYear: " << temp->year
             << "\nPrice: $" << temp->price
             << "\n-----------------------\n";
        temp = temp->next;
        count++;
    }

    cout << "All cars processed successfully in FCFS order.\n";
}

// Show the cheapest car
void showCheapestCar() {
    if (!head) {
        cout << "No cars to evaluate.\n";
        return;
    }
    Node* temp = head;
    Node* minCar = head;
    while (temp) {
        if (temp->price < minCar->price)
            minCar = temp;
        temp = temp->next;
    }
    cout << "\nCheapest Car:\n"
         << "Model: " << minCar->model
         << "\nCompany: " << minCar->company
         << "\nYear: " << minCar->year
         << "\nPrice: $" << minCar->price << "\n";
}

int main() {
    int choice;
    do {
        cout << "\n--- Car Showroom Management ---\n"
             << "1. Add Car\n"
             << "2. View All Cars\n"
             << "3. Search Car by Model\n"
             << "4. Delete Car by Model\n"
             << "5. Process Cars (FCFS Scheduling)\n"
             << "6. Show Cheapest Car\n"
             << "7. Exit\n"
             << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: addCar(); break;
            case 2: displayCars(); break;
            case 3: searchCar(); break;
            case 4: deleteCar(); break;
            case 5: processCarsFCFS(); break;
            case 6: showCheapestCar(); break;
            case 7: cout << "Exiting program. Goodbye!\n"; break;
            default: cout << "Invalid choice. Please try again.\n";
        }

    } while (choice != 7);

    return 0;
}
