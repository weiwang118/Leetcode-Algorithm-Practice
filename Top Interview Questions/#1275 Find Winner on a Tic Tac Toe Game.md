#### #1275 Find Winner on a Tic Tac Toe Game
[Leetcode #1275](https://leetcode.com/problems/find-winner-on-a-tic-tac-toe-game/)  

##### My Solution
```
class Solution {
public:
    string tictactoe(vector<vector<int>>& moves) {
        int grid[3][3];
        memset(grid,-10,sizeof(grid));
        for(int i=0;i<moves.size();i++){
                if(i%2==0)
                grid[moves[i][0]][moves[i][1]]=1;
                else grid[moves[i][0]][moves[i][1]]=2;
        }
        for(int i=0;i<3;i++){
                if(grid[i][0]+grid[i][1]+grid[i][2]==3||grid[0][i]+grid[1][i]+grid[2][i]==3)
                        return "A";
                if(grid[i][0]+grid[i][1]+grid[i][2]==6||grid[0][i]+grid[1][i]+grid[2][i]==6)
                        return "B";
        }
        if(grid[0][0]+grid[1][1]+grid[2][2]==3||grid[0][2]+grid[1][1]+grid[2][0]==3)
                return "A";
        else if(grid[0][0]+grid[1][1]+grid[2][2]==6||grid[0][2]+grid[1][1]+grid[2][0]==6)
                return "B";
        if(moves.size()<9)
                return "Pending";
        return "Draw";
    }
};
```
Time Complexity: O(n)  
Space Complexity:O(1)  

#### Solution from discussion board
```
 string tictactoe(vector<vector<int>>& moves) {
      vector<int> A(8,0), B(8,0); // 3 rows, 3 cols, 2 diagonals
      for(int i=0; i<moves.size(); i++) {
          int r=moves[i][0], c=moves[i][1];
          vector<int>& player = (i%2==0)?A:B;
          player[r]++;
          player[c+3]++; 
          if(r==c) player[6]++;
          if(r==2-c) player[7]++;
      }
      for(int i=0; i<8; i++) {
          if(A[i]==3) return "A";
          if(B[i]==3) return "B";
      }
      return moves.size()==9 ? "Draw":"Pending";
  }
  ```
  Time Complexity: O(n)  
  Space Complexity: O(1)  
  
  
