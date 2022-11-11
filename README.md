/*DSA Assignment 2 To create a Club*/
#include <stdio.h>  
#include<string.h>
#include<stdlib.h>

struct club
{
    char name[20];
    int prn;
    struct club *prv;
    struct club *next;
    
};

void inserts(struct club *); 
void insertm(struct club*);
struct club* deletep(struct club *); 
void deletes(struct club*);
void deletem(struct club *);
void count(struct club *);
void reverse(struct club *);
void display(struct club *head);

void main()
{ 
    struct club *head;
    head=(struct club *)malloc(sizeof(struct club));
    printf("Enter name of President:");
    scanf(" %s",head->name);
    printf("Enter PRN of President:");
    scanf("%d",&head->prn);
    head->next=NULL;
    head->prv=NULL;
    inserts(head); 
    int choice,y;
    do{
        printf("\n1.insert member \n2.delete president \n3.delete secreatary \n4.delete member \n5.count \n6.reverse \n7.display");
        printf("\nEnter your choice:");
        scanf("%d",&choice); 
        struct club *temp;
        temp=head;
        switch(choice){
           
        case 1:insertm(head);
                break;
        case 2:head=deletep(head);
                break;
        case 3:deletes(head);
                break;
        case 4:deletem(head);
                break;
        case 5:count(head);
                break;
        case 6:while(temp->next!=NULL){
               temp=temp->next;
               }
               reverse(temp);
                break;
        case 7:display(head);
                break;
        default:
                printf("Invalid choice");
        } 
       printf("\nDo you want to continue (0:NO/1:YES):");
       scanf("%d",&y); 
    } 
    while(y==1);
} 

void inserts(struct club *head)
{ 
    struct club *new;
    new=(struct club *)malloc(sizeof(struct club));
    printf("Enter name of Secreatary:");
    scanf(" %s",new->name);
    printf("Enter PRN of secreatary:");
    scanf("%d",&new->prn);
    new->next=NULL;
    new->prv=NULL; 
    head->next=new;
    new->prv=head;
    
}

void insertm(struct club *head)
{ 
    struct club *new,*temp;
    new=(struct club *)malloc(sizeof(struct club));
    printf("Enter name of Member:");
    scanf(" %s",new->name);
    printf("Enter PRN of Member:");
    scanf("%d",&new->prn);
    new->next=NULL;
    new->prv=NULL; 
    temp=head->next;
    head->next=new; 
    new->prv=head;
    new->next=temp;
    temp->prv=new;
} 

void display(struct club *head){
    struct club *temp=head;
    while(temp!=NULL){
        printf("\n Name:%s\t PRN:%d\t",temp->name,temp->prn); 
        temp=temp->next;}
}

struct club* deletep(struct club *head){
    struct club *temp;
    temp=head;
    head=head->next; 
    head->prv=NULL;
    free(temp); 
    return head;
} 

void deletes(struct club *head){ 
    struct club *temp,*p;
    while(temp->next!=NULL){
        p=temp;
        temp=temp->next;
    } 
    p->next=NULL;
    free(temp);
}

void deletem(struct club *head){
    struct club *temp;
    temp=head->next;
    head->next=temp->next;
    temp->next->prv=head;
    free(temp);
}
    
void count(struct club *head){
    int i=0;
    struct club *temp;
    temp=head;
    while(temp!=NULL){
        i++;
        temp=temp->next;}
        printf("%d",i);
}
    
void reverse(struct club *temp){
    if(temp!=NULL){
        printf("\n %s %d",temp->name,temp->prn);
        temp=temp->prv;
        reverse(temp);
    }
}


