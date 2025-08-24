# Student-assignment-submission-tracker
/*Maintaining student academic records is a critical task in every  educational institution. As the volume of data grows and changes frequently, static data storage methods such as spreadsheets become inefficient. A dynamic system is needed to efficiently manage student information, including adding new students, deleting records.*/
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Define the structure for an assignment submission node
struct Assignment {
    char studentId[20];
    char assignmentTitle[50];
    char submissionDate[20];
    char status[20];
    struct Assignment* next;
};

// Global head of the linked list
struct Assignment* head = NULL;

// Function to add a new submission record
void addRecord(const char* studentId, const char* assignmentTitle, const char* submissionDate, const char* status) {
    // Allocate memory for the new node
    struct Assignment* newRecord = (struct Assignment*)malloc(sizeof(struct Assignment));
    if (newRecord == NULL) {
        printf("Memory allocation failed!\n");
        return;
    }

    // Copy data into the new node
    strcpy(newRecord->studentId, studentId);
    strcpy(newRecord->assignmentTitle, assignmentTitle);
    strcpy(newRecord->submissionDate, submissionDate);
    strcpy(newRecord->status, status);
    newRecord->next = NULL;

    // Add the new node to the end of the list
    if (head == NULL) {
        head = newRecord;
    } else {
        struct Assignment* current = head;
        while (current->next != NULL) {
            current = current->next;
        }
        current->next = newRecord;
    }
    printf("Submission record added successfully.\n");
}

// Function to update the status of a record
void updateStatus(const char* studentId, const char* assignmentTitle, const char* newStatus) {
    struct Assignment* current = head;
    int found = 0;
    while (current != NULL) {
        if (strcmp(current->studentId, studentId) == 0 && strcmp(current->assignmentTitle, assignmentTitle) == 0) {
            strcpy(current->status, newStatus);
            found = 1;
            printf("Status updated for Student ID: %s\n", studentId);
            break;
        }
        current = current->next;
    }
    if (!found) {
        printf("Record not found for Student ID: %s and Title: %s\n", studentId, assignmentTitle);
    }
}

// Function to search submissions by Student ID
void searchSubmissions(const char* studentId) {
    struct Assignment* current = head;
    int found = 0;
    printf("Searching for submissions for Student ID: %s\n", studentId);
    while (current != NULL) {
        if (strcmp(current->studentId, studentId) == 0) {
            printf("Student ID: %s, Title: %s, Date: %s, Status: %s\n",
                   current->studentId, current->assignmentTitle, current->submissionDate, current->status);
            found = 1;
        }
        current = current->next;
    }
    if (!found) {
        printf("No submissions found for Student ID: %s\n", studentId);
    }
}

// Function to display all records
void displayAllRecords() {
    struct Assignment* current = head;
    if (current == NULL) {
        printf("No submission records found.\n");
        return;
    }
    printf("--- All Submission Records ---\n");
    while (current != NULL) {
        printf("Student ID: %s, Title: %s, Date: %s, Status: %s\n",
               current->studentId, current->assignmentTitle, current->submissionDate, current->status);
        current = current->next;
    }
    printf("------------------------------\n");
}

// Main function to run the program and user interface
int main() {
    int choice;
    char studentId[20], assignmentTitle[50], submissionDate[20], status[20];

    do {
        printf("\n--- Student Assignment Submission Tracker ---\n");
        printf("1. Add new submission record\n");
        printf("2. Update submission status\n");
        printf("3. Search submissions by Student ID\n");
        printf("4. Display all records\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        // Consume the newline character left by scanf()
        while
