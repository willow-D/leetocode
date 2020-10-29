# 题目

leetcode : [电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

## dfs + 回溯 （推荐）
```Java
class Solution {
    public  List<String> letterCombinations(String digits) {
        List<String> res = new LinkedList<>();
        if(digits==null || digits.length()==0){
            return res;
        }

        Map<Character, String[]> map = new HashMap<>();
        map.put('2', new String[]{"a", "b", "c"});
        map.put('3', new String[]{"d", "e", "f"});
        map.put('4', new String[]{"g", "h", "i"});
        map.put('5', new String[]{"j", "k", "l"});
        map.put('6', new String[]{"m", "n", "o"});
        map.put('7', new String[]{"p", "q", "r", "s"});
        map.put('8', new String[]{"t", "u", "v"});
        map.put('9', new String[]{"w", "x", "y", "z"});
        StringBuilder combination = new StringBuilder();
        dfs(res, map, 0, digits, combination);
        return res;
    }
    public  void dfs(List<String> res, Map<Character, String[]> map, int index, String digits, StringBuilder combination){
        if(index==digits.length()){
            res.add(combination.toString());
            return;
        }
        String[] enter = map.get(digits.charAt(index));
        for(int i=0;i<enter.length;i++){
            combination.append(enter[i]);
            dfs(res, map, index+1, digits, combination);
            combination.deleteCharAt(index);
        }
    }
}

```


## 队列来实现
```Java
class Solution {
    public static List<String> letterCombinations(String digits) {
        List<String> res = new LinkedList<>();
        if(digits==null || digits.length()==0){
            return res;
        }

        Map<Character, String[]> map = new HashMap<>();
        map.put('2', new String[]{"a", "b", "c"});
        map.put('3', new String[]{"d", "e", "f"});
        map.put('4', new String[]{"g", "h", "i"});
        map.put('5', new String[]{"j", "k", "l"});
        map.put('6', new String[]{"m", "n", "o"});
        map.put('7', new String[]{"p", "q", "r", "s"});
        map.put('8', new String[]{"t", "u", "v"});
        map.put('9', new String[]{"w", "x", "y", "z"});


        Queue<String> queue = new LinkedList<>();
        for(int k=0;k<map.get(digits.charAt(0)).length;k++){
            queue.add(map.get(digits.charAt(0))[k]);
        }
        int cnt = queue.size();

        for(int i=1;i<digits.length();i++){
            for(int j=0;j<cnt;j++){
                String s = queue.poll();
                for(int k=0;k<map.get(digits.charAt(i)).length;k++){
                    queue.add(s+map.get(digits.charAt(i))[k]);
                }
            }
            cnt = queue.size();
        }
        
        for(int i=0;i<cnt;i++){
            res.add(queue.poll());
        }
        return res;
    }
}
```
