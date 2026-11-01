# 一元多项式运算
# 采用单向链表实现一元多项式的存储，并实现两个多项式相加，输出结果。
# 输入格式:4（请输入第一个一元多项式的项数） 2,2 3,3 5,5 7,7（请输入第一个一元多项式的系数和指数）;5（请输入第二个一元多项式的项数） -2,2 2,3 4,4 5,7 9,9（请输入第二个一元多项式的系数和指数）
# 输出格式:5*x^3 4*x^4 5*x^5 12*x^7 9*x^9（每个多项式用空格隔开）

#include <bits/stdc++.h>
using namespace std;
typedef struct LNode{
    int a;
    int b;
    struct LNode* next;
}LNode,*LinkList;

LinkList create(){
    int n;
    cin >>n;
    LinkList L=new LNode;
    L->next=NULL;
    LinkList r=L;
    for(int i=0;i<n;i++){
        LinkList p=new LNode;
        p->next=NULL;
        char s;
        cin >>p->a >>s >>p->b;
        r->next=p;
        r=p;
    }
    return L;
}

LinkList add(LinkList L1,LinkList L2){
    LinkList p1=L1->next;
    LinkList p2=L2->next;
    LinkList L=new LNode;
    L->next=NULL;
    LinkList p=L;
    while(p1&&p2){
        if(p1->b < p2->b){
            p->next=p1;
            p=p1;
            p1=p1->next;
        }
        else if(p1->b > p2->b){
            p->next=p2;
            p=p2;
            p2=p2->next;
        }
        else{
            if(p1->a + p2->a != 0){
                LinkList q=new LNode;
                q->next=NULL;
                q->a=p1->a+p2->a;
                q->b=p1->b;
                p->next=q;
                p=q;
                p1=p1->next;
                p2=p2->next;
            }
            else{
                p1=p1->next;
                p2=p2->next;
            }
        }
    }
    if(p1) p->next=p1;
    if(p2) p->next=p2;
    return L;
}

int main(){
    LinkList L1=create();
    LinkList L2=create();
    LinkList L=add(L1,L2);
    LinkList p=L->next;
    while(p){
        cout <<p->a <<"*x^" <<p->b;
        if(p->next) cout <<" ";
        p=p->next;
    }
    return 0;
}
