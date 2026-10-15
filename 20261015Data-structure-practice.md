# 7-1 顺序栈的操作
# 试编写算法，采用顺序存储方式实现栈的初始化、入栈、出栈操作。要求输入整形数据，输入0表示结束（0不存储在栈中）。
# 输入格式: 1 2 3 4 5 6 7 8 9 0
# 输出格式: 9 8 7 6 5 4 3 2 1

#include<bits/stdc++.h>
using namespace std;
typedef int SElemType;
#define Max 100
typedef struct{
    SElemType *base;
    SElemType *top;
    int stacksize;
}Sqstack;

void init(Sqstack &S){
    S.stacksize=Max;
    S.base=new SElemType[S.stacksize];
    S.top=S.base;
}

void push(Sqstack &S){
    int x;
    while(cin >>x&&x!=0){
        *S.top++=x;
    }
}

void pop(Sqstack &S){
    if(S.top==S.base) return;
    int x=*--S.top;
    cout <<x<<" ";
    while(S.top!=S.base){
        x=*--S.top;
        cout <<" "<<x;
    }
}

int main(){
    Sqstack S;
    init(S);
    push(S);
    pop(S);
    delete[] S.base;
    return 0;
}

---------------------------------------------------------------------------------------------------------------

# 7-2 链栈的操作
# 试编写算法，采用链式存储实现栈的初始化、入栈、出栈操作。要求输入整形数据，输入0表示结束（0不存储在栈中）。
# 输入格式: 1 2 3 4 5 6 7 8 9 0
# 输出格式: 9 8 7 6 5 4 3 2 1

#include <bits/stdc++.h>
using namespace std;
#define Max 100
typedef int SElemType;
typedef struct StackNode{
    SElemType data;
    struct StackNode *next;
}StackNode,*LinkStack;

void init(LinkStack &S){
    S=NULL;
}

void push(LinkStack &S){
    int x;
    while(cin >>x&&x!=0){
        LinkStack p=new StackNode;
        p->data=x;
        p->next=S;
        S=p;
    }
}

void pop(LinkStack &S){
    int x=S->data;
    cout <<x;
    while(S->next){
        LinkStack p=S->next;
        cout <<" "<<p->data;
        S=S->next;
    }
}

int main(){
    LinkStack S;
    init(S);
    push(S);
    pop(S);
    return 0;
}

--------------------------------------------------------------------------------------------------------------

# 7-3 链队列的操作
# 采用链式存储实现队列的初始化、入队、出队操作。要求输入整形数据，输入0表示结束（0不存储在栈中）。
# 输入格式: 1 2 3 4 5 6 7 8 9 0
# 输出格式: 1 2 3 4 5 6 7 8 9

#include <bits/stdc++.h>
using namespace std;
typedef int QElemType;
typedef struct QNode{
    QElemType data;
    struct QNode *next;
}QNode,*QueuePtr;
typedef struct{
    QueuePtr front;
    QueuePtr rear;
}LinkQueue;

void init(LinkQueue &Q){
    Q.front=Q.rear=new QNode;
    Q.front->next=NULL;
}

void en(LinkQueue &Q){
    int x;
    while(cin >>x&&x!=0){
        QueuePtr p=new QNode;
        p->data=x;
        p->next=NULL;
        Q.rear->next=p;
        Q.rear=p;
    }
}

void de(LinkQueue &Q){
    if(Q.front==Q.rear) return;
    QueuePtr p=Q.front->next;
    cout <<p->data;
    Q.front->next=p->next;
    if(Q.rear==p){
        Q.rear=Q.front;
    }
    delete p;
    while(Q.front!=Q.rear){
        p=Q.front->next;
        cout <<" "<<p->data;
        Q.front->next=p->next;
        if(Q.rear==p){
            Q.rear=Q.front;
        }
        delete p;
    }
}

int main(){
    LinkQueue Q;
    init(Q);
    en(Q);
    de(Q);
    return 0;
}

-----------------------------------------------------------------------------------------------------------

# 7-4 循环队列的操作
# 采用顺序存储实现循环队列的初始化、入队、出队操作。要求输入整形数据，输入0表示结束（0不存储在栈中）。
# 输入格式: 1 2 3 4 5 6 7 8 9 0
# 输出格式: 1 2 3 4 5 6 7 8 9

#include <bits/stdc++.h>
using namespace std;
#define Max 100
typedef int QElemType;
typedef struct{
    QElemType *base;
    int front;
    int rear;
}SqQueue;

void init(SqQueue &Q){
    Q.base=new QElemType[Max];
    Q.front=Q.rear=0;
}

void en(SqQueue &Q){
    int x;
    while(cin >>x&&x!=0){
        Q.base[Q.rear]=x;
        Q.rear=(Q.rear+1)%Max;
    }
}

void de(SqQueue &Q){
    int x=Q.base[Q.front];
    cout <<x;
    Q.front=(Q.front+1)%Max;
    while(Q.front&&Q.base[Q.front]!=0){
        x=Q.base[Q.front];
        cout <<" "<<x;
        Q.front=(Q.front+1)%Max;
    }
}

int main(){
    SqQueue Q;
    init(Q);
    en(Q);
    de(Q);
    return 0;
}

-----------------------------------------------------------------------------------------

$\color{#7ccdbb}{\text{努力地去对待，去做现下生活所给予你的一切事物，便可以找到适合自己的道路。————JEONGHAN}}$
$\color{#7ccdbb}{\text{2026.10.15}}$
