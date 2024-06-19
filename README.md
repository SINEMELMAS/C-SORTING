# C-SORTING
C++
#include <iostream>
#include <cstring>

struct student {
    char firstName[20];
    char lastName[20];
    unsigned int age;
    char gender;
    int level;
};

class MyLinkedList {
private:
    struct Node {
        student data;
        Node* next;
    };

    Node* head;

public:
    MyLinkedList() : head(nullptr) {}

    void insertNode(student data) {
        Node* newNode = new Node;
        newNode->data = data;
        newNode->next = nullptr;

        if (head == nullptr) {
            head = newNode;
        } else {
            Node* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
    }

    void displayList() {
        Node* temp = head;
        while (temp != nullptr) {
            std::cout << "Name: " << temp->data.firstName << " " << temp->data.lastName
                      << ", Age: " << temp->data.age
                      << ", Gender: " << temp->data.gender
                      << ", Level: " << temp->data.level << std::endl;
            temp = temp->next;
        }
    }

    void bubbleSort() {
        Node* current;
        Node* next;
        student temp;

        for (current = head; current != nullptr; current = current->next) {
            for (next = current->next; next != nullptr; next = next->next) {
                if (current->data.age > next->data.age) {
                    temp = current->data;
                    current->data = next->data;
                    next->data = temp;
                }
            }
        }
    }

    void insertionSort() {
        Node* current;
        Node* temp;
        student key;

        for (current = head->next; current != nullptr; current = current->next) {
            key = current->data;
            temp = current->next;

            while (temp != nullptr && temp->data.age < key.age) {
                temp->next->data = temp->data;
                temp = temp->next;
            }

            temp->data = key;
        }
    }

    void selectionSort() {
        Node* current;
        Node* next;
        Node* minNode;
        student temp;

        for (current = head; current != nullptr; current = current->next) {
            minNode = current;

            for (next = current->next; next != nullptr; next = next->next) {
                if (next->data.age < minNode->data.age) {
                    minNode = next;
                }
            }

            temp = current->data;
            current->data = minNode->data;
            minNode->data = temp;
        }
    }
};

int main() {
    MyLinkedList myList;
    int numStudents;
    student newStudent;

    std::cout << "Enter the number of students: ";
    std::cin >> numStudents;

    for (int i = 0; i < numStudents; ++i) {
        std::cout << "\nEnter information for student " << i + 1 << ":\n";
        std::cout << "First Name: ";
        std::cin >> newStudent.firstName;
        std::cout << "Last Name: ";
        std::cin >> newStudent.lastName;
        std::cout << "Age: ";
        std::cin >> newStudent.age;
        std::cout << "Gender (M/F): ";
        std::cin >> newStudent.gender;
        std::cout << "Level: ";
        std::cin >> newStudent.level;

        myList.insertNode(newStudent);
    }

    int sortChoice;
    std::cout <<"~~ WELCOME Sorting Algorithms program ~~ \n";
    std::cout << "Select and Enter Your Choice from the Menu :\n";
    std::cout <<" O (n * n) Sorting Algorithms programs :\n";
    std::cout << "1. Bubble Sort\n";
    std::cout << "2. Insertion Sort\n";
    std::cout << "3. Selection Sort\n";
    std::cout << "Enter choice: ";
    std::cin >> sortChoice;

    switch (sortChoice) {
        case 1:
            myList.bubbleSort();
            std::cout << "Sorted list by age using Bubble Sort:\n";
            myList.displayList();
            break;
        case 2:
            myList.insertionSort();
            std::cout << "Sorted list by age using Insertion Sort:\n";
            myList.displayList();
            break;
        case 3:
            myList.selectionSort();
            std::cout << "Sorted list by age using Selection Sort:\n";
            myList.displayList();
            break;
        default:
            std::cout << "Invalid choice. Exiting program.\n";
    }

    return 0;
}
