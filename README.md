#include <iostream>
#include <vector>
#include <string>

using namespace std;

class Book {
public:
    int id;
    string title;
    string author;
    bool isIssued;

    Book(int i, string t, string a) {
        id = i;
        title = t;
        author = a;
        isIssued = false;
    }
};

vector<Book> library;

void addBook() {
    int id;
    string title, author;
    cout << "Enter Book ID: ";
    cin >> id;
    cin.ignore();
    cout << "Enter Title: ";
    getline(cin, title);
    cout << "Enter Author: ";
    getline(cin, author);
    library.push_back(Book(id, title, author));
    cout << "Book added successfully!\n";
}

void displayBooks() {
    cout << "\n--- Library Books ---\n";
    for (auto &book : library) {
        cout << "ID: " << book.id << ", Title: " << book.title
             << ", Author: " << book.author
             << ", Issued: " << (book.isIssued ? "Yes" : "No") << endl;
    }
}

void searchBook() {
    int id;
    cout << "Enter Book ID to search: ";
    cin >> id;
    for (auto &book : library) {
        if (book.id == id) {
            cout << "Book Found - Title: " << book.title << ", Author: " << book.author << endl;
            return;
        }
    }
    cout << "Book not found!\n";
}

void issueBook() {
    int id;
    cout << "Enter Book ID to issue: ";
    cin >> id;
    for (auto &book : library) {
        if (book.id == id) {
            if (!book.isIssued) {
                book.isIssued = true;
                cout << "Book issued successfully!\n";
            } else {
                cout << "Book is already issued.\n";
            }
            return;
        }
    }
    cout << "Book not found!\n";
}

void returnBook() {
    int id;
    cout << "Enter Book ID to return: ";
    cin >> id;
    for (auto &book : library) {
        if (book.id == id) {
            if (book.isIssued) {
                book.isIssued = false;
                cout << "Book returned successfully!\n";
            } else {
                cout << "Book was not issued.\n";
            }
            return;
        }
    }
    cout << "Book not found!\n";
}

int main() {
    int choice;
    do {
        cout << "\nLibrary Management System Menu:\n";
        cout << "1. Add Book\n";
        cout << "2. Display Books\n";
        cout << "3. Search Book\n";
        cout << "4. Issue Book\n";
        cout << "5. Return Book\n";
        cout << "6. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: addBook(); break;
            case 2: displayBooks(); break;
            case 3: searchBook(); break;
            case 4: issueBook(); break;
            case 5: returnBook(); break;
            case 6: cout << "Exiting...\n"; break;
            default: cout << "Invalid choice!\n"; break;
        }
    } while (choice != 6);

    return 0;
}
