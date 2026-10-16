# 7-5 数制转换
# 利用栈实现数制转换（将一个十进制数转换成d进制数，d为整数），例如 1024 2，输出为1024(10)=10000000000(2)。
# 输入格式: 117 6
# 输出格式: 117(10)=313(6）

#include <bits/stdc++.h>
using namespace std;
#define Max 100
typedef int SElemType;
typedef struct{
    SElemType *base;
    SElemType *top;
    int stacksize;
}SqStack;

void init(SqStack &S){
    S.stacksize=Max;
    S.base=new SElemType[S.stacksize];
    S.top=S.base;
}

void push(SqStack &S,SElemType e){
    *S.top++=e;
}

bool empty(SqStack S){
    return S.top==S.base;
}

bool pop(SqStack &S,SElemType &e){
    if(empty(S)) return false;
    e=*--S.top;
    return true;
}

void conversion(int n,int d){
    SqStack S;
    init(S);
    while(n){
        push(S,n%d);
        n=n/d;
    }
    SElemType e;
    while(!empty(S)){
        pop(S,e);
        cout <<e;
    }
}

int main(){
    int n,d;
    cin >>n>>d;
    cout <<n <<"(10)=";
    conversion(n,d);
    cout <<"("<<d<<")";
    return 0;
}

--------------------------------------------------------------------------------------------

# 7-6 括号匹配
# 利用栈的运算，实现一个表达式（以#结束）中括号的匹配算法：括号只含有｛｝，（），[ ]。匹配输出1，否则输出0。
# 输入格式: 1+(2+3)*[3*6]/{4+5}+{[8*7]}#
# 输出格式: 1

#include<bits/stdc++.h>
using namespace std;
typedef char SElemType;
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

void push(Sqstack &S,SElemType e){
    *S.top++=e;
}

bool empty(Sqstack S){
    return S.top==S.base;
}

void pop(Sqstack &S,SElemType &e){
    e=*--S.top;
}

int match(){
    Sqstack S;
    init(S);
    char ch;
    while(cin >>ch&&ch!='#'){
        if(ch=='('||ch=='['||ch=='{'){
            push(S,ch);
        }
        else if(ch==')'){
            if(empty(S)) return 0;
            char a;
            pop(S,a);
            if(a!='(') return 0;
        }
        else if(ch==']'){
            if(empty(S)) return 0;
            char a;
            pop(S,a);
            if(a!='[') return 0;
        }
        else if(ch=='}'){
            if(empty(S)) return 0;
            char a;
            pop(S,a);
            if(a!='{') return 0;
        }
    }
        if(empty(S)) return 1;
        else return 0;
}
int main(){
    int ans=match();
    cout <<ans<<endl;
}

---------------------------------------------------------------------------------------------------------

# 7-7 利用栈进行表达式运算
# 试编写算法，利用栈实现表达式求值算法。要求输入数字为个位数，表达式只包含+、-、*、/、()，表达式以#结束。
# 输入格式: 6-(9-3)/2-(7-1)/3#
# 输出格式: 1

#include<bits/stdc++.h>
using namespace std;
typedef int SElemTypeN;
typedef char SElemTypeC;
#define Max 100
typedef struct{
    SElemTypeN *base;
    SElemTypeN *top;
    int stacksize;
}SqstackN;
typedef struct{
    SElemTypeC *base;
    SElemTypeC *top;
    int stacksize;
}SqstackC;

void initC(SqstackC &S){
    S.stacksize=Max;
    S.base=new SElemTypeC[S.stacksize];
    S.top=S.base;
}
void pushC(SqstackC &S,SElemTypeC e){
    *S.top++=e;
}
bool emptyC(SqstackC S){
    return S.top==S.base;
}
void popC(SqstackC &S,SElemTypeC &e){
    e=*--S.top;
}

void initN(SqstackN &S){
    S.stacksize=Max;
    S.base=new SElemTypeN[S.stacksize];
    S.top=S.base;
}
void pushN(SqstackN &S,SElemTypeN e){
    *S.top++=e;
}
bool emptyN(SqstackN S){
    return S.top==S.base;
}
void popN(SqstackN &S,SElemTypeN &e){
    e=*--S.top;
}

void headC(SqstackC S,SElemTypeC &e){
    e=*(S.top-1);
}

int youxian(char a){
    if(a=='*'||a=='/') return 2;
    if(a=='+'||a=='-') return 1;
    if(a=='(') return 0;
    return -1;
}

int jisuan(int a,char b,int c){
    if(b=='+') return a+c;
    if(b=='-') return a-c;
    if(b=='*') return a*c;
    if(b=='/') return a/c;
    return 0;
}

int zongjisuan(){
    SqstackC optr;
    SqstackN opnd;
    initN(opnd);
    initC(optr);
    char ch;
    while(cin >>ch){
        if(ch=='#') break;
        if(ch>='0'&&ch<='9') pushN(opnd,ch-'0');
        else if(ch=='(') pushC(optr,ch);
        else if(ch==')'){
            char op;
            headC(optr,op);
            while(op!='('){
                int b,a;
                popN(opnd,b);
                popN(opnd,a);
                popC(optr,op);
                int ans=jisuan(a,op,b);
                pushN(opnd,ans);
                headC(optr,op);
            }
            popC(optr,op);
        }
        else if(ch=='+'||ch=='-'||ch=='*'||ch=='/'){
            char ct;
            while(!emptyC(optr)){
                headC(optr,ct);
                if(youxian(ct)>=youxian(ch)){
                    int b,a;
                    popN(opnd,b);
                    popN(opnd,a);
                    popC(optr,ct);
                    int ans=jisuan(a,ct,b);
                    pushN(opnd,ans);
                    }
                else break;
            }
        pushC(optr,ch);
        }
    }
        while(!emptyC(optr)){
            char op;
            headC(optr,op);
            int b,a;
            popN(opnd,b);
            popN(opnd,a);
            popC(optr,op);
            int ans=jisuan(a,op,b);
            pushN(opnd,ans);
        }
        int res;
        popN(opnd,res);
        return res;
    }

int main(){
    int ans=zongjisuan();
    cout <<ans<<endl;
    return 0;
}

--------------------------------------------------------------------------------------------

# 7-8 队列应用-杨辉三角
# 利用队列打印杨辉三角：编写程序，根据输入的行数，屏幕显示杨辉三角。输入整形数据，输出数字图形。

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

bool empty(SqQueue Q){
    return Q.front==Q.rear;
}

void en(SqQueue &Q,QElemType e){
    Q.base[Q.rear]=e;
    Q.rear=(Q.rear+1)%Max;
}

void de(SqQueue &Q,QElemType &e){
    e=Q.base[Q.front];
    Q.front=(Q.front+1)%Max;
}

void head(SqQueue Q,QElemType &e){
    e=Q.base[Q.front];
}

void yanghui(int n){
    SqQueue Q;
    init(Q);
    en(Q,1);
    for(int i=1;i<=n;i++){
        int pre=0;
        for(int k=1;k<=n-i;k++){
            cout <<"  ";
        }
        for(int j=1;j<=i;j++){
            int cur;
            de(Q,cur);
            cout <<cur;
            if(j<i) cout<<"  ";
            int next=pre+cur;
            en(Q,next);
            pre=cur;
        }
        en(Q,1);
        cout <<endl;
    }
}

int main(){
    int n;
    cin >>n;
    yanghui(n);
    return 0;
}

------------------------------------------------------------------------------------------------------------------

$\color{#8A2BE2}{\text{不把它当作和他人的竞争，而是作为和我自己的对决去努力地奔跑。————WONWOO}}$
$\color{#8A2BE2}{\text{2026.10.16}}$
