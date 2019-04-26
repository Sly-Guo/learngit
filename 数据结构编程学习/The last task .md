# The last task 
* 递归
* 回溯
* 分治
* 动态规划

## 	递归
#### Leetcode 70. 爬楼梯
* top-down(python)

```
class Solution(object):
    def climbStairs(self, n):
        if n == 1: return 1
        res = [-1 for i in range(n)]
        res[0], res[1] = 1, 2
        return self.dp(n-1, res)
        
    def dp(self, n, res):
        if res[n] == -1:
            res[n] = self.dp(n - 1, res) + self.dp(n - 2, res)
        return res[n]

```

## 回溯
#### 回溯算法解八皇后问题

```
	#include<cstring> 
#include<iostream>
using namespace std;  
int vis[3][15],tot;  
 
void search(int cur)  
{  
    int i,j;  
    if(cur==8) tot++;
    else  
    {  
    	for(i=0;i<8;i++)  
        {  
            if(!vis[0][i]&&!vis[1][cur-i+8]&&!vis[2][cur+i])  
            {  
                vis[0][i]=1;  
                vis[1][cur-i+8]=1;  
                vis[2][cur+i]=1;    
                search(cur+1);  
                //改回辅助的全局变量 
                vis[0][i]=0;       
                vis[1][cur-i+8]=0;  
                vis[2][cur+i]=0;  
            }  
        }  
    }  
}  
 
int main()  
{  
    search(0);   
    cout<<tot<<endl;
}

```

#### 背包问题

```

#include<iostream>
using namespace std;
int n,c,bestp;//物品个数,背包容量,最大价值
int p[10000],w[10000],x[10000],bestx[10000];//物品的价值,物品的重量,物品的选中情况
 
void backtrack(int i,int cp,int cw)
{
    if(i>n)
    {
        if(cp>bestp)
        {
            bestp=cp;
            for(i=1;i<=n;i++) bestx[i]=x[i];
        }
    }
    else
	{
        for(int j=0;j<=1;j++)  
        {
            x[i]=j;
            if(cw+x[i]*w[i]<=c)  
            {
                cw+=w[i]*x[i];
                cp+=p[i]*x[i];
                backtrack(i+1,cp,cw);
                cw-=w[i]*x[i];
                cp-=p[i]*x[i];
            }
        }
	}
}
 
int main()
{
    bestp=0; 
    cin>>c>>n;
    for(int i=1;i<=n;i++) cin>>w[i];
    for(int i=1;i<=n;i++) cin>>p[i];
    backtrack(1,0,0);
    cout<<bestp<<endl;
}

```

## 分治

```
#include <iostream>
#include <math.h>
using namespace std;
const int NUM=100000;
const char* filepath="E:\\data.txt";
int Mid[NUM]={0};
long long answer=0;
void File_to_Array(int* array)
{
	FILE * f;
	int idx=0;
	if((f=fopen(filepath,"r"))==NULL)
	{
		cout<<"文件打开失败！"<<endl;
	}
	else{
		while(!feof(f))
		{
			fscanf(f,"%d",&array[idx]);
			idx++;
		}
		fclose(f);
	}
}
void Merge(int* s,int low,int mid,int up)
{
        int a=low,b=mid+1;
        for(int i=low;i<=up;i++)
                Mid[i]=s[i];
        for(int i=low;i<=up;i++)
        {
                if(a>mid)
                        s[i]=Mid[b++];
                else if(b>up)
                        s[i]=Mid[a++];
                else if(Mid[a]<=Mid[b])
                        s[i]=Mid[a++];
                else {
                	s[i]=Mid[b++];
                	answer+=mid-a+1;
                }
        }
}
void Sort(int* s,int low,int up)//归并排序
{
       if(up<=low)
                return;
       else
       {
               int mid=(low+up)/2;
               Sort(s,low,mid);
               Sort(s,mid+1,up);
               Merge(s,low,mid,up);
       }
}
 
int main()
{
		int array[NUM];
		File_to_Array(array);
        Sort(array,0,NUM-1);
//        printf("\n");
//        for(int i=0;i<NUM;i++)
//        {
//                printf("%d ",array[i]);
//        }
        cout<<answer;
    return 0;
}


```

## 动态规划
#### 实现莱文斯坦最短编辑距离
```
# Python 

def normal_leven(str1, str2):
  len_str1 = len(str1) + 1
  len_str2 = len(str2) + 1
  #create matrix
  matrix = [0 for n in range(len_str1 * len_str2)]
  #init x axis
  for i in range(len_str1):
    matrix[i] = i
  #init y axis
  for j in range(0, len(matrix), len_str1):
    if j % len_str1 == 0:
      matrix[j] = j // len_str1
 
  for i in range(1, len_str1):
    for j in range(1, len_str2):
      if str1[i-1] == str2[j-1]:
        cost = 0
      else:
        cost = 1
      matrix[j*len_str1+i] = min(matrix[(j-1)*len_str1+i]+1,
                    matrix[j*len_str1+(i-1)]+1,
                    matrix[(j-1)*len_str1+(i-1)] + cost)
 
  return matrix[-1]
```
#### 两个字符串的最长公共连续子序列的长度

>假设两个字符串str1和str2，长度分别为m和n，则构建一个m*n的矩阵matrix
>
> matrix[i][j]==1表示字符串str1中第i个字符与str2中第j个字符相等，为0则不相等
> 
> 统计矩阵matrix中每条斜线上1的连续最大个数就是str1和str2中公共连续子串的最大长度


```
#include <bits/stdc++.h>
#define ll long long
#define inf 0x3f3f3f3f
#define mem(a,b) memset(a,b,sizeof(a))
using namespace std;
int m[100][100];
int main(){//freopen("1.txt","r",stdin);
    int i,j,k1,k2,n,ans=0,max;
    string s1,s2;
    getline(cin,s1);
    getline(cin,s2);
    k1=s1.size();
    k2=s2.size();
    mem(m,0);
    for(i=0;i<k1;i++)
        for(j=0;j<k2;j++)
            if(s1[i]==s2[j])m[i][j]=1;
    for(i=0;i<k1;i++){
        max=0;
        for(j=0;j<k2;j++){
            if(m[i+j][j]==1)max++;
            else max=0;
            if(max>ans)ans=max;
        }
    }//统计从左边第一列开始的斜向右下斜线的最大值
    for(i=0;i<k2;i++){
        max=0;
        for(j=0;j<k1;j++){
            if(m[j][i+j]==1)max++;
            else max=0;
            if(max>ans)ans=max;
        }
    }//统计从顶部第一行开始的斜向右下斜线的最大值
    printf("%d\n",ans);
    /*
    for(i=0;i<k1;i++){
        for(j=0;j<k2;j++)
            printf("%d ",m[i][j]);
        printf("\n");
    }
    */
    return 0;
}
```
