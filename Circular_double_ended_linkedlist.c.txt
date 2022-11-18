//Circular double ended linked list
#include<stdio.h>  
#include<stdlib.h>  
struct node  
{  
    struct node *prev;  
    struct node *next;  
    int data;  
};  
struct node *getnode() {
    return ((struct node *)malloc(sizeof(struct node)));
}

struct node *head = NULL;  

void insert_atBeginning();  
void insert_atEnd();  
void insert_atLocation();  
void delete_atBeginning();  
void delete_atEnd();  
void delete_atLocation();  
void display();  
void search();
void concatenate();
void split();
void copy();
void reverse(); 

int main ()  
{  
    int choice;  
    while(1)
    {  
        printf("\nLinked list functions");
        printf("\n1.Insert at Beginning	\n2.Insert at End	\n3.Insert at Position		\n4.Delete at Beginning		\n5.Delete at End");
        printf("\n6.Delete at Position      \n7.Display     \n8.Search      \n9.Reverse     \n10.Copy       \n11.Concatenate");
        printf("\n12.Split     \n13.Exit");            
        
        printf("\nEnter your choice : ");
        scanf("%d", &choice);
        printf("\n");
                
        switch(choice)  
        {  
            case 1: insert_atBeginning();  
                    break;  
            
            case 2: insert_atEnd();  
                    break;  
            
            case 3: insert_atLocation();  
                    break;  
                
            case 4: delete_atBeginning();  
                    break;  
            
            case 5: delete_atEnd();  
                    break;  
                
            case 6: delete_atLocation();  
                    break;  
            
            case 7: display(); 
                    break;  

            case 8: search();  
                    break;  
            
            case 9: reverse();  
                    break;  
            
            case 10: copy(); 
                    break;  

            case 11: concatenate();  
                    break;  
            
            case 12: split();  
                    break;  
            
            case 13: return 0; 
            
            default: printf("Invalid choice!");  
        }  
    }  

}  

void insert_atBeginning()  
{  
    struct node *newnode;   
    int n;  
    newnode = getnode();  
    
    printf("\nEnter node value : ");  
    scanf("%d",&n);  
        
    if(head==NULL)  
    {  
        newnode->next = NULL;  
        newnode->prev=NULL;  
        newnode->data=n;  
        head=newnode;  
    } else {  
        newnode->data=n;  
        newnode->prev=NULL;  
        newnode->next = head;  
        head->prev=newnode;  
        head=newnode;  
    }
    display();   
          
}  

void insert_atEnd()  
{  
    struct node *newnode,*temp;  
    int n;  
    newnode = getnode();  
    
    printf("\nEnter node value : ");  
    scanf("%d",&n);  
    newnode->data=n;  
    if(head == NULL)  
    {  
       newnode->next = NULL;  
        newnode->prev = NULL;  
        head = newnode;  
    }  
    else  
    {  
        temp = head;  
        while(temp->next!=NULL)  
        {  
            temp = temp->next;  
        }  
        temp->next = newnode;  
        newnode ->prev=temp;
        newnode->next = NULL;  
    }
    display();  

}  

void insert_atLocation()  
{  
    struct node *newnode,*temp;  
    int n,loc,i;  
    newnode = getnode();    
    temp=head;  
    printf("Enter the location");  
    scanf("%d",&loc);  
    for(i=0;i<loc;i++)  
    {  
       temp = temp->next;  
       if(temp == NULL)  
       {  
           printf("\nThere are less than %d elements", loc);  
           return;  
        }  
    }  
    printf("Enter value");  
    scanf("%d",&n);  
    newnode->data = n;  
    newnode->next = temp->next;  
    newnode -> prev = temp;  
    temp->next = newnode;  
    temp->next->prev=newnode;  
    display();

}  

void delete_atBeginning()  
{  
    struct node *newnode;  
    if(head == NULL)  
    {  
        printf("\nList is empty!\n");  
    }  
    else if(head->next == NULL)  
    {  
        head = NULL;   
        free(head);   
    }  
    else  
    {  
        newnode = head;  
        head = head -> next;  
        head -> prev = NULL;  
        free(newnode);  
        
    }  
    display(); 

}  

void delete_atEnd()  
{  
    struct node *newnode;  
    if(head == NULL)  
    {  
        printf("\nList is empty!\n");  
    }  
    else if(head->next == NULL)  
    {  
        head = NULL;   
        free(head);   
    }  
    else   
    {  
        newnode = head;   
        if(newnode->next != NULL)  
        {  
            newnode = newnode -> next;   
        }  
        newnode -> prev -> next = NULL;   
        free(newnode);  
        
    } 
    display();  

} 

void delete_atLocation()  
{  
    struct node *newnode, *temp;  
    int val;  
    printf("\n Enter the data after which the node is to be deleted : ");  
    scanf("%d", &val);  
    newnode = head;  
    while(newnode -> data != val)  
        newnode = newnode -> next;  
    if(newnode -> next == NULL)  
    {  
        printf("Since there are lesser elements in list, no node was deleted!\n");  
    }  
    else if(newnode -> next -> next == NULL)  
    {  
        newnode ->next = NULL;  
    }  
    else  
    {   
        temp = newnode -> next;  
        newnode -> next = temp -> next;  
        temp -> next -> prev = newnode;  
        free(temp);
    }
    display();      
}  

void display()  
{  
    struct node *newnode;
    newnode = head;  
    if(newnode == NULL)  
    {  
        printf("\nList is empty!\n");  
    }  
    else  
    {   
        while(newnode != NULL)  
        {  
            printf("%d -> ",newnode->data);  
            newnode=newnode->next;  
        }  
    }

}  

void search()  
{  
    struct node *newnode;  
    int n,count=0;  
    newnode = head;   
    if(newnode == NULL)  
    {  
        printf("\nList is empty!\n");  
    }  
    else  
    {   
        printf("\nEnter node to be searched : ");   
        scanf("%d",&n);  
        while (newnode!=NULL)  
        {  
            if(newnode->data == n)  
            {  
                printf("\nNode found!");  
                count++;  
                break;  
            }   
            newnode = newnode -> next;  
        }  
        if(count==0)  
        {  
            printf("\nItem not found!\n");  
        }  
    }     
          
}  

void copy(){
    //working on it
}

void concatenate(){
    //working on it
}

void split(){
    //working on it
}

void reverse(){
    //working on it
}