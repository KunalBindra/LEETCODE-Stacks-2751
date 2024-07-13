# LEETCODE-Stacks-2751
Let's perform a dry run of the `survivedRobotsHealths` method in the `Solution` class with the following input:

```java
int[] positions = {5, 3, 10, 2};
int[] healths = {3, 2, 5, 1};
String directions = "RLRL";
```

### Step-by-step Execution

1. **Initialization:**
   ```java
   List<Integer> ans = new ArrayList<>();
   Robot[] robots = new Robot[positions.length]; // robots array
   List<Robot> stack = new ArrayList<>(); // running robots stack
   ```

2. **Creating Robots:**
   ```java
   for (int i = 0; i < positions.length; ++i)
     robots[i] = new Robot(i, positions[i], healths[i], directions.charAt(i));
   ```
   This creates the following `robots` array:
   ```
   [Robot(0, 5, 3, 'R'), Robot(1, 3, 2, 'L'), Robot(2, 10, 5, 'R'), Robot(3, 2, 1, 'L')]
   ```

3. **Sorting Robots by Position:**
   ```java
   Arrays.sort(robots, (a, b) -> a.position - b.position);
   ```
   After sorting by position, `robots` becomes:
   ```
   [Robot(3, 2, 1, 'L'), Robot(1, 3, 2, 'L'), Robot(0, 5, 3, 'R'), Robot(2, 10, 5, 'R')]
   ```

4. **Processing Robots:**

   - **Robot(3, 2, 1, 'L'):**
     - Direction is 'L', and the stack is empty, so it is added to the stack.
     - Stack: `[Robot(3, 2, 1, 'L')]`

   - **Robot(1, 3, 2, 'L'):**
     - Direction is 'L', and the stack is not empty but contains a 'L' robot, so it is added to the stack.
     - Stack: `[Robot(3, 2, 1, 'L'), Robot(1, 3, 2, 'L')]`

   - **Robot(0, 5, 3, 'R'):**
     - Direction is 'R', so it is added to the stack.
     - Stack: `[Robot(3, 2, 1, 'L'), Robot(1, 3, 2, 'L'), Robot(0, 5, 3, 'R')]`

   - **Robot(2, 10, 5, 'R'):**
     - Direction is 'R', so it is added to the stack.
     - Stack: `[Robot(3, 2, 1, 'L'), Robot(1, 3, 2, 'L'), Robot(0, 5, 3, 'R'), Robot(2, 10, 5, 'R')]`

5. **Processing Collisions:**
   Since all robots are either moving in the same direction or haven't collided based on the stack contents, no collisions occur.

6. **Sorting Stack by Index:**
   ```java
   stack.sort((a, b) -> a.index - b.index);
   ```
   The stack is already sorted by index:
   ```
   [Robot(0, 5, 3, 'R'), Robot(1, 3, 2, 'L'), Robot(2, 10, 5, 'R'), Robot(3, 2, 1, 'L')]
   ```

7. **Creating the Answer List:**
   ```java
   for (Robot robot : stack)
     ans.add(robot.health);
   ```
   Resulting `ans` list:
   ```
   [3, 2, 5, 1]
   ```

### Conclusion
The `survivedRobotsHealths` method returns `[3, 2, 5, 1]` for the given input, as no collisions occur and all robots survive with their initial healths.
