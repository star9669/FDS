#include <iostream>
#define MAX 10
using namespace std;

struct Queue {
    int arr[MAX];
    int front, rear;
};

void init(Queue &q) {
    q.front = q.rear = -1;
}

bool isEmpty(const Queue &q) {
    return q.front == -1;
}

bool isFull(const Queue &q) {
    return (q.rear + 1) % MAX == q.front;
}

void insertFront(Queue &q, int data) {
    if (isFull(q)) {
        cout << "Queue is full! Cannot insert at front.\n";
    } else {
        if (isEmpty(q)) {
            q.front = q.rear = 0;
        } else {
            q.front = (q.front - 1 + MAX) % MAX;
        }
        q.arr[q.front] = data;
        cout << "Data inserted at front: " << data << endl;
    }
}

void insertRear(Queue &q, int data) {
    if (isFull(q)) {
        cout << "Queue is full! Cannot insert at rear.\n";
    } else {
        if (isEmpty(q)) {
            q.front = q.rear = 0;
        } else {
            q.rear = (q.rear + 1) % MAX;
        }
        q.arr[q.rear] = data;
        cout << "Data inserted at rear: " << data << endl;
    }
}

int deleteFront(Queue &q) {
    if (isEmpty(q)) {
        cout << "Queue is empty! Cannot delete from front.\n";
        return -1;
    } else {
        int data = q.arr[q.front];
        if (q.front == q.rear) {
            init(q); // Reset the queue when it's empty
        } else {
            q.front = (q.front + 1) % MAX;
        }
        return data;
    }
}

int deleteRear(Queue &q) {
    if (isEmpty(q)) {
        cout << "Queue is empty! Cannot delete from rear.\n";
        return -1;
    } else {
        int data = q.arr[q.rear];
        if (q.front == q.rear) {
            init(q); // Reset the queue when it's empty
        } else {
            q.rear = (q.rear - 1 + MAX) % MAX;
        }
        return data;
    }
}

void display(const Queue &q) {
    if (isEmpty(q)) {
        cout << "Queue is empty!\n";
    } else {
        cout << "Queue elements: ";
        int i = q.front;
        while (i != q.rear) {
            cout << q.arr[i] << " ";
            i = (i + 1) % MAX;
        }
        cout << q.arr[q.rear] << endl;
    }
}

int main() {
    Queue q;
    int choice, data;
    init(q);

    do {
        cout << "\n1. Insert at Front";
        cout << "\n2. Insert at Rear";
        cout << "\n3. Delete from Front";
        cout << "\n4. Delete from Rear";
        cout << "\n5. Display Queue";
        cout << "\n6. Exit";
        cout << "\nEnter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter data to insert at front: ";
                cin >> data;
                insertFront(q, data);
                break;
            case 2:
                cout << "Enter data to insert at rear: ";
                cin >> data;
                insertRear(q, data);
                break;
            case 3:
                data = deleteFront(q);
                if (data != -1) {
                    cout << "Deleted data from front: " << data << endl;
                }
                break;
            case 4:
                data = deleteRear(q);
                if (data != -1) {
                    cout << "Deleted data from rear: " << data << endl;
                }
                break;
            case 5:
                display(q);
                break;
            case 6:
                cout << "Exiting program...\n";
                break;
            default:
                cout << "Invalid choice. Please try again.\n";
        }
    } while (choice != 6);

    return 0;
}
