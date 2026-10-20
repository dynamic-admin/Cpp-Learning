# 6-8 在单链表指定位置插入元素
# 在一个带头结点的单链表的指定位置location，增加一个新的元素  x ，若给定的位置不合法则提示插入失败。
# 例如：单链表  9 5 1 2 3，
# 指定位置3插入元素4，则 新的单链表为  9 5 4 1  2   3
# 指定位置7插入元素8，则 提示插入失败。

int insertLink(LinkList L, int location, ElemType x){
    if(location<=0) return 0;
    LinkList p=L;
    for(int i=1;i<location;i++){
        p=p->next;
        if(p==NULL) return 0;
    }
    LinkList q=(LinkList)malloc(sizeof(LNode));
    q->data=x;
    q->next=p->next;
    p->next=q;
    return 1;
}
