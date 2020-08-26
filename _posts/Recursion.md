### Number of Islands

```java
public class Solution {
    
    char[][] island;
    
    public int numIslands(char[][] grid) {
        int count = 0;
        
        this.island = grid;
        for(int i = 0; i < island .length; i++){
            for(int j = 0; j < island [i].length; j++){
                /*find a cell belong to an island, then disappear the whole 
                  island and increase count*/
                if(island [i][j] == '1'){
                    disappear(i,j);
                    count++;
                }
            }
        }
        return count;
    }
    
    //Use for disapearing an island
    public void disappear(int i, int j){
        //array edge detect
        if(i < 0 || i >= island .length){
            return;
        }
        if(j < 0 || j >= island [i].length){
            return;
        }
        //island edge detect
        if(island [i][j] == '0'){
            return;
        }
        
        //disapear this cell
        island [i][j] = '0';
        //disapear other cell in the same island
        disappear(i + 1, j);
        disappear(i - 1, j);
        disappear(i, j + 1);
        disappear(i, j - 1);
    }
}
```