# Linked Lists

## Quick Overview

![Linked List](https://upload.wikimedia.org/wikipedia/commons/6/6d/Singly-linked-list.svg)

* A linked list is a linear data structure where each element is a separate object.

* Each element (we will call it a **node**) of a list is comprising of two items - the data and a reference to the next node. 
* The last node has a reference to null. 

* The entry point into a linked list is called the **head** of the list. It should be noted that head is not a separate node, but the reference to the first node. **If the list is empty then the head is a null reference.**

* A linked list is a **dynamic data structure**. The number of nodes in a list is not fixed and can grow and shrink on demand. Any application which has to deal with an unknown number of objects will need to use a linked list.

## Types of Linked Lists
### **Singly Linked List**
A linked list in which each node has a single reference: one to the next node.
![Singly Linked List](http://upload.wikimedia.org/wikipedia/commons/6/6d/Singly-linked-list.svg)


### **Doubly Linked List**
A linked list in which each node has two references: one to the next node and another to previous node.
![Doubly Linked List](http://upload.wikimedia.org/wikipedia/commons/5/5e/Doubly-linked-list.svg)

### **Circular Linked List**
Similar to doubly linked list, except that the last node of the list points back to the first node (or the head) of the list.

![Circular Linked List](http://upload.wikimedia.org/wikipedia/commons/d/df/Circularly-linked-list.svg)


## Common Linked List Functions

The following functions are written in C for use with a singly linked list.

### Define a Linked List Node
```c
struct node {
    int data;              // data stored inside a node
    struct node* next;     // pointer to the next node
};
```

### Create a Linked List
```c
struct node* head = NULL;
head = malloc(sizeof(struct node));
if (head == NULL) return 1;    // make sure malloc doesn't return NULL
head->val = 1;
head->next = NULL;
```

### Length of a linked list
```c
/* 
Given a linked list head pointer, compute
and return the number of nodes in the list.
*/
int Length(struct node* head) {
    struct node* current = head;
    int count = 0;
    
    while (current != NULL) {
        count++;
        current = current->next;
    }
    
    return count;
}
```

### Adding an item at the beginning of the list (push)
Here, we need **a double pointer** (i.e a pointer to a ```node*```) because we need to change the head pointer that is 
passed to the function as a function argument, and to do so, we need a double pointer. You can read more [here](http://stackoverflow.com/questions/5580761/why-use-double-pointer-or-why-use-pointers-to-pointers).

```c
void push(struct node** headRef, int val) {
    struct node* newNode;
    newNode = malloc(sizeof(struct node));
    newNode->data = val;
    newNode->next = *headRef;    // Former 1st node is now the second in list
    *headRef = newNode;          // newNode is now the 1st one
}

```


### Adding an item at the end of the list (append)
Again, we pass in a double pointer (```node**```) because we *might* need to change the head pointer, 
if the linked list is empty. (Notice, in this case, it is the same as the above method.)

```c
/*
Given a head pointer to the start of a linked list,
and an integer value, add a new node with the value
at the end of the linked list.
*/
void append(struct node** headRef, int val) {
    struct node* current = *headRef;    // current points to the first node
    
    struct node* newNode;
    newNode = malloc(sizeof(struct node));
    newNode->data = val;
    newNode->next = NULL;
    
    // Special case for length 0
    if (current == NULL) {
        *headRef = newNode;
    } else {
        // Locate the last node, and append our newNode.
        while (current->next != NULL) {
            current = current->next;
        }
        current->next = newNode;  
    }  
}
```

## References
* This guide is based on: https://www.cs.cmu.edu/~adamchik/15-121/lectures/Linked%20Lists/linked%20lists.html

* To learn more about Linked Lists: http://cslibrary.stanford.edu/103/LinkedListBasics.pdf

* For Linked List implementation in C: http://www.learn-c.org/en/Linked_lists
