# 6-12 带头结点的链队列的基本操作
# 实现链队列的入队列及出队列操作。

Status QueueInsert(LinkQueue *Q,ElemType e){
    LinkList p=(LinkList)malloc(sizeof(LNode));
    p->data=e;
    p->next=NULL;
    Q->rear->next=p;
    Q->rear=p;
    return OK;
}

Status QueueDelete(LinkQueue *Q,ElemType *e){
    if(Q->front==Q->rear) return ERROR;
    LinkList p=Q->front->next;
    *e=p->data;
    Q->front->next=p->next;
    if(Q->rear==p){
        Q->rear=Q->front;
    }
    free(p);
    return OK;
}

-------------------------------------------------------------------

# 6-13 数据结构考题 - 链队列-出队
# 程序用链队列作存储结构，实现队列（元素为整型）的基本运算。本题只需完成 DeQueue函数，然后提交系统。

bool DeQueue(LinkQueue &Q, ElemType &e){
    if(Q.front==Q.rear){
        cout <<"NULL";
        return false;
    }
    QNode* p=Q.front->next;
    e=p->data;
    Q.front->next=p->next;
    if(Q.rear==p){
        Q.rear=Q.front;
    }
    delete p;
    return true;
}
