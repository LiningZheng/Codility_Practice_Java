### 1
```java
import java.util.*;

class Solution {
    public int solution(int[] H) {
        // write your code in Java SE 8
        Deque<Integer> stack = new LinkedList<>();
        int count = 0;
        for (int x : H) {
            if (stack.isEmpty() || x > stack.peek()) {
                stack.push(x);
            } else if (x < stack.peek()) {
                while (!stack.isEmpty() && x < stack.peek()) {
                    stack.pop();
                    count += 1;
                }
                if (stack.isEmpty() || stack.peek() < x) {
                    stack.push(x);
                }
            } // else, x == peek(), do nothing.
        }
        count += stack.size();
        return count;
    }
}
```

basic idea: form a block when you see a downhill relation with the previous wall. if you see an equal height to the previous wall, do nothig to the current wall.
