> LeetCode 20. Valid Parentheses - Easy  
> <a href="https://leetcode.com/problems/valid-parentheses/">Source</a>

## Problem
<div><p>Given a string <code>s</code> containing just the characters <code>'('</code>, <code>')'</code>, <code>'{'</code>, <code>'}'</code>, <code>'['</code> and <code>']'</code>, determine if the input string is valid.</p>

<p>An input string is valid if:</p>

<ol>
	<li>Open brackets must be closed by the same type of brackets.</li>
	<li>Open brackets must be closed in the correct order.</li>
	<li>Every close bracket has a corresponding open bracket of the same type.</li>
</ol>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> s = "()"
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> s = "()[]{}"
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> s = "(]"
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>4</sup></code></li>
	<li><code>s</code> consists of parentheses only <code>'()[]{}'</code>.</li>
</ul>
</div>

## Solution
### My Approach - Stack
```java
class Solution {
    public boolean isValid(String s) {
        // stack
        Stack<Character> stack = new Stack<>();
        for(int i=0; i<s.length(); i++) {
            if(stack.isEmpty()){
                if(isOpen(s.charAt(i))){
                    stack.push(s.charAt(i));
                } else {
                    return false;
                }
            } else {
                if(isOpen(s.charAt(i))) stack.push(s.charAt(i));
                else {
                    if(areMatch(stack.pop(), s.charAt(i))) continue;
                    return false;
                }
            }
        }
        if(stack.isEmpty()) return true;
        return false;
    }
    
    private boolean isOpen(char c) {
        if(c == '(' || c == '{' || c == '[' ) return true;
        return false;
    }
    
    private boolean areMatch(char a, char b){
        if(a == '{' && b == '}') return true;
        if(a == '(' && b == ')') return true;
        if(a == '[' && b == ']') return true;
        return false;
    }
}
```
I declared the stack to store a character of string `s`. While iterating through all chracters in the string, if the character is an opening bracket, it is pushed into the stack. Otherwise, validation is checked by popping the last character from the stack. This is because the stack has the characteristic of Last-In-Last-Out(LIFO).

#### Time Complexity - Worst case
$$ O(n) $$

### LeetCode Solution - Stack
```java
class Solution {

  // Hash table that takes care of the mappings.
  private HashMap<Character, Character> mappings;

  // Initialize hash map with mappings. This simply makes the code easier to read.
  public Solution() {
    this.mappings = new HashMap<Character, Character>();
    this.mappings.put(')', '(');
    this.mappings.put('}', '{');
    this.mappings.put(']', '[');
  }

  public boolean isValid(String s) {

    // Initialize a stack to be used in the algorithm.
    Stack<Character> stack = new Stack<Character>();

    for (int i = 0; i < s.length(); i++) {
      char c = s.charAt(i);

      // If the current character is a closing bracket.
      if (this.mappings.containsKey(c)) {

        // Get the top element of the stack. If the stack is empty, set a dummy value of '#'
        char topElement = stack.empty() ? '#' : stack.pop();

        // If the mapping for this bracket doesn't match the stack's top element, return false.
        if (topElement != this.mappings.get(c)) {
          return false;
        }
      } else {
        // If it was an opening bracket, push to the stack.
        stack.push(c);
      }
    }

    // If the stack still contains elements, then it is an invalid expression.
    return stack.isEmpty();
  }
}
```

#### Time Complexity
$$ O(n) $$

## Related Topics
- String
- Stack

## Companies
- Amazon(24)
- BlackRock(17)
- Bloomberg(14)
- Apple(14)
<!-- - Adobe(10) -->
- Google(12)
- Facebook(8)
- Microsoft(6)
- Oracle(6)
<!-- - Uber(6) -->
<!-- - IBM(4) -->
