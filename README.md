#include <iostream>
#include <vector>
#include <string>

using namespace std;

struct Flight {
    int flightNumber;
    string destination;
    int seatsAvailable;
};

struct Reservation {
    string passengerName;
    int flightNumber;
};

vector<Flight> flights = {
    {101, "New York", 50},
    {102, "London", 40},
    {103, "Paris", 30},
    {104, "Tokyo", 20}
};

vector<Reservation> reservations;

void displayFlights() {
    cout << "\nAvailable Flights:\n";
    cout << "Flight Number\tDestination\tSeats Available\n";
    for (const auto& flight : flights) {
        cout << flight.flightNumber << "\t\t" << flight.destination << "\t\t" << flight.seatsAvailable << "\n";
    }
}

void bookFlight() {
    string name;
    int flightNumber;

    cout << "\nEnter your name: ";
    cin.ignore();
    getline(cin, name);

    displayFlights();

    cout << "\nEnter the flight number you want to book: ";
    cin >> flightNumber;

    for (auto& flight : flights) {
        if (flight.flightNumber == flightNumber) {
            if (flight.seatsAvailable > 0) {
                flight.seatsAvailable--;
                reservations.push_back({name, flightNumber});
                cout << "\nBooking successful!\n";
                return;
            } else {
                cout << "\nSorry, no seats available on this flight.\n";
                return;
            }
        }
    }

    cout << "\nInvalid flight number. Please try again.\n";
}

void viewReservations() {
    if (reservations.empty()) {
        cout << "\nNo reservations found.\n";
        return;
    }

    cout << "\nCurrent Reservations:\n";
    cout << "Passenger Name\tFlight Number\n";
    for (const auto& reservation : reservations) {
        cout << reservation.passengerName << "\t\t" << reservation.flightNumber << "\n";
    }
}

void cancelBooking() {
    string name;
    int flightNumber;

    cout << "\nEnter your name: ";
    cin.ignore();
    getline(cin, name);

    cout << "Enter the flight number of your booking: ";
    cin >> flightNumber;

    for (auto it = reservations.begin(); it != reservations.end(); ++it) {
        if (it->passengerName == name && it->flightNumber == flightNumber) {
            reservations.erase(it);

            for (auto& flight : flights) {
                if (flight.flightNumber == flightNumber) {
                    flight.seatsAvailable++;
                    break;
                }
            }

            cout << "\nBooking canceled successfully.\n";
            return;
        }
    }

    cout << "\nNo matching booking found.\n";
}

void collectFeedback() {
    string feedback;
    cout << "\nWe value your feedback. Please let us know how your experience was:\n";
    cin.ignore();
    getline(cin, feedback);
    cout << "\nThank you for your feedback!\n";
}

void menu() {
    while (true) {
        cout << "\n===========================================\n";
        cout << "            Flight Reservation System       \n";
        cout << "===========================================\n";
        cout << "1. Display Flights\n";
        cout << "2. Book Flight\n";
        cout << "3. View Reservations\n";
        cout << "4. Cancel Booking\n";
        cout << "5. Provide Feedback\n";
        cout << "6. Exit\n";           
        cout << "===========================================\n";

        cout << "\n>> Enter your choice: ";
        int choice;
        cin >> choice;

        switch (choice) {
            case 1:
                displayFlights();
                break;
            case 2:
                bookFlight();
                break;
            case 3:
                viewReservations();
                break;
            case 4:
                cancelBooking();
                break;
            case 5:
                collectFeedback();
                break;
            case 6:
                cout << "\nThank you for using the Flight Reservation System. Goodbye!\n";
                return;
            default:
                cout << "\nInvalid choice. Please try again.\n";
        }
    }
}

int main() {
    cout << "Welcome to the Flight Reservation System!\n";
    menu();
    return 0;
}# FlightReservation
