---
title: "Nov | Leetcoding Challenge"
author: Priyashu Tiwari
date: 2021-11-1 20:00:00 +0530
categories: [leetcode]
tags: [leetcode, nov]
---

## 1 Nov | 130. Surrounded Regions

```cpp
class Solution {
public:
    void DFS(vector<vector<char>>& board, int x, int y, char c) {
        if (x < 0 || x >= board.size() || y < 0 || y >= board[0].size() || board[x][y] != 'O')                 return;
            
        board[x][y] = c;
        DFS(board, x + 1, y, c);
        DFS(board, x - 1, y, c);
        DFS(board, x, y + 1, c);
        DFS(board, x, y - 1, c);
    }
    
    void solve(vector<vector<char>>& board) {
        int n = board.size(), m = board[0].size();
        for (int i = 0; i < n; i++) {
            if (board[i][0] == 'O') DFS(board, i, 0, '!');
            if (board[i][m-1] == 'O') DFS(board, i, m-1, '!');
        }
        
        for (int i = 0; i < m; i++) {
            if (board[0][i] == 'O') DFS(board, 0, i, '!');
            if (board[n-1][i] == 'O') DFS(board, n-1, i, '!');
        }
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (i && j && i < n - 1 && j < m - 1 && board[i][j] == 'O') board[i][j] = 'X';
                if (board[i][j] == '!') board[i][j] = 'O';
            }
        }
    }
};
```

## 2 Nov | 980. Unique Paths III

```cpp
class Solution {
public:
    int res = 0, empty = 1;
    void dfs(vector<vector<int>>& grid, int x, int y, int count) {
        if (x < 0 || x >= grid.size() || y < 0 || y >= grid[0].size() || grid[x][y] == -1) return;
        
        if (grid[x][y] == 2) {
            if(empty == count) res++; 
            return;
        }
        
        grid[x][y] = -1;
        
        dfs(grid, x+1, y, count+1);
        dfs(grid, x-1, y, count+1);
        dfs(grid, x, y+1, count+1);
        dfs(grid, x, y-1, count+1);
        
        grid[x][y] = 0;
        
    }
    
    int uniquePathsIII(vector<vector<int>>& grid) {
        int start_x, start_y;
        for (int i = 0; i < grid.size(); i++) {
            for (int j = 0; j < grid[0].size(); j++) {
                if (grid[i][j] == 1) start_x = i, start_y = j;
                else if (grid[i][j] == 0) empty++;
            }
        }
        
        dfs(grid, start_x, start_y, 0);
        return res;
    }
};
```

## 4 Nov | 404. Sum of Left Leaves

```cpp
class Solution {
public:
    int sumOfLeftLeaves(TreeNode* root) {
        int ans = 0;
        if (root == NULL)
            return 0;
        if (root->left != NULL)
            ans += sumOfLeftLeaves(root->left);
        if (root->right != NULL)
            ans += sumOfLeftLeaves(root->right);
        if(root->left and root->left->left == NULL and root->left->right == NULL)
            ans += root->left->val;
        return ans;
    }
};
```

## 5 Nov |  441. Arranging Coins

```cpp
class Solution {
public:
    int arrangeCoins(int n) {
        return int(sqrt(8*long(n)+1)-1)/2;
    }
};
```

## 6 Nov | 260. Single Number III

#### Worst 

* Sort the vector and skip `` if num[i] == num[i+1] ``
* Time Complexity : **O(nlongn)** 
* Space Complexity : **O(n)** / **O(1)**

```cpp
vector<int> singleNumber(vector<int> &nums) {
	sort (nums.begin(), nums.end());
	vector<int> ans;
	int i = 0, n = nums.size();
	while (i < n - 1)
		if (nums[i] == nums[i + 1]) i += 2;
		else ans.push_back(nums[i++]);
            
	if (ans.size() == 1) 
		ans.push_back(nums.back());

	return ans;
}
```

#### Better

* Use hashmap to store the frequency of each element.
* Time Complexity : **O(n)**
* Space Complexity : **O(n)**

```cpp
vector<int> singleNumber(vector<int> &nums) {
	unordered_map<int, int> freq;
	for (auto &num: nums) ++freq[num];
	vector<int> ans;
	for (auto &[ele, f]: freq)
		if (f == 1)
			ans.push_back(ele);
	return ans;
}
```

#### Better 

* Use hashset and ``erase`` all the visited elements.
* Time Complexity : **O(n)** 
* Space Complexity : **O(n)**

```cpp
vector<int> singleNumber(vector<int> &nums) {
	unordered_set<int> visited;
	for (auto &num: nums)
		if (visited.count(num))
			visited.erase(num);
		else visited.insert(num);
	return vector<int> (visited.begin(), visited.end());
}
```

#### Optimal

* Use three variable pointing to and 
* Time Complexity : **O(n)**
* Space Complexity : **O(1)**

```cpp
class Solution {
public:
     vector<int> singleNumber(vector<int>& nums) {
        long long int x_or = nums[0], x = 0, n = nums.size();
        
        for(int i = 1; i < n; i++)  x_or ^= nums[i];
        
        long long int sbn = x_or & ~(x_or - 1);
        
        for(int i = 0; i < n; i++)
            if(sbn & nums[i])
                x ^= nums[i];
            
        return {(int)x, (int)sbn^x};
    }
};
```
