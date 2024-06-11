# graph
graph problems


417 Pacific Atlantic Water Flow (DFS)

![image](https://github.com/atishay2/graph/assets/52835993/ae565b0e-cb75-425c-8d4c-f3b0c6f2f94e)

![image](https://github.com/atishay2/graph/assets/52835993/8b58ea74-dc67-4dc8-9bbe-543dbd113093)

![image](https://github.com/atishay2/graph/assets/52835993/00680a91-29dd-47b3-b117-c9631688257b)


    class Solution:
      def pacificAtlantic(self, heights: List[List[int]]) -> List[List[int]]:
          ROW = len(heights) ; COL = len(heights[0])
          ATL = set() ; PAC = set()
          
          def dfs(i, j, visit):
              
              if i < 0 or j < 0 or i == ROW or j == COL or (i,j) in visit:
                  return 
              visit.add((i,j))
              
              for a,b in [(1,0), (0,1), (-1,0), (0,-1)]:
                  if 0 <= a+i < ROW and 0 <= b+j < COL and heights[i][j] <= heights[a+i][b+j]:
                      print (i, j, a+i, b+j)
                      dfs(a+i, b+j, visit)    
          
          for x in range(ROW):
              for y in range(COL):
                  if y == 0 or x == 0:
                      dfs(x,y, PAC)
                  if y == COL-1 or x == ROW -1:
                      dfs(x,y, ATL)
          
          
          res = []
          for m,n in ATL:
              if (m,n) in PAC:
                  res.append([m,n]) 
          return res

LC : 207. Course Schedule
![image](https://github.com/atishay2/graph/assets/52835993/84f593cc-3f5f-4136-819c-192494be177a)
![image](https://github.com/atishay2/graph/assets/52835993/f7e83235-1046-4e3d-9a28-bb90615b8974)


    class Solution:
        def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
            
            adj = {i : [] for i in range(numCourses)}
    
            for x,y in prerequisites:
                adj[x].append(y)
    
            cur_visit = set()
    
            def dfs(cur):
                
                
                if adj[cur] == []: return True
                for cr in adj[cur]:
                    if cr in cur_visit:
                        return False
                    cur_visit.add(cur)
                    if not dfs(cr): return False
                    
                    cur_visit.remove(cur)
                    adj[cur] = []
                return True
            
            for x in range(numCourses):
                if not dfs(x):
                    return False
            return True
