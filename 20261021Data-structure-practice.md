# 6-9 寻找链表元素的前驱结点
# 本题要求实现一个函数，可查找单链表(无监督元)中某个元素的前驱结点。例如链表中的元素为1，6，3，2，4，查找3的前驱为6。如果表中无此元素或没有前驱则返回空指针。

ptr pre (ptr h,int x){
    if((h==NULL)||(h->next->data==x)) return NULL;
    ptr p=h->next;
    while((p->next!=NULL)&&(p->next->data!=x)){
        p=p->next;
    }
    if(p->next==NULL) return NULL;
    return p;
}

---------------------------------------------------------------------------------------------------------

# 6-10 顺序栈的基本运算
# 编写函数实现顺序栈的初始化、出栈、入栈运算。

Status iniStack(Sqstack &S){
    S.stacksize=stack_INIT_SIZE;
    S.base=new SElemType[S.stacksize];
    S.top=S.base;
    return OK;
}
Status push(Sqstack &S,SElemType x){
        *S.top++=x;
    return OK;
}
Status pop(Sqstack &S,SElemType &e){
    if(S.top==S.base) return FALSE;
    e=*--S.top;
    return OK;
}
