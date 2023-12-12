> LeetCode - 1464. Maximum Product of Two Elements in an Array - Easy  
> <a href="https://leetcode.com/problems/maximum-product-of-two-elements-in-an-array/">Source</a>

## Problem
<div>Given the array of integers <code>nums</code>, you will choose two different indices <code>i</code> and <code>j</code> of that array. <em>Return the maximum value of</em> <code>(nums[i]-1)*(nums[j]-1)</code>.
<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [3,4,5,2]
<strong>Output:</strong> 12 
<strong>Explanation:</strong> If you choose the indices i=1 and j=2 (indexed from 0), you will get the maximum value, that is, (nums[1]-1)*(nums[2]-1) = (4-1)*(5-1) = 3*4 = 12. 
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [1,5,4,5]
<strong>Output:</strong> 16
<strong>Explanation:</strong> Choosing the indices i=1 and j=3 (indexed from 0), you will get the maximum value of (5-1)*(5-1) = 16.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> nums = [3,7]
<strong>Output:</strong> 12
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= nums.length &lt;= 500</code></li>
	<li><code>1 &lt;= nums[i] &lt;= 10^3</code></li>
</ul>
</div>

## Solution
### My First Approach - Sorting
```java
class Solution {
    public int maxProduct(int[] nums) {
        Arrays.sort(nums);
        return (nums[nums.length-1]-1)*(nums[nums.length-2]-1);
    }
}
```
This is the simplest way to solve the problem using the Arrays library. When using ```Arrays.sort```, the numbers are sorted in ascending order. Therefore, you can select the last two numbers to obtain the maximum value.

#### Time Complexity
$$ O(n log n) $$

### My Second Approach - Priority Queue
```java
class Solution {
    public int maxProduct(int[] nums) {
        PriorityQueue<Integer> pq = new PriorityQueue<Integer>(Collections.reverseOrder());
        for(int i = 0 ; i < nums.length; i++){
            pq.add(nums[i]);
        }
        return (pq.remove()-1) * (pq.remove()-1);
    }
}
```
After seeing the category of this problem, I solved it using a Priority Queue. However, the time complexity of the PQ is also nlogn. This is because adding and element to the PQ takes logn times, and the total length of nums is n. Therefore, there is no significant improvement in terms of time complexity.

#### Time Complexity
$$ O(n log n) $$

### LeetCode Approach - Track Second Biggest
```java
class Solution {
    public int maxProduct(int[] nums) {
        int biggest = 0, secondBiggest = 0;
        for(int i = 0; i < nums.length; i++){
            if (nums[i] > biggest) {
                secondBiggest = biggest;
                biggest = nums[i];
            } else {
               secondBiggest = Math.max(secondBiggest, nums[i]);
            }
        }
        return (biggest-1)*(secondBiggest-1);
    }
}
```
Without sorting, you can easily find the maximum element is ```nums``` by iterating over ```nums``` and coninuously updating a variable with the largest value. When the current value is greater than the ```biggest```, update ```biggest```, and the second biggest value becomes the previous value of ```biggest```. Otherwise, do not update the ```biggest``` and compare/update ```secondBiggest``` by comparing the current value with the previous ```secondBiggest```. This approach allow us to obtain the largest and second-largest values.
#### Time Complexity
$$ O(n) $$
#### Space Complexity
$$ O(1) $$

## Related Topics
- Array
- Sorting
- Heap(Primary Queue)

## Companies
- Amazon(2)
- Cisco(2)
