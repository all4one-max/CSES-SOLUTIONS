### [Grid Paths](https://cses.fi/problemset/task/1638)

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
    n=II()
    li=[input() for i in range(n)]
    if n==1:
        if li[0]=="*":
            P(0)
            return
        else:
            P(1)
            return
    dp=[[0 for j in range(n)] for i in range(n)]
    dp[0][0]=1
    for i in range(n):
        for j in range(n):
            if li[i][j]!="*":
                if i!=0 or j!=0:
                    if (i-1)>=0 and li[i-1][j]!='*':
                        dp[i][j]+=dp[i-1][j]
                    if (j-1)>=0 and li[i][j-1]!="*":
                        dp[i][j]+=dp[i][j-1]
                    dp[i][j]%=mod

    print(dp[n-1][n-1]%mod)
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
