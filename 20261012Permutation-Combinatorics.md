# 非降路径  在平面直角坐标系内，有(a,b)和(c,d)两点，且a,b,c,d都大于0，而且(c,d)点位于(a,b)点的右上方！从(a,b)出发走到(c,d)点，只能向上走和向右走，请问共有多少种走法（非降路径数）？输入：输入a,b,c,d(0<=a,b,c,d<=12)。输出：输出非降路径数！

#include<bits/stdc++.h>
using namespace std;
int main(){
  int a,b,c,d;
  cin >>a>>b>>c>>d;
  int m=c-a,n=d-b;
  int ans1=m+n,ans2=m,ans3=n;
  for(int i=m+n-1;i>0;i--) ans1*=i;
  for(int j=m-1;j>0;j--) ans2*=j;
  for(int k=n-1;k>0;k--) ans3*=k;
  cout <<ans1/ans2/ans3;
  return 0;
}

----------------------------------------------------------

# 特殊的非降路径  设a,b,c,d,m,n是非负整数，其中 a<=c<=m,b<=d<=n;请你计算从(a,b)点经过(c,d)点到(m,n)点的非降路径数？输入：在一行内输入a,b,c,d,m,b,所有的数值范围为【0-14】，本题为单组数据。输出：在一行内输出非降路径数。

#include<bits/stdc++.h>
using namespace std;
int main(){
  int a,b,c,d,m,n;
  cin >>a>>b>>c>>d>>m>>n;
  int x1=c-a,y1=d-b;
  int q1=x1+y1,q2=x1,q3=y1;
  int x2=m-c,y2=n-d;
  int q4=x2+y2,q5=x2,q6=y2;
  for(int i=x1+y1-1;i>0;i--) q1*=i;
  for(int j=x1-1;j>0;j--) q2*=j;
  for(int k=y1-1;k>0;k--) q3*=k;
  int ans1=q1/q2/q3;
  for(int i=x2+y2-1;i>0;i--) q4*=i;
  for(int j=x2-1;j>0;j--) q5*=j;
  for(int k=y2-1;k>0;k--) q6*=k;
  int ans2=q4/q5/q6;
  cout <<ans1*ans2;
  return 0;
}

------------------------------------------------------------

# 简单组合：  计算C(n,m)的值，C(n,m)代表从n个元素中选取m个元素的方法数，其中有1<=m<=n<=65。输入：输入数据有多组，每组数据一行，有2个整数分别为n和m。输出：输出从总共n个元素中选出m个元素共有多少种方法?

#include<bits/stdc++.h>
using namespace std;
typedef long long LL;
LL a[67][67]={0};
void yanghui(){
  for(int i=1;i<=66;i++){ //为什么是66？因为1<=m<=n<=65，我们把第零行（i=0）和第零列（j=0）都闲置，从它们的下一行和下一列开始，所以最大下标是65+1=66
    for(int j=1;j<=i;j++){
      if(j==1||i==j) a[i][j]=1;
      else a[i][j]=a[i-1][j]+a[i-1][j-1];
    }
  }
}
int main(){
  int n,m;
  yanghui();
  while(cin >>n>>m) cout <<a[n+1][m+1]<<endl;
  return 0;
}

---------------------------------------------------------------

# 小兔的棋盘（卡特兰数*2）  小兔的叔叔从外面旅游回来给她带来了一个礼物，小兔高兴地跑回自己的房间，拆开一看是一个棋盘，小兔有所失望。不过没过几天发现了棋盘的好玩之处。从起点(0，0)走到终点(n,n)的最短路径数是C(2n,n),现在小兔又想如果不穿越对角线(但可接触对角线上的格点)，这样的路径数有多少?小兔想了很长时间都没想出来，现在想请你帮助小兔解决这个问题，对于你来说应该不难吧 ！输入：多组输入，每次输入一个数n(1<=n<=30)，当n等于－1时结束输入。输出：对于每个输入数据输出路径数，具体格式看Sample。

#include<bits/stdc++.h>
using namespace std;
typedef long long LL;
LL a[63][63]={0};
void yanghui(){
  for(int i=1;i<=62;i++){ //为什么是62？因为1<=n<=30，而我们要用到2*n,最大是2*30=60(60个格),我们把第零行（i=0）和第零列（j=0）都闲置，从它们的下一行和下一列开始，所以最大下标是61+1=62
    for(int j=1;j<=i;j++){
      if(j==1||i==j) a[i][j]=1;
      else a[i][j]=a[i-1][j]+a[i-1][j-1];
    }
  }
}
int main(){
  int n;
  yanghui();
  int count=1;
  while(cin >>n&&n!=-1){
    LL ans=2*a[2*n+1][n+1]/(n+1);
    cout <<count<<" "<<n<<" "<<ans<<endl;
    count++;
  }
  return 0;
}
