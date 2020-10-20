#题目
leetcode : [有效的括号](https://leetcode-cn.com/problems/valid-parentheses/submissions/)

## 栈
```Java
class Solution {
    public boolean isValid(String s) {
        Map<Character, Character> map = new HashMap<>();
        map.put(')', '(');
        map.put('}', '{');
        map.put(']', '[');

        Stack<Character> stack = new Stack<>();
        for(int i=0;i<s.length();i++){
            if(!map.containsKey(s.charAt(i))){
                stack.add(s.charAt(i));
                continue;
            }

            if(stack.empty()){
                return false;
            }
            Character left = stack.pop();
            if(left!=map.get(s.charAt(i))){
                return false;
            }
        }
        return stack.empty() ? true : false;
    }
}
```
