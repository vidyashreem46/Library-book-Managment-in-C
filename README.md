#include <stdio.h>
#include <string.h>

// Step 1: Define struct
struct Book {
    int id;
    char title[50];
    char author[50];
    int available; // 1 = available, 0 = issued
};

// Step 2: Add a Book
void addBook(struct Book books[], int *count) {
    printf("Enter Book ID: ");
    scanf("%d", &books[*count].id);

    printf("Enter Title of the book: ");
    scanf(" %[^\n]s", books[*count].title);

    printf("Enter Author of the book: ");
    scanf(" %[^\n]s", books[*count].author);

    books[*count].available = 1; // available by default
    (*count)++;
    printf("Book added successfully!\n\n");
}

// Step 3: Display All Books
void displayBooks(struct Book books[], int count) {
    if (count == 0) {
        printf("No books to display.\n\n");
        return;
    }

    printf("List of Books:\n");
    for (int i = 0; i < count; i++) {
        printf("Book ID: %d\n", books[i].id);
        printf("Title: %s\n", books[i].title);
        printf("Author: %s\n", books[i].author);
        printf("Availability: %s\n\n", books[i].available ? "Available" : "Issued");
    }
}

// Step 4: Search Book by ID
void searchBook(struct Book books[], int count) {
    if (count == 0) {
        printf("No books in the library.\n\n");
        return;
    }

    int searchId, found = 0;
    printf("Enter Book ID to search: ");
    scanf("%d", &searchId);

    for (int i = 0; i < count; i++) {
        if (books[i].id == searchId) {
            printf("Book Found!\n");
            printf("Book ID: %d\n", books[i].id);
            printf("Title: %s\n", books[i].title);
            printf("Author: %s\n", books[i].author);
            printf("Availability: %s\n\n", books[i].available ? "Available" : "Issued");
            found = 1;
            break;
        }
    }

    if (!found) {
        printf("Book not found!\n\n");
    }
}

// Step 5: Issue a Book
void issueBook(struct Book books[], int count) {
    int id, found = 0;
    printf("Enter Book ID to issue: ");
    scanf("%d", &id);

    for (int i = 0; i < count; i++) {
        if (books[i].id == id) {
            found = 1;
            if (books[i].available == 1) {
                books[i].available = 0;
                printf("Book issued successfully!\n\n");
            } else {
                printf("Book already issued!\n\n");
            }
            break;
        }
    }

    if (!found) {
        printf("Book not found!\n\n");
    }
}

// Step 6: Return a Book
void returnBook(struct Book books[], int count) {
    int id, found = 0;
    printf("Enter Book ID to return: ");
    scanf("%d", &id);

    for (int i = 0; i < count; i++) {
        if (books[i].id == id) {
            found = 1;
            if (books[i].available == 0) {
                books[i].available = 1;
                printf("Book returned successfully!\n\n");
            } else {
                printf("Book is not issued!\n\n");
            }
            break;
        }
    }

    if (!found) {
        printf("Book not found!\n\n");
    }
}

// Step 7: Main Menu
int main() {
    struct Book books[100];
    int count = 0;
    int choice;

    do {
        printf("Library Book Management System\n");
        printf("1. Add Book\n");
        printf("2. Display All Books\n");
        printf("3. Search Book by ID\n");
        printf("4. Issue Book\n");
        printf("5. Return Book\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: addBook(books, &count); break;
            case 2: displayBooks(books, count); break;
            case 3: searchBook(books, count); break;
            case 4: issueBook(books, count); break;
            case 5: returnBook(books, count); break;
            case 6: printf("Exiting program.\n"); break;
            default: printf("Invalid choice! Try again.\n\n");
        }

    } while (choice != 6);

    return 0;
}
