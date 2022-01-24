# projects-
1. Problem statement: Given a linked list reverse it up to first N elements without using any additional spac
#include <stdio.h>
#include <stdlib.h>

struct node{
	int data; // data field
	struct node *next;
};

void display(struct node* head){
	struct node* current=head; // current node set to head
	
	printf("traversing the list...\n");
	while(current!=NULL){ //traverse until current node isn't NULL
		printf("%d ",current->data);
		current=current->next; // go to next node		
	}	
}

struct node* reverse_N(struct node* head,struct node* temp,int n){
	struct node *next=NULL,*cur=head,*prev=temp; //initialize the pointers
	int count=0;
	while(cur!=NULL && (count++)<n){//loop till the end of linked list
		next=cur->next;//next = cur->next to store the rest of the list;
		cur->next=prev;//change the direction of linked list
		prev=cur; //update prev
		cur=next; //update cur
	}
    
	head=prev; //update head
	return head; //return head
}

struct node* creatnode(int d){
	struct node* temp=malloc(sizeof(struct node));
	temp->data=d;
	temp->next=NULL;
	return temp;
}

int main(){
	printf("creating the linked list by inserting new nodes at the end\n");
	
	printf("enter 0 to stop building the list, else enter any integer\n");
	
	int k,count=0,x=1,n;
	
	struct node* curr,*temp;
	
	scanf("%d",&k);
	struct node* head=creatnode(k); //buliding list, first node
	scanf("%d",&k);
	temp=head;
	///////////////////inserting at the end//////////////////////
	while(k){
	curr=creatnode(k);
	temp->next=curr;//appending each node
	temp=temp->next;
	x++;
	scanf("%d",&k);
	}
	display(head); // displaying the list
	printf("\nInput N\n");
	while(1){
		scanf("%d",&n);
		if(n<x)
		break;
		printf("N greater than no of element, enter again\n");
	}
	
	printf("\nreversing upto first N elements...\n");
	
	//traversing to the node from which no reversing needed
	temp=head;
	while((count++)<n){
		temp=temp->next;
	}
	
	head=reverse_N(head,temp,n);
	display(head); // displaying the reversed( only first N terms) list
	
	return 0;
}
![image](https://user-images.githubusercontent.com/98012187/150728914-5e1bc5c5-d023-458a-9770-8a85e535b150.png)


2. program to implement linked list
#include <iostream>
 
using namespace std;
 
//Declare Node 
struct Node{
    int num;
    Node *next;
};
 
//Declare starting (Head) node
struct Node *head=NULL;
 
//Insert node at start
void insertNode(int n){
    struct Node *newNode=new Node;
    newNode->num=n;
    newNode->next=head;
    head=newNode;
}
 
//Traverse/ display all nodes (print items)
void display(){
    if(head==NULL){
        cout<<"List is empty!"<<endl;
        return;
    }
    struct Node *temp=head;
    while(temp!=NULL){
        cout<<temp->num<<" ";
        temp=temp->next;
    }
    cout<<endl;
}
 
//delete node from start
void deleteItem(){
    if(head==NULL){
        cout<<"List is empty!"<<endl;
        return;
    }
    cout<<head->num<<" is removed."<<endl;
    head=head->next;
}
int main(){
     
    display();
    insertNode(10);
    insertNode(20);
    insertNode(30);
    insertNode(40);
    insertNode(50);
    display();
    deleteItem(); deleteItem(); deleteItem(); deleteItem(); deleteItem();
    deleteItem();
    display();
    return 0;
}

	
	3. 
	// C++ program for the above approach
#include <iostream>
using namespace std;

// Node class to represent
// a node of the linked list.
class Node {
public:
	int data;
	Node* next;

	// Default constructor
	Node()
	{
		data = 0;
		next = NULL;
	}

	// Parameterised Constructor
	Node(int data)
	{
		this->data = data;
		this->next = NULL;
	}
};

// Linked list class to
// implement a linked list.
class Linkedlist {
	Node* head;

public:
	// Default constructor
	Linkedlist() { head = NULL; }

	// Function to insert a
	// node at the end of the
	// linked list.
	void insertNode(int);

	// Function to print the
	// linked list.
	void printList();

	// Function to delete the
	// node at given position
	void deleteNode(int);
};

// Function to delete the
// node at given position
void Linkedlist::deleteNode(int nodeOffset)
{
	Node *temp1 = head, *temp2 = NULL;
	int ListLen = 0;

	if (head == NULL) {
		cout << "List empty." << endl;
		return;
	}

	// Find length of the linked-list.
	while (temp1 != NULL) {
		temp1 = temp1->next;
		ListLen++;
	}

	// Check if the position to be
	// deleted is less than the length
	// of the linked list.
	if (ListLen < nodeOffset) {
		cout << "Index out of range"
			<< endl;
		return;
	}

	// Declare temp1
	temp1 = head;

	// Deleting the head.
	if (nodeOffset == 1) {

		// Update head
		head = head->next;
		delete temp1;
		return;
	}

	// Traverse the list to
	// find the node to be deleted.
	while (nodeOffset-- > 1) {

		// Update temp2
		temp2 = temp1;

		// Update temp1
		temp1 = temp1->next;
	}

	// Change the next pointer
	// of the previous node.
	temp2->next = temp1->next;

	// Delete the node
	delete temp1;
}

// Function to insert a new node.
void Linkedlist::insertNode(int data)
{
	// Create the new Node.
	Node* newNode = new Node(data);

	// Assign to head
	if (head == NULL) {
		head = newNode;
		return;
	}

	// Traverse till end of list
	Node* temp = head;
	while (temp->next != NULL) {

		// Update temp
		temp = temp->next;
	}

	// Insert at the last.
	temp->next = newNode;
}

// Function to print the
// nodes of the linked list.
void Linkedlist::printList()
{
	Node* temp = head;

	// Check for empty list.
	if (head == NULL) {
		cout << "List empty" << endl;
		return;
	}

	// Traverse the list.
	while (temp != NULL) {
		cout << temp->data << " ";
		temp = temp->next;
	}
}

// Driver Code
int main()
{
	Linkedlist list;

	// Inserting nodes
	list.insertNode(1);
	list.insertNode(2);
	list.insertNode(3);
	list.insertNode(4);

	cout << "Elements of the list are: ";

	// Print the list
	list.printList();
	cout << endl;

	// Delete node at position 2.
	list.deleteNode(2);

	cout << "Elements of the list are: ";
	list.printList();
	cout << endl;
	return 0;
}
