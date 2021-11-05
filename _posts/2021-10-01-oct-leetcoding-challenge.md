---
title: "Oct | Leetcoding Challenge"
author: Priyashu Tiwari
date: 2021-10-1 20:00:00 +0530
categories: [leetcode]
tags: [leetcode, oct]
---


## 4 Oct | Island Perimeter

* We will use bruforce to count all the sides of the island.

```cpp
class Solution {
public:
    int islandPerimeter(vector<vector<int>>& grid) {
        int n = grid.size();
        int ans = 0;
        for (int i=0; i<n; i++)
        {
            int m = grid[i].size();
            for(int j=0; j<m; j++){
            if(grid[i][j] == 1){
             
                if (i == 0) ans++;
                else if(grid[i-1][j] != 1) ans ++;
                
                if (i == n-1) ans++;
                else if(grid[i+1][j] != 1) ans ++;
                
                
                if (j == 0) ans++;
                else if(grid[i][j-1] != 1) ans ++;
                
                if (j == m-1) ans++;
                else if(grid[i][j+1] != 1) ans ++;
                  
            }
            }
        }
        return ans;
    }
};
```

## 5 Oct | Climbing Stairs

* We will use dynamic programming to calculate the nth term of the fibonacci seq.

```cpp
class Solution {
public:
    int climbStairs(int n) {
        vector<int> dp = {1,2};
        int index = 1;
        if (n < 3) return dp[n-1];
        for(int i=2; i<n; i++)
        {
            dp.push_back(dp[index] + dp[index-1]);
            index++;
        }
        return dp[index];
    }
};
```

## 6 Oct | Find All Duplicates in an Array

* We will use the absolute value of nums[i] as the index to mark the visited elements.

```cpp
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans;
        for(auto e : nums)
        {
            e = abs(e);
            if(nums[e-1] < 0) ans.push_back(e);
            else nums[e-1] *= -1;
        }
        return ans;
    }
};
```

## 6 Oct | Find All Duplicates in an Array

* We will use the absolute value of nums[i] as the index to mark the visited elements.

```cpp
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans;
        for(auto e : nums)
        {
            e = abs(e);
            if(nums[e-1] < 0) ans.push_back(e);
            else nums[e-1] *= -1;
        }
        return ans;
    }
};
```

### 12 | Guess Number Higher or Lower

* The trick is to use ``mid = l + (r - l)/2`` to avoid stackoverflow.

```cpp
class Solution {
public:
    int guessNumber(int n) {
        int l = 1 , r = n ;
        while(l <= r) 
        {
            int m = l + (r-l)/2 ;
            if(guess(m) == 0) 
                return m ;
            if(guess(m) < 0) 
                r = m - 1 ;
            else 
                l = m + 1 ;
        }
        return 0;
    }
};
```

### 21 | Insert Delete GetRandom()

```cpp
class RandomizedSet {
public:
set<int> st;
    
bool insert(int val) {
    if(!st.count(val)){
        st.insert(val);
        return true;
    }
    return false;
}

bool remove(int val) {
    if(st.count(val)){
        st.erase(val);
        return true;
    }
    return false;
}

int getRandom() {
   int offset = rand()%st.size();
    auto itr = st.begin();
    advance(itr,offset);
    return *itr;
}
};
```

### 28 | 3Sum

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
  	vector<vector<int>> result;
    size_t n = nums.size();
	if (n < 3)
		return result;
	
	sort(nums.begin(), nums.end());
        
	for (int i = 0; i < n; ++i) {
		if (nums[i] > 0) break;
		if (i > 0 and nums[i] == nums[i-1]) continue;
		int left = i+1, right = n - 1;
		while (left < right) {
			int sum = nums[i] + nums[left] + nums[right];
			if (sum < 0) 
				++left;
			else if (sum > 0) 
				--right;
			else {
				result.push_back({nums[i], nums[left], nums[right]});
				int ll = nums[left], rr = nums[right];
				while (left < right && nums[left] == ll) ++left;
				while (left < right && nums[right] == rr) --right;
			}
		}

	}
	return result;
    }
};
```