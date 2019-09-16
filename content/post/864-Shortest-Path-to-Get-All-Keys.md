---
title: "864 Shortest Path to Get All Keys"
date: 2019-09-11T23:56:51-04:00
draft: true
---

We are given a 2-dimensional grid. "." is an empty cell, "#" is a wall, "@" is the starting point, ("a", "b", ...) are keys, and ("A", "B", ...) are locks.

We start at the starting point, and one move consists of walking one space in one of the 4 cardinal directions.  We cannot walk outside the grid, or walk into a wall.  If we walk over a key, we pick it up.  We can't walk over a lock unless we have the corresponding key.

For some 1 <= K <= 6, there is exactly one lowercase and one uppercase letter of the first K letters of the English alphabet in the grid.  This means that there is exactly one key for each lock, and one lock for each key; and also that the letters used to represent the keys and locks were chosen in the same order as the English alphabet.

Return the lowest number of moves to acquire all keys.  If it's impossible, return -1.

**Example 1:**

```
Input: ["@.a.#","###.#","b.A.B"]
Output: 8
```

**Example 2:**

```
Input: ["@..aA","..B#.","....b"]
Output: 6
```
思路：
看到最短路径，想到BFS，路径遍历过程中会遇到的状态有：
'#': 墙，不用处理直接跳过
'.': 可以走，加到队列里
'a-f': 钥匙，可以走，加到队列里，但钥匙的状态需要变
'A-F':锁，如果没有对应的钥匙，直接跳过，如果有对应的钥匙，可以走，加到队列

```
class Solution {
public:
    queue<vector<int>> q;
    int count = 0;
     int knt = 0;
    bool find = false;
    vector<vector<int>> dist = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    unordered_set<string> visited;
    int shortestPathAllKeys(vector<string>& grid) {
        int keys = 0;
        if(grid.empty()) return 0;
        int n = grid.size();
        int m = grid[0].size();
        int si = 0, sj = 0;
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(grid[i][j] == '@'){
                    si = i;
                    sj = j;
                }
                 if(grid[i][j] - 'a' >= 0 && grid[i][j] - 'a' <= 6){
                     knt ++;
                 }
            }
        }
        q.push({si, sj, 0});
        visited.insert(to_string(si)+" "+ to_string(sj) + " " + to_string(0));
        bfs(grid);
       if(find){
           return count;
       }
        return -1;
    }
    
    void bfs(vector<string>& grid){
        while(!q.empty()){
            int n = q.size();
            
            for(int l = 0; l < n; l ++){
                int i = q.front()[0];
                int j = q.front()[1];
                int tmp = q.front()[2];
                q.pop();
                if(tmp == (1<<knt)-1){
                    find = true;
                    return;
                }
                for(int k = 0; k < 4; k ++){
                    int keys = tmp;
                    int x = i + dist[k][0];
                    int y = j + dist[k][1];
                    if(x < 0 || y < 0 || x >= grid.size() || y >= grid[0].size() || grid[x][y] == '#') continue;
                    char c = grid[x][y];
                    if(c - 'A' >= 0 && c - 'A' <= 6 && ((keys >> (c - 'A')) & 1)  == 0){ //注意(keys >> (c - 'A')) & 1)
                        continue;
                    }

                    else if(c - 'a' >= 0 && c - 'a' <= 6){
                        keys |= ( 1<<(c-'a'));
                    }
                    
                    if(visited.find(to_string(x)+" "+ to_string(y) + " " + to_string(keys)) == visited.end()){
                        visited.insert(to_string(x)+" "+ to_string(y) + " " + to_string(keys));
                        q.push({x, y, keys});
                    }
                }
            }
            count ++;
        }
    }
};
```

待续：旅行商问题， 状态压缩问题