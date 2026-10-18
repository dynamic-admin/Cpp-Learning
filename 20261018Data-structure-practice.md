# 6-2 jmu-ds- 顺序表删除重复元素
# 设计一个算法，从顺序表中删除重复的元素，并使剩余元素间的相对次序保存不变。
# 输入格式: 第一行输入顺序表长度。 第二行输入顺序表数据元素。中间空格隔开。
# 输出格式：数据之间空格隔开，最后一项尾部不带空格。
# 输出删除重复元素后的顺序表。
# 你需要实现的函数有下面三个：

void CreateSqList(List &L,int a[],int n){
    L=NULL;
    if(n<=0) return;
    L=new SqList;
    L->length=0;
    for(int i=0;i<n;i++){
        L->data[i]=a[i];
        L->length++;
    }
}
void DispSqList(List L){
    if((L==NULL)||L->length==0) return;
    cout <<L->data[0];
    for(int i=1;i<L->length;i++){
        cout <<" "<<L->data[i];
    }
}
void DelSameNode(List &L){
    if((L==NULL)||L->length==0) return;
    int i=0;
    while(i<L->length){
        int j=i+1;
        while(j<L->length){
            if(L->data[j]==L->data[i]){
                for(int k=j;k<L->length-1;k++){
                    L->data[k]=L->data[k+1];
                }
                L->length--;
            }
            else j++;
        }
        i++;
    }
}
