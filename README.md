#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Structure for each credit card application
struct node {
    char name[50];
    char gender[10];
    char address[100];
    char date[15];
    char time[10];
    char ifsc[20];
    char acc_no[20];
    float balance;
    char service_type[20]; // Internet Banking / Credit Card / Debit Card
    char phone[15];
    char transaction_status[20]; // Pending / Successful
    char pan[15];
    char aadhar[20];
    char payment_status[20]; // Successful / Failed
    struct node *next;
};

// Global queue pointers
struct node *front = NULL, *rear = NULL;

// Enqueue - Apply
void enqueue(char name[], char gender[], char address[], char date[], char time[],
             char ifsc[], char acc_no[], float balance, char service_type[],
             char phone[], char transaction_status[], char pan[], char aadhar[], char payment_status[]) {
    
    struct node *nn = (struct node *)malloc(sizeof(struct node));
    if (nn == NULL) {
        printf("Memory allocation failed.\n");
        return;
    }

    strcpy(nn->name, name);
    strcpy(nn->gender, gender);
    strcpy(nn->address, address);
    strcpy(nn->date, date);
    strcpy(nn->time, time);
    strcpy(nn->ifsc, ifsc);
    strcpy(nn->acc_no, acc_no);
    nn->balance = balance;
    strcpy(nn->service_type, service_type);
    strcpy(nn->phone, phone);
    strcpy(nn->transaction_status, transaction_status);
    strcpy(nn->pan, pan);
    strcpy(nn->aadhar, aadhar);
    strcpy(nn->payment_status, payment_status);
    nn->next = NULL;

    if (rear == NULL) {
        front = rear = nn;
    } else {
        rear->next = nn;
        rear = nn;
    }

    printf("Application submitted successfully for %s.\n", name);
}

// Dequeue - Process the next application
void dequeue() {
    if (front == NULL) {
        printf("No applications to process.\n");
        return;
    }

    struct node *temp = front;
    printf("\n--- Processed Application ---\n");
    printf("Name: %s | Gender: %s | Phone: %s\n", temp->name, temp->gender, temp->phone);
    printf("Address: %s\n", temp->address);
    printf("Date: %s | Time: %s\n", temp->date, temp->time);
    printf("IFSC: %s | Account No: %s | Balance: %.2f\n", temp->ifsc, temp->acc_no, temp->balance);
    printf("Service: %s | PAN: %s | Aadhar: %s\n", temp->service_type, temp->pan, temp->aadhar);
    printf("Transaction: %s | Payment: %s\n", temp->transaction_status, temp->payment_status);

    front = front->next;
    if (front == NULL)
        rear = NULL;

    free(temp);
}

// Peek - View all pending applications
void peek() {
    if (front == NULL) {
        printf("No pending applications.\n");
        return;
    }

    struct node *temp = front;
    printf("\n--- Pending Credit Card Applications ---\n");
    while (temp != NULL) {
        printf("\nName: %s | Gender: %s | Phone: %s\n", temp->name, temp->gender, temp->phone);
        printf("Address: %s\n", temp->address);
        printf("Date: %s | Time: %s\n", temp->date, temp->time);
        printf("IFSC: %s | Account No: %s | Balance: %.2f\n", temp->ifsc, temp->acc_no, temp->balance);
        printf("Service: %s | PAN: %s | Aadhar: %s\n", temp->service_type, temp->pan, temp->aadhar);
        printf("Transaction: %s | Payment: %s\n", temp->transaction_status, temp->payment_status);
        temp = temp->next;
    }
}

// Main menu
int main() {
    int choice;
    char name[50], gender[10], address[100], date[15], time[10];
    char ifsc[20], acc_no[20], service_type[20], phone[15];
    char transaction_status[20], pan[15], aadhar[20], payment_status[20];
    float balance;

    while (1) {
        printf("\n===== Credit Card Application Menu =====\n");
        printf("1. Apply for Service\n");
        printf("2. View All Applications\n");
        printf("3. Process Next Application\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        getchar();

        switch (choice) {
            case 1:
                printf("Enter Name: "); fgets(name, sizeof(name), stdin); name[strcspn(name, "\n")] = 0;
                printf("Enter Gender: "); fgets(gender, sizeof(gender), stdin); gender[strcspn(gender, "\n")] = 0;
                printf("Enter Address: "); fgets(address, sizeof(address), stdin); address[strcspn(address, "\n")] = 0;
                printf("Enter Date (dd/mm/yyyy): "); fgets(date, sizeof(date), stdin); date[strcspn(date, "\n")] = 0;
                printf("Enter Time (hh:mm): "); fgets(time, sizeof(time), stdin); time[strcspn(time, "\n")] = 0;
                printf("Enter IFSC Code: "); fgets(ifsc, sizeof(ifsc), stdin); ifsc[strcspn(ifsc, "\n")] = 0;
                printf("Enter Account Number: "); fgets(acc_no, sizeof(acc_no), stdin); acc_no[strcspn(acc_no, "\n")] = 0;
                printf("Enter Account Balance: "); scanf("%f", &balance); getchar();
                printf("Enter Service Type (Internet/Credit/Debit): "); fgets(service_type, sizeof(service_type), stdin); service_type[strcspn(service_type, "\n")] = 0;
                printf("Enter Phone Number: "); fgets(phone, sizeof(phone), stdin); phone[strcspn(phone, "\n")] = 0;
                printf("Enter Transaction Status (Pending/Successful): "); fgets(transaction_status, sizeof(transaction_status), stdin); transaction_status[strcspn(transaction_status, "\n")] = 0;
                printf("Enter PAN Number: "); fgets(pan, sizeof(pan), stdin); pan[strcspn(pan, "\n")] = 0;
                printf("Enter Aadhar Number: "); fgets(aadhar, sizeof(aadhar), stdin); aadhar[strcspn(aadhar, "\n")] = 0;
                printf("Enter Payment Status (Successful/Failed): "); fgets(payment_status, sizeof(payment_status), stdin); payment_status[strcspn(payment_status, "\n")] = 0;

                enqueue(name, gender, address, date, time, ifsc, acc_no, balance,
                        service_type, phone, transaction_status, pan, aadhar, payment_status);
                break;

            case 2:
                peek();
                break;

            case 3:
                dequeue();
                break;

            case 4:
                printf("Thank you for using the Application System.\n");
                exit(0);

            default:
                printf("Invalid choice. Try again.\n");
        }
    }

    return 0;
}
