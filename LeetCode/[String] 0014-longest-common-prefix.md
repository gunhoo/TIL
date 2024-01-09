> LeetCode 14. Longest Common Prefix - Easy  
> <a href="https://leetcode.com/problems/longest-common-prefix/">Source</a>

## Problem
<h2><a href="https://leetcode.com/problems/longest-common-prefix/">14. Longest Common Prefix</a></h2><h3>Easy</h3><hr><div><p>Write a function to find the longest common prefix string amongst an array of strings.</p>

<p>If there is no common prefix, return an empty string <code>""</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> strs = ["flower","flow","flight"]
<strong>Output:</strong> "fl"
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> strs = ["dog","racecar","car"]
<strong>Output:</strong> ""
<strong>Explanation:</strong> There is no common prefix among the input strings.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= strs.length &lt;= 200</code></li>
	<li><code>0 &lt;= strs[i].length &lt;= 200</code></li>
	<li><code>strs[i]</code> consists of only lowercase English letters.</li>
</ul>
</div>

## Solution
### My Approach - Brute-Force
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0) return "";
        else if(strs.length == 1 || strs[0].equals("")) return strs[0];
        String prefix = strs[0];
        for (int i = 1; i < strs.length ; i++) {
            if(strs[i].equals("")) return "";
            StringBuilder answer = new StringBuilder();
            int c = 0;
            while(prefix.charAt(c) == strs[i].charAt(c) ){
                answer.append(strs[i].charAt(c));
                c++;
                if(c >= prefix.length() || c >= strs[i].length()) break;
            }
            if( c == 0) return "";
            else prefix = answer.toString();
        }
        return prefix;
    }
}
```
I solved it with a very messy code. While iterating through all `strs`, update the new string `prefix` by comparing the previous `prefix` with new string `strs[i]`. Since the comparison is done using the `charAt` method, the time comlexity would be worse.

#### Time Complexity - Worst case
$$ O(NlogN) $$

### LeetCode Solution - Horizontal Scanning
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0) return "";
        String prefix = strs[0];
        for(int i = 1; i <strs.length ; i++){
            while(strs[i].indexOf(prefix) != 0){
                prefix = prefix.substring(0, prefix.length()-1);
                if(prefix.isEmpty()) return "";
            }
        }
        return prefix;
    }
}
```


#### Time Complexity
$$ O(N) $$

## Related Topics
- String
- Trie

## Companies
- Amazon(20)
- Adobe(10)
- Google(9)
- Facebook(9)
- Apple(9)
- Uber(6)
- IBM(4)
