### 1

```java
import java.util.*;

class Solution {
    public int solution(int[] A) {
        // write your code in Java SE 8
        Integer gl = globalLeader(A);
        if (gl == null) return 0;
        
        int n = A.length;
        int[] dp = new int[n]; // # of occurrences of gl from left to position i.
        int curSum = 0;
        for (int i = 0; i < n; i ++) {
            if (A[i] == gl) curSum += 1;
            dp[i] = curSum;
        }
        
        int res = 0;
        int tSum = dp[n - 1]; // total count of gl
        for (int i = n - 2; i >= 0; i --) {
            int rCount = tSum - dp[i]; // gl count in range [i+1, n-1]
            int rLen = n - 1 - i;
            int lLen = i + 1;
            if (dp[i] > (lLen / 2) && rCount > (rLen / 2)) 
                res++;
        }
        return res;
    }
    
    
    private Integer globalLeader(int[] A) {
        Deque<Integer> stack = new LinkedList<>();
        for (int x : A) {
            if (stack.isEmpty() || stack.peek() == x) {
                stack.push(x);
            } else {
                stack.pop();
            }
        }
        if (stack.isEmpty()) return null;
        else return stack.peek();
    }
}
```

basic idea: find the global leader first. then check each candidate to see if they make a equileader.

because the equileader has to be the global leader: the equileader occurs more than half of times on both sides.
Also, there can't be an equileader that is not the global leader.

global and equi: Necessary and sufficient conditions to each other
