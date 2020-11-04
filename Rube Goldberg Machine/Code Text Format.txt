#include <stdlib.h>
#include <stdio.h>
#include <string.h>

int choice = 1; // input choice

struct node
{
    char fname[15];
    char lname[15];
    int age;
    int year;
    struct node*next;
} *front = NULL,*rear=NULL,*front2=NULL,*rear2=NULL,*top=NULL,*prev;

//FILE HANDLING---------------------a----START-----------------------------------------------
int entryCount;
typedef struct
{
    char *f_name;
    char *l_name;
    int age_i;
    int year_i;
} Entry;

//FILE HANDLING-------------------------END-------------------------------------------------

//function declarations(prototypes)----------------------------------------------------------
void enq(char fn[],char ln[],int ag,int yr);
void enq2(char fn[],char ln[],int age2,int year2);
void enq3(char fn[],char ln[],int age4,int year4);
void dq();
void dq2();
void push(char fn[],char ln[],int age3,int year3);
void pop();
void reverse_stack();
void display_reverse();
void display_q();

//first enqueue function---------------------------------------------------------
int t=0;
void enq(char fn[],char ln[],int ag,int yr)
{

    struct node* newnode;
    newnode=(struct node *)(malloc(sizeof(struct node)));
    strcpy(newnode->fname,fn);
    strcpy(newnode->lname,ln);
    newnode->age = ag;
    newnode->year = yr;
    newnode->next=NULL;
    printf("Data Serial Number:%d\n",t+1);

    printf("%s %s,%d,%d\n\n",fn,ln,ag,yr);
    t++;
    if(front == NULL && rear == NULL)
    {
        front = rear = newnode;
    }
    else
    {
        rear->next=newnode;
        rear=newnode;
    }


}
//second enqueue function----------------------------------------------------------------------------------
void enq2(char fn[],char ln[],int age2,int year2)
{
    struct node* newnode;
    newnode=(struct node *)(malloc(sizeof(struct node)));

    strcpy(newnode->fname,fn);
    strcpy(newnode->lname,ln);
    newnode->age=age2;
    newnode->year=year2;
    newnode->next=NULL;

    if(front2 == NULL && rear2 == NULL)
    {
        front2 = rear2 = newnode;
    }
    else
    {
        rear2->next=newnode;
        rear2=newnode;
    }
}

// first dequeue function----------------------------------------------------------------
void dq()
{
    struct node *temp=front;
    if(front == NULL && rear == NULL)
    {
        printf("\nQueue is empty!\n\n");
        printf("-------------------------------------------------------------------\n");
        choice = 0;
    }
    else if(front == rear)
    {   printf("Dequeued Data: ");
        printf("%s %s,%d,%d\n\n",temp->fname,temp->lname,temp->age,temp->year);

        enq2(temp->fname,temp->lname,temp->age,temp->year);

        front = rear = NULL;
    }
    else
    {
        printf("Dequeued Data: ");
        printf("%s %s,%d,%d\n\n",temp->fname,temp->lname,temp->age,temp->year);
        enq2(temp->fname,temp->lname,temp->age,temp->year);
        front=front->next;
        free(temp);
    }
}

//second dequeue function--------------------------------------------------------------
void dq2()
{
    struct node *temp=front2;

    if(front2 == NULL && rear2 == NULL)
    {
        printf("\nQueue is empty!\n\n");
        printf("All data pushed successfully to stack\n");
        printf("\n-------------------------------------------------------------------\n");
        printf("Press 2 to reverse order of stack\n");
        printf("-------------------------------------------------------------------\n\n");

    }
    else if(front2 == rear2)
    {
        printf("Dequeued and pushed data to stack: ");
        printf("%s %s,%d,%d\n\n",temp->fname,temp->lname,temp->age,temp->year);
        push(temp->fname,temp->lname,temp->age,temp->year);    //push data to stack
        front2 = rear2 = NULL;
    }
    else
    {
        printf("Dequeued and pushed data to stack: ");
        printf("%s %s,%d,%d\n\n",temp->fname,temp->lname,temp->age,temp->year);
        push(temp->fname,temp->lname,temp->age,temp->year);   //push data to stack
        front2=front2->next;
        free(temp);
    }
}

//stack operations ---------------start----------------------------------------
//push function for stack------------------------------
void push(char fn[],char ln[],int age3,int year3)
{
    struct node * newdata;
    newdata=(struct node *)(malloc)(sizeof(struct node));

    //data initialization-------
    strcpy(newdata->fname,fn);
    strcpy(newdata->lname,ln);
    newdata->age=age3;
    newdata->year=year3;

    newdata->next=top;
    top=newdata;


}

//pop function for stack--------------------------------
void pop()
{

    struct node *temp=prev;
    if(temp==NULL)
    {
        printf("\nStack is empty\n\n");

        printf("-------------------------------------------------------------------\n");
        printf("Press 4 to display the final data of Queue\n");
        printf("-------------------------------------------------------------------\n");
    }
    else
    {

    printf("The popped element is: %s %s,%d,%d\n\n",prev->fname,prev->lname,prev->age,prev->year);
    enq3(prev->fname,prev->lname,prev->age,prev->year);
    prev=prev->next;
    free(temp);
    }

}

//reverse function for stack-----------------------------------------------
void reverse_stack()
{
    struct node*current,*nextn;
    prev =NULL;
    current=nextn=top;
    while(nextn!=NULL)
    {
        nextn=nextn->next;
        current->next=prev;
        prev= current;
        current=nextn;
    }
    display_reverse();
}
//display reverse stack-----------------------------------------------------
void display_reverse()
{
    struct node*temp;
    temp= prev;
    printf("reversed data:\n\n");
    while(temp!=NULL)
    {
        printf("%s %s,%d,%d \n",temp->fname,temp->lname,temp->age,temp->year);
        temp=temp->next;
    }
    printf("\n-------------------------------------------------------------------\n");
    printf("Press 3 to pop and requeue data one after another:\n");
    printf("-------------------------------------------------------------------\n");
}


//stack operations ---------------end------------------------------------------

//third enqueue function-------------------------------------------------------
void enq3(char fn[],char ln[],int age4,int year4)
{
    struct node* newnode;
    newnode=(struct node *)(malloc(sizeof(struct node)));
    strcpy(newnode->fname,fn);
    strcpy(newnode->lname,ln);
    newnode->age=age4;
    newnode->year=year4;
    newnode->next=NULL;

    if(front == NULL && rear == NULL)
    {
        front = rear = newnode;
    }
    else
    {
        rear->next=newnode;
        rear=newnode;
    }

}

//display final Queue data----------------------------------------------------
void display_q()
{
    struct node *temp;
    temp=front;
    printf("\nInitial Queue is preserved\n\nFinal Queue data:\n\n");

    while (temp!=rear)
    {
        printf("%s %s,%d,%d \n",temp->fname,temp->lname,temp->age,temp->year);
        temp=temp->next;
    }
    printf("%s %s,%d,%d \n",temp->fname,temp->lname,temp->age,temp->year);
    choice = 0; //exit from loop
}

//tree part-------------------------------------------------------------------------------------------
struct node1{
    int age;
    int year;
    char fName[20];
    char lName[20];
    struct node1 *left;
    struct node1 *right;
} *root = NULL;

struct node1* createNode(int age, int year, char fName[], char lName[]){
    struct node1 *newNode = malloc(sizeof(struct node1));
    newNode->age = age;
    newNode->year = year;
    strcpy(newNode->fName, fName);
    strcpy(newNode->lName, lName);
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

struct queue{
    int front, rear, size;
    struct node1* *arr;
};

struct queue* createQueue(){
    struct queue* newQueue = malloc(sizeof(struct queue));
    newQueue->front = -1;
    newQueue->rear = 0;
    newQueue->size = 0;
    newQueue->arr = (struct node1**)malloc(100 * sizeof(struct node1*));
    return newQueue;
}

void enqueue(struct queue* queue, struct node1 *temp){
    queue->arr[queue->rear++] = temp;
    queue->size++;
}

struct node1 *dequeue(struct queue *queue){
    queue->size--;
    return queue->arr[++queue->front];
}

void insertNode(int age, int year, char fName[], char lName[]){
    struct node1 *newNode = createNode(age, year, fName, lName);
    if(root == NULL){
        root = newNode;
        return;
    }
    else{
        struct queue *queue = createQueue();
        enqueue(queue, root);
        while(1){
            struct node1 *node = dequeue(queue);
            if(node->left != NULL && node->right != NULL){
                enqueue(queue, node->left);
                enqueue(queue, node->right);
            }
            else{
                if(node->left == NULL){
                    node->left = newNode;
                    enqueue(queue, node->left);
                }
                else{
                    node->right = newNode;
                    enqueue(queue, node->right);
                }
                break;
            }
        }
    }
}

//moving Contents in a linked list-----------------------------------------------------------
struct linkedList{
    int age;
    int year;
    char firstNm[20];
    char lastNm[20];
    struct linkedList *next;
} *head = NULL, *pre, *p;

//creating linked-list--------------------------------------------------------------------------
void linkTransfer(struct node1 *root){
    p = malloc(sizeof(struct linkedList));
    p->age = root->age;
    p->year = root->year;
    strcpy(p->firstNm, root->fName);
    strcpy(p->lastNm, root->lName);
    p->next = NULL;
    if(head == NULL){
        head = p;
    }
    else{
        pre->next = p;
    }
    pre = p;
}

void inOrder(struct node1* root){
    if(root == NULL){
        return;
    }
    else{
        inOrder(root->left);
        linkTransfer(root);
        inOrder(root->right);
    }
}

//printing linked-list----------------------------------------------------------------
void linklist(struct linkedList* head){
    printf("Printing Contents of linked list\n\n");
    struct linkedList *temp = head;
    while(temp != NULL){
        printf("%s %s %d %d\n", temp->firstNm, temp->lastNm, temp->age, temp->year);
        temp = temp->next;
    }
}

//post-Order----------------------------------------------------------------------------
void postOrder(struct node1 *root){
    if(root == NULL){
        return;
    }
    else{
        postOrder(root->left);
        postOrder(root->right);
         printf("%s %s %d %d\n",root->fName, root->lName, root->age, root->year);
    }
}

//preorder printing------------------------------------------------------------------
void preOrder(struct node1 *root){
    if(root == NULL){
        return;
    }
    else{
        printf("%s %s %d %d\n",root->fName, root->lName, root->age, root->year);
        preOrder(root->left);
        preOrder(root->right);
    }
}

//quick sort----------------------------------------------------------------------------

struct linkedList *getTail(struct linkedList *cur)
{
    while (cur != NULL && cur->next != NULL)
        cur = cur->next;
    return cur;
}

struct linkedList *partition(struct linkedList *head, struct linkedList *end,
                    struct linkedList **newHead, struct linkedList **newEnd)
{
    struct linkedList *pivot = end;
    struct linkedList *prev = NULL, *cur = head, *tail = pivot;

    // During partition, both the head and end of the list might change
    // which is updated in the newHead and newEnd variables
    while (cur != pivot)
    {
        if (cur->year < pivot->year)
        {
            // First node that has a value less than the pivot - becomes
            // the new head
            if ((*newHead) == NULL)
                (*newHead) = cur;

            prev = cur;
            cur = cur->next;
        }
        else // If cur node is greater than pivot
        {
            // Move cur node to next of tail, and change tail
            if (prev)
                prev->next = cur->next;
            struct linkedList *tmp = cur->next;
            cur->next = NULL;
            tail->next = cur;
            tail = cur;
            cur = tmp;
        }
    }

    // If the pivot data is the smallest element in the current list,
    // pivot becomes the head
    if ((*newHead) == NULL)
        (*newHead) = pivot;

    // Update newEnd to the current last node
    (*newEnd) = tail;

    // Return the pivot node
    return pivot;
}


//here the sorting happens exclusive of the end node
struct linkedList *quickSortRecur(struct linkedList *head, struct linkedList *end)
{
    // base condition
    if (!head || head == end)
        return head;

    struct linkedList *newHead = NULL, *newEnd = NULL;

    // Partition the list, newHead and newEnd will be updated
    // by the partition function
    struct linkedList *pivot = partition(head, end, &newHead, &newEnd);

    // If pivot is the smallest element - no need to recur for
    // the left part.
    if (newHead != pivot)
    {
        // Set the node before the pivot node as NULL
        struct linkedList *tmp = newHead;
        while (tmp->next != pivot)
            tmp = tmp->next;
        tmp->next = NULL;

        // Recur for the list before pivot
        newHead = quickSortRecur(newHead, tmp);

        // Change next of last node of the left half to pivot
        tmp = getTail(newHead);
        tmp->next = pivot;
    }

    // Recur for the list after the pivot element
    pivot->next = quickSortRecur(pivot->next, newEnd);

    return newHead;
}

// The main function for quick sort. This is a wrapper over recursive
// function quickSortRecur()
void quickSort(struct linkedList **headRef)
{
    (*headRef) = quickSortRecur(*headRef, getTail(*headRef));
}


//-----------------------------------------------------------------------------

//putNewDetail--------------------------------
struct linkedList* putNewDetail(struct linkedList *head, struct linkedList *ptr){
    struct linkedList *previous = head;
    struct linkedList *run = previous->next;
    if(head->year > ptr->year){
            ptr->next = head;
            head = ptr;
    }
    else{
        while(run != NULL){
            if(run->year > ptr->year){
                ptr->next = run;
                previous->next = ptr;
                break;
            }
            previous = run;
            run = previous->next;
            if(run == NULL){
                previous->next = ptr;
                ptr->next = run;
            }
        }
    }
    return head;
}

//-----------------------------
//tree part end---------------------------------------------------------------------------------------


//main function----------------------------------------------------------------
int main()
{
    //file handling input--------------------start-----------------------------

    FILE *fp = fopen("input.txt","r");
    Entry *entries = malloc(sizeof(Entry) * entryCount);   //allocate number of inputs
    fscanf(fp, "%i" , &entryCount);
    char first_data_fname[15],first_data_lname[15];
    int first_data_age,first_data_year;

    for (int i = 0; i < entryCount; i++)
    {

        entries[i].f_name = malloc(sizeof(char));
        entries[i].l_name = malloc(sizeof(char));
        fscanf(fp,"%s %s %i %i",entries[i].f_name, entries[i].l_name,&entries[i].age_i,&entries[i].year_i);
        if(i==0)
        {
        strcpy(first_data_fname,entries[0].f_name);
        strcpy(first_data_lname,entries[0].l_name);
        first_data_age = entries[0].age_i;
        first_data_year = entries[0].year_i;
        }
    }



    //file handling input--------------------end-------------------------------

    char ch[1];   //choice for yes or no for stack processing
    // enqueue dequeue requeue ---------------start----------------------------

    printf("Press 1 to read data from file\nPress 0 to exit\n");
    printf("-------------------------------------------------------------------\n\n");
    int r=0;
    char fn[15],ln[15];
    int ag,yr;
    do
    {

        printf("Choice:");
        scanf("%d",&choice);
        switch(choice)
        {
            case 1:
                if(r==0)
                {
                    strcpy(fn,first_data_fname);
                    strcpy(ln,first_data_lname);
                    ag = first_data_age;
                    yr = first_data_year;

                }
                else
                {
                    strcpy(fn,entries[r].f_name);
                    strcpy(ln,entries[r].l_name);
                    ag = entries[r].age_i;
                    yr = entries[r].year_i;
                }
            enq(fn,ln,ag,yr);
            if (r+1==entryCount)
                {

                    printf("Data inputs Successfull\n");
                    printf("\n");
                   printf("-------------------------------------------------------------------\n");
                   printf("Press 2 to dequeue data\nPress 0 to exit\n");
                   printf("-------------------------------------------------------------------\n\n");
                   choice=0;
                }
            r++;
            break;
            case 0:
            return 0;
            default:
            printf("Please enter valid Input\n\n");
        }

    } while(choice);
//first dequeue-------------------------------------------------------------------------
do
    {

        printf("Choice:");
        scanf("%d",&choice);
        switch(choice)
        {


            case 2:
            dq();
            break;
            case 0:
            return 0;
            default:
            printf("Please enter valid Input\n");
        }

    } while(choice);

// enqueue dequeue requeue ---------------end----------------------------------------
printf("Press Y to continue processing or any key to exit:");
scanf("%s",ch);

// Queue to stack push pop and requeue-----------------------start-------------------



if (strcmp(ch,"Y") == 0 || strcmp(ch,"y") == 0)
{
    printf("-------------------------------------------------------------------\n");
    printf("Press 1 to dequeue and push element to stack\nPress 0 to exit\n");
    printf("-------------------------------------------------------------------\n\n");
    do
    {
        printf("Choice:");
        scanf("%d",&choice);
        switch(choice)
        {
            case 1:
            dq2();
            break;
            case 2:
            reverse_stack();
            break;
            case 3:
            pop();
            break;
            case 4:
            display_q();
            case 0:
            break;
            default:
            printf("Please enter valid Input\n\n");
        }
    } while(choice);
}
else
{
    printf("-------------------------------------------------------------------\n");
    printf("Program Exited\n");
    return 0;
}

        printf("-------------------------------------------------------------------\n");
        printf("Press Y to continue or any key to exit:");
        scanf("%s",ch);
        printf("-------------------------------------------------------------------\n");

// Queue to stack push pop and requeue-----------------------end-------------------


if (strcmp(ch,"Y") == 0 || strcmp(ch,"y") == 0)
{
    int i, age, year;
    char fName[20];
    char lName[20];
    int ch, ch1, ch2, ch3;
    for(i = 0; i< entryCount; i++){
      if(i == 0){
        strcpy(fName,first_data_fname);
        strcpy(lName,first_data_lname);
        age = first_data_age;
        year = first_data_year;
      }
      else{
        strcpy(fName,entries[i].f_name);
        strcpy(lName,entries[i].l_name);
        age = entries[i].age_i;
        year = entries[i].year_i;

      }
        insertNode(age,year, fName, lName);
    }
    printf("Printing Contents of tree in Pre-Order:\n\n");
    preOrder(root);
    printf("-------------------------------------------------------------------\n");
    printf("Press 1 to continue processing or any other key to stop:");
    scanf("%d", &ch);
    printf("-------------------------------------------------------------------\n");

    if(ch == 1){
        printf("Printing Contents of tree in Post-Order:\n\n");
        postOrder(root);
        printf("\n-------------------------------------------------------------------\n");
        printf("Press 1 to continue processing or any other key to stop:");
        scanf("%d", &ch1);
        printf("-------------------------------------------------------------------\n");
        if(ch1 == 1){
            printf("Moving Contents of tree in a Linked List using In-Order traversal\n\n");
            inOrder(root);

            linklist(head);
            printf("-------------------------------------------------------------------\n");
            printf("Press 1 to continue processing or any other key to stop:");
            scanf("%d", &ch2);
            printf("-------------------------------------------------------------------\n");

            if(ch2 == 1){
                printf("\nSorting Contents of linked List:\n\n");
                quickSort(&head);
                linklist(head);
                printf("-------------------------------------------------------------------\n");
                printf("Press 1 to continue processing or any other key to stop:");
                scanf("%d", &ch3);
                printf("-------------------------------------------------------------------\n");

                if(ch3 == 1){
                    printf("Enter details in the given format (first_Name last_Name age year_of_birth):\n");
                    scanf("%s %s %d %d", fName, lName, &age, &year);
                    printf("\n");
                    struct linkedList *ptr = malloc(sizeof(struct linkedList));
                    ptr->age = age;
                    ptr->year = year;
                    strcpy(ptr->firstNm, fName);
                    strcpy(ptr->lastNm, lName);
                    head = putNewDetail(head,ptr);
                    linklist(head);
                    printf("\n-------------------------------------------------------------------\n");
                    printf("All processes Completed Successfully.\n\nPlease enter 1 to exit:");
                    scanf("%d",&choice);
                    printf("\n-------------------------------------------------------------------\n");
                    if(choice == 1)
                        {
                           printf("\nProgram exited Successfully.\n");
                        }
                }
            }
        }

    }

}
else
{
    return 0;
}


    return 0;
}

