# 7-1 线性表逆置
# 设有一个线性表存放在一个一维数组中的前n个数组元素位置。请编写一个顺序表的程序，将这个线性表原地逆置。分别输出逆置前的顺序表和逆置后的顺序表。（顺序表的元素类型为整型）
# 输入格式:先输入一个整数n，表示顺序表的长度，之后输入n个整数
# 输出格式:两行（每个数之间用一个空格分隔）第一行为原来的顺序表，第二行为逆置后的顺序表

----------------------------------------------------------------------------------------------------
#include<bits/stdc++.h>
using namespace std;
int a[1000];
void sub(int n,int a[]){
    int left=0,right=n-1;
    int t;
    while(left<right){
        t=a[left];
        a[left]=a[right];
        a[right]=t;
        left++; //第一次提交的时候忘了这两行
        right--; //导致没有逆置的顺序表输出
    }
}
int main(){
    int n;
    cin >>n;
    for(int i=0;i<n;i++){
        cin >>a[i];
        cout <<a[i];
        if(i!=n-1){
            cout <<" ";
        }
    }
    cout <<endl;
    sub(n,a);
    for(int i=0;i<n;i++){
        cout <<a[i];
        if(i!=n-1){
            cout <<" ";
        }
    }
    return 0;
}

$\color{#f0a8b8}{\text{相信时间会给出答案 ——Joshua}}$
$\color{#f0a8b8}{\text{2026.10.13}}$
