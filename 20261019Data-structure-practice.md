# 错排
# 在n个字母的全排列中，使得每个字母都不在原来位置的排列数是多少？请使用错位排列的递推公式来计算本题。
# Input:输入数据有多组，每组有1个正整数n(1<=n<=10),代表字母的个数。
# Output:在一行内输出这n个字母都不在原来位置的方法数。

#include <bits/stdc++.h>
using namespace std;
int a[10000];
int cuopai(int n){
  a[1]=0;
  a[2]=1;
  for(int i=3;i<=n;i++){
    a[i]=(i-1)*(a[i-1]+a[i-2]);
  }
  return a[n];
}
int main(){
  int n;
  while(cin >>n){
    cout <<cuopai(n)<<endl;
  }
  return 0;
}

---------------------------------------------------------------------------

# 欧拉函数值
# 对于一个正整数n，求出它的欧拉函数值，其中1<n<=100000000
# Input:输入数据有多组，每组数据一行，有1个正整数为n。
# Output:输出n的欧拉函数的值

#include <bits/stdc++.h>
using namespace std;
typedef long long LL;
LL oula(LL n){
	LL ans=n;
  for(LL i=2;i*i<=n;i++){
    if(n%i==0){
      ans=ans/i*(i-1);
      while(n%i==0) n=n/i;
      }
  }
    if(n>1) ans=ans/n*(n-1);
  return ans;
}
int main(){
  LL n;
  while(cin >>n){
    cout <<oula(n)<<endl;
  }
  return 0;
}

-------------------------------------------------------------------------

# 考新郎
# 国庆期间,省城HZ刚刚举行了一场盛大的集体婚礼,为了使婚礼进行的丰富一些,司仪临时想出了有一个有意思的节目,叫做"考新郎",具体的操作是这样的:首先,给每位新娘打扮得几乎一模一样,并盖上大大的红盖头随机坐成一排;然后,让各位新郎寻找自己的新娘.每人只准找一个,并且不允许多人找一个.最后,揭开盖头,如果找错了对象就要当众跪搓衣板...看来做新郎也不是容易的事情...假设一共有N对新婚夫妇,其中有M个新郎找错了新娘,求发生这种情况一共有多少种可能.
# Input:输入数据的第一行是一个整数C,表示测试实例的个数，然后是C行数据，每行包含两个整数N和M(1<M<=N<=40)。
# Output:对于每个测试实例，请输出一共有多少种发生这种情况的可能，每个实例的输出占一行。

#include <bits/stdc++.h>
using namespace std;
typedef long long LL;
LL a[42][42]={0};
LL b[42];
void yanghui(){
  for(int i=1;i<=41;i++){
    for(int j=1;j<=i;j++){
      if(j==1||i==j) a[i][j]=1;
      else a[i][j]=a[i-1][j]+a[i-1][j-1];
    }
  }
}
LL cuopai(int n){
  b[1]=0;
  b[2]=1;
  for(int i=3;i<=n;i++){
    b[i]=(i-1)*(b[i-1]+b[i-2]);
  }
  return b[n];
}
int main(){
  int n;
  cin >>n;
  int M,N;
  yanghui();
  for(int i=0;i<n;i++){
    cin >>N>>M;
    cout <<a[N+1][M+1]*cuopai(M)<<endl;
  }
  return 0;
}
