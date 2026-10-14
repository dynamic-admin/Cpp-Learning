# 7-2 单链表简单操作
# 键盘输入一组元素，以0做结束输入的标记，建立一个带头结点的单向链表（无序，且值域为整型），遍历单向链表，显示相应元素。
# 输入格式: 1 2 3 4 5 6 7 8 0
# 输出格式: 1 2 3 4 5 6 7 8 

#include<bits/stdc++.h>
using namespace std;
typedef int ElemType;
typedef struct LNode{
    ElemType data;
    struct LNode *next;
}LNode,*LinkList;

void build(LinkList &L){ //尾插法
    L=new LNode;
    LinkList r=L;
    L->next=NULL;
    int x;
    while(cin >>x&&x!=0){
        LinkList p=new LNode;
        p->data=x;
        p->next=NULL;
        r->next=p;
        r=p;
    }
}

void printList(LinkList &L){
    LinkList q=L->next;
    while(q){
        cout <<q->data;
        if(q->next){
            cout <<" ";
        }
        q=q->next;
    }
}

int main(){
    LinkList L;
    build(L);
    printList(L);
    return 0;
}

------------------------------------------------------------------------------------------------

# 7-3 单链表逆置
# 试编写算法，把单向链表（值域为整型）中元素逆置（不允许申请新的结点空间）。
# 输入格式: 输入整形数值，以0作为结束输入的标记，元素不一样有序
# 输出格式: 逆置后的单链表，元素之间用一个空格分隔

#include<bits/stdc++.h>
using namespace std;
typedef int ElemType;
typedef struct LNode{
    ElemType data;
    struct LNode *next;
}LNode,*LinkList;

void build(LinkList &L){ //头插法
   L=new LNode;
   L->next=NULL;
   int x;
   while(cin >>x&&x!=0){
       LinkList p=new LNode;
       p->data=x;
       p->next=L->next;
       L->next=p;
   }
}

void printList(LinkList &L){
    LinkList q=L->next;
    while(q){
        cout <<q->data;
        if(q->next){
            cout <<" ";
        }
        q=q->next;
    }
}

int main(){
    LinkList L;
    build(L);
    printList(L);
    return 0;
}

