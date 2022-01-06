### Sliding Window Notes
This method is often used to simplify a nested for loop to a single for loop so that it reduces the time complexity.  
#### When will this method be used?
A. The problem will involve a data structure that is ordered and iterable like an array or a string.  
B. You are looking for some subrange in that array/string, like a longest, shortest or target value.  
C. There is an apparent naive or brute force solution that runs in O(N²), O(2^N) or some other large time complexity.  
With this method, you can always solve the problem with O(n) time complexity and O(1) space complexity.  

#### How many types of sliding window?
A. Fast/Slow  
These ones have a fast pointer that grows your window under a certain condition. So for Minimum Window Substring, you want to grow your window until you have a window that contains all the characters you’re looking for.
It will also have a slow pointer, that shrinks the window. Once you find a valid window with the fast pointer, you want to start sliding the slow pointer up until you no longer have a valid window.
So in the Minimum Window Substring problem, once you have a substring that contains all the characters you’re looking for, then you want to start shrinking it by moving the slow pointer up until you no longer have a valid substring (meaning you no longer have all the characters you’re looking for)  

B. Fast/Catch Up  
This is very similar to the first kind, except, instead of incrementing the slow pointer up, you simply move it up the fast pointer’s location and then keep moving the fast pointer up. It sort of “jumps” to the index of the fast pointer when a certain condition is met.
This is apparent in the Max Consecutive Sum problem. Here you’re given a list of integers, positive and negative, and you are looking for a consecutive sequence that sums to the largest amount. Key insight: The slow pointer “jumps” to the fast pointer’s index when the current sum ends up being negative. More on how this works later.
For example, in the array: [1, 2, 3, -7, 7, 2, -12, 6] the result would be: 9 (7 + 2)  

C. Fast/Lagging  
This one is a little different, but essentially the slow pointer is simply referencing one or two indices behind the fast pointer and it’s keeping track of some choice you’ve made.
In the House Robber problem you are trying to see what the maximum amount of gold you can steal from houses that are not next door to each other. Here the choice is whether or not you should steal from the current house, given that you could instead have stolen from the *previous* house.  

D. Front/Back  
These ones are different because instead of having both pointers traveling from the front, you have one from the front, and the other from the back. An example of this is the Rainwater Problem where you are calculating the maximum amount of rainwater you can capture in a given terrain. Again, you are looking for a maximum value, though the logic is slightly different, you are still optimizing a brute force O(N²) solution.  

