# Task-5 
#include <iostream>
#include <vector>
#include <string>

using namespace std;

class Book {
public:
    int id;
    string title;
    string author;

    Book(int bookId, string bookTitle, string bookAuthor) {
        id = bookId;
        title = bookTitle;
        author = bookAuthor;
    }

    void displayBook() {
        cout << "ID: " << id << ", Title: " << title << ", Author: " << author << endl;
    }
};

class Library {
private:
    vector<Book> books;

public:
    void addBook(int id, string title, string author) {
        Book newBook(id, title, author);
        books.push_back(newBook);
        cout << "Book added successfully!" << endl;
    }

    void viewBooks() {
        if (books.empty()) {
            cout << "No books in the library!" << endl;
        } else {
            cout << "\n--- List of Books ---\n";
            for (const auto &book : books) {
                book.displayBook();
            }
        }
    }

    void searchBookByTitle(const string &title) {
        bool found = false;
        for (const auto &book : books) {
            if (book.title == title) {
                cout << "Book found:" << endl;
                book.displayBook();
                found = true;
                break;
            }
        }
        if (!found) {
            cout << "Book not found!" << endl;
        }
    }

    void deleteBook(int id) {
        bool found = false;
        for (auto it = books.begin(); it != books.end(); ++it) {
            if (it->id == id) {
                books.erase(it);
                cout << "Book deleted successfully!" << endl;
                found = true;
                break;
            }
        }
        if (!found) {
            cout << "Book with ID " << id << " not found!" << endl;
        }
    }
};

void displayMenu() {
    cout << "\n--- Library Management System Menu ---\n";
    cout << "1. Add Book\n";
    cout << "2. View All Books\n";
    cout << "3. Search Book by Title\n";
    cout << "4. Delete Book\n";
    cout << "5. Exit\n";
    cout << "Choose an option: ";
}

int main() {
    Library library;
    int choice;

    do {
        displayMenu();
        cin >> choice;
        cin.ignore(); // clear the newline character from the buffer

        switch (choice) {
            case 1: {
                cout << "Enter Book ID: ";
                int id;
                cin >> id;
                cin.ignore();

                cout << "Enter Book Title: ";
                string title;
                getline(cin, title);

                cout << "Enter Book Author: ";
                string author;
                getline(cin, author);

                library.addBook(id, title, author);
                break;
            }
            case 2: {
                library.viewBooks();
                break;
            }
            case 3: {
                cout << "Enter Book Title to search: ";
                string title;
                getline(cin, title);

                library.searchBookByTitle(title);
                break;
            }
            case 4: {
                cout << "Enter Book ID to delete: ";
                int id;
                cin >> id;

                library.deleteBook(id);
                break;
            }
            case 5: {
                cout << "Exiting the program. Goodbye!" << endl;
                break;
            }
            default: {
                cout << "Invalid option! Please choose again." << endl;
                break;
            }
        }
    } while (choice != 5);

    return 0;
}
