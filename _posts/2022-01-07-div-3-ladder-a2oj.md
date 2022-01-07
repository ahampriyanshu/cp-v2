---
title: "Div 2 | Ladders | a2oj"
author: Priyashu Tiwari
date: 2021-09-1 20:00:00 +0530
categories: [a2oj]
tags: [a2oj, ladder, codeforces]
---

## 1 Queue at the School

```cpp
#include <bits/stdc++.h>
using namespace std;

typedef long long int ll;

void solve()
{
    ll n, t;
    string str;
    cin >> n >> t >> str;
    while(t--){
        int i = 0;
        while (i<n-1)
        {
            if( str[i] == 'B' and str[i+1] == 'G')
            {
                str[i] = 'G';
                str[++i] = 'B';
            }
            i++;
        }
        
    }
    cout << str << endl;
}

int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    solve();
}
```