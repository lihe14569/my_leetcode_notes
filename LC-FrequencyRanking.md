# LC Problems ranked in Frequency(Medium)

## 1041. Robot Bounded In Circle

```
Input: (String) Instrucitons string with  only letter G, L and R.

Condition: "G": go straight 1 unit; "L": turn 90 degrees to the left; "R": turn 90 degrees to the right.

Output: (Boolean) return true if and only if there exists a circle in the plane such that the robot never leaves the circle.
```

Solution:

```java
class Solution {
    public boolean isRobotBounded(String instructions) {
        //north = 0, east = 1, south = 2, west = 3
        int[][] dirs = new int[][]{{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
        //start position (0, 0) and face north
        int x = 0, y = 0, dir = 0;
        
        for(char i : instructions.toCharArray()) {
            if(i == 'L') 
                dir = (dir + 3) % 4;
            else if(i == 'R')
                dir = (dir + 1) % 4;
            else {
                //update position
                x += dirs[dir][0];
                y += dirs[dir][1];
            }
        }
        //If go through one cycle of instruction and back to start posiiont or Robot doesn't face to north, it is Limit Cycle Trajectory
        return (x == 0 && y == 0) || (dir != 0);
    }
}
```

Time complexity: **O(N)**
Space complexity: **O(1)**

