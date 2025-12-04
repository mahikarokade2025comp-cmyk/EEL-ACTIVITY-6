# EEL-ACTIVITY-6
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void markAttendance();
void viewAttendance();
void searchAttendance();

int main() {
    int choice;

    while (1) {
        printf("\n===== SMART ATTENDANCE SYSTEM =====\n");
        printf("1. Mark Attendance\n");
        printf("2. View Attendance\n");
        printf("3. Search Attendance\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                markAttendance();
                break;
            case 2:
                viewAttendance();
                break;
            case 3:
                searchAttendance();
                break;
            case 4:
                exit(0);
            default:
                printf("Invalid choice! Try again.\n");
        }
    }
}

void markAttendance() {
    FILE *fp;
    fp = fopen("attendance.txt", "a");

    if (fp == NULL) {
        printf("Error opening file!\n");
        return;
    }

    char name[50];
    printf("Enter name: ");
    scanf("%s", name);

    fprintf(fp, "%s - Present\n", name);

    printf("Attendance marked successfully for %s\n", name);
    fclose(fp);
}

void viewAttendance() {
    FILE *fp;
    fp = fopen("attendance.txt", "r");

    if (fp == NULL) {
        printf("No attendance record found!\n");
        return;
    }

    char line[200];
    printf("\n--- All Attendance Records ---\n");

    while (fgets(line, sizeof(line), fp)) {
        printf("%s", line);
    }

    fclose(fp);
}

void searchAttendance() {
    FILE *fp;
    fp = fopen("attendance.txt", "r");

    if (fp == NULL) {
        printf("No attendance record found!\n");
        return;
    }

    char name[50], line[200];
    int found = 0;

    printf("Enter name to search: ");
    scanf("%s", name);

    while (fgets(line, sizeof(line), fp)) {
        if (strstr(line, name)) {
            printf("Record Found: %s", line);
            found = 1;
        }
    }

    if (!found) {
        printf("No attendance record found for %s\n", name);
    }

    fclose(fp);
}
