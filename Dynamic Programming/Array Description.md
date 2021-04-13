### [Array Description](https://cses.fi/problemset/task/1746)

```python
import time,math as mt,bisect,sys
from sys import stdin,stdout
from collections import deque
from fractions import Fraction
from collections import Counter
from collections import OrderedDict
pi=3.14159265358979323846264338327950
def II(): # to take integer input
    return int(stdin.readline())
def IO(): # to take string input
    return stdin.readline()
def IP(): # to take tuple as input
    return map(int,stdin.readline().split())
def L(): # to take list as input
    return list(map(int,stdin.readline().split()))
def P(x): # to print integer,list,string etc..
    return stdout.write(str(x)+"\n")
def PI(x,y): # to print tuple separatedly
    return stdout.write(str(x)+" "+str(y)+"\n")
def lcm(a,b): # to calculate lcm
    return (a*b)//gcd(a,b)
def gcd(a,b): # to calculate gcd
    if a==0:
        return b
    elif b==0:
        return a
    if a>b:
        return gcd(a%b,b)
    else:
        return gcd(a,b%a)

def bfs(adj,v): # a schema of bfs
    visited=[False]*(v+1)
    q=deque()
    while q:
        pass
def sieve():
    li=[True]*1000001
    li[0],li[1]=False,False
    for i in range(2,len(li),1):
        if li[i]==True:
            for j in range(i*i,len(li),i):
                li[j]=False
    prime=[]
    for i in range(1000001):
        if li[i]==True:
            prime.append(i)
    return prime
def setBit(n):
    count=0
    while n!=0:
        n=n&(n-1)
        count+=1
    return count
mx=10**7
spf=[mx]*(mx+1)
def SPF():
    spf[1]=1
    for i in range(2,mx+1):
        if spf[i]==mx:
            spf[i]=i
            for j in range(i*i,mx+1,i):
                if i<spf[j]:
                    spf[j]=i
    return
def readTree(n): # to read tree
    adj=[set() for i in range(n+1)]
    for i in range(n-1):
        u1,u2=IP()
        adj[u1].add(u2)
        adj[u2].add(u1)
    return adj
#####################################################################################
mod=10**9+7
def solve(i):
    n,m=IP()
    x=L()
    dp=[[0 for i in range(m+1)] for j in range(n)]
    if x[0]==0:
        for i in range(1,m+1):
            dp[0][i]=1
    else:
        dp[0][x[0]]=1
    for i in range(1,n):
        if x[i]!=0:
            for k in range(x[i]-1,x[i]+2):
                if k>=1 and k<=m:
                    dp[i][x[i]]=(dp[i][x[i]]+dp[i-1][k])%mod
        else:
            for v in range(1,m+1):
                for k in range(v-1,v+2):
                    if k>=1 and k<=m:
                        dp[i][v]=(dp[i][v]+dp[i-1][k])%mod
    ans=0
    for j in range(1,m+1):
        ans=(ans+dp[n-1][j])%mod
    print(ans)
    return


t=1
for i in range(t):
    solve(i)

    #######
   #
  #
 #######   #     #  # ####   # #     #
       #  # #   #  # #   #  # # #   #
      #  ####  #  # ####   ####  # #
######  #   # #### #    # #   #   #

```
