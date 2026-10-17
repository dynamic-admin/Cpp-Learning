# 6-1 jmu-ds-有序表插入数据
# 要求实现3个函数，在递增的顺序表中插入一个新整数，并保持该顺序表的有序性。

void CreateSqList(SqList &L,int n){
    L=NULL;
    if(n<=0) return;
    L=new List;
    L->length=0;
    for(int i=0;i<n;i++){
        cin >>L->data[i];
        L->length++;
    }
}
void InsertSq(SqList &L,int x){
    if((L==NULL) || L->length>=MaxSize) return;
    int i=0;
    for(i=0;i<L->length;i++){
        if(x<=L->data[i]) break;
        }
    for(int j=L->length-1;j>=i;j--){
        L->data[j+1]=L->data[j];
        }
    L->data[i]=x;
    L->length++;
}
void DispSqList(SqList L){
    if((L==NULL) || L->length==0){
        cout <<"error";
        return;
    }
    cout <<L->data[0];
    for(int i=1;i<L->length;i++){
        cout <<" "<<L->data[i];
    }
}

---------------------------------------------------------------------------------

# 6-3 xcu-sjjg-C-List-2 顺序表就地逆置
# 将顺序表的元素就地逆置。空间复杂度要求O(1)。

void reverse(SqList &L){
    for(int i=0;i<L.length/2;i++){
        int t=L.data[i];
        L.data[i]=L.data[L.length-1-i];
        L.data[L.length-1-i]=t;
    }
}

----------------------------------------------------------------------------------

# 6-6 单链表逆置
# 将单链表倒置，要求只利用原表的存储空间。

void Reverse(LinkedList list){
    LinkedList pre=NULL;
    LinkedList cur=list->next;
    while(cur){
        LinkedList nxt=cur->next;
        cur->next=pre;
        pre=cur;
        cur=nxt;
    }
    list->next=pre;
}
