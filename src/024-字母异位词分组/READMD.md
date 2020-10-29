# 题目

leetcode : [字母异位词分组](https://leetcode-cn.com/problems/group-anagrams/)

## 哈希建立映射 排序
```Java
    class Solution {

        public List<List<String>> groupAnagrams(String[] strs) {

            Map<String, List<String>> map = new HashMap<>();
            List<List<String>> res = new LinkedList<List<String>>();
            for(int i=0;i<strs.length;i++){
                char[] chars = strs[i].toCharArray();
                Arrays.sort(chars);
                String key = new String(chars);
                if(map.containsKey(key)){
                    map.get(key).add(strs[i]);
                }
                else{
                    List<String> s = new LinkedList<>();
                    s.add(strs[i]);
                    map.put(key, s);
                }
            }
            for(Map.Entry entry: map.entrySet()){
                res.add((List<String>) entry.getValue());
            }
            return res;
        }
    }

```

## 哈希建立映射 素数
```Java
    class Solution {
        public List<List<String>> groupAnagrams(String[] strs) {
            int[] prime = getPrime();
            Map<Long, List<String>> map = new HashMap<>();
            List<List<String>> res = new LinkedList<List<String>>();

            for(int i=0;i<strs.length;i++){
                String s = strs[i];
                Long key = 1L;
                for(int j=0;j<s.length();j++){
                    key*=prime[s.charAt(j)-'a'];
                }
                if(map.containsKey(key)){
                    map.get(key).add(s);
                }
                else{
                    map.put(key, new LinkedList<String>(){{add(s);}});
                }
            }
            for(Long i:map.keySet()){
                res.add(map.get(i));
            }
        return res;
        }


        public int[] getPrime(){
            int[] prime = new int[26];
            int[] nums = new int[400];
            for(int i=2;i<200;i++){
                if(nums[i]==0){
                    int index = i*2;
                    while(index<nums.length){
                        nums[index] = 1;
                        index+=i;
                    }
                }
            }
            int i=0;
            for(int j=2;j<nums.length;j++){
                if(i==26){
                    break;
                }
                if(nums[j]==0){
                    prime[i] = j;
                    i++;
                }
            }
            return prime;
        }
    }
```

### 埃式筛法求素数
```Java
        public int[] getPrime(){
            int[] prime = new int[26];
            int[] nums = new int[400];
            for(int i=2;i<200;i++){
                if(nums[i]==0){
                    int index = i*2;
                    while(index<nums.length){
                        nums[index] = 1;
                        index+=i;
                    }
                }
            }
            int i=0;
            for(int j=2;j<nums.length;j++){
                if(i==26){
                    break;
                }
                if(nums[j]==0){
                    prime[i] = j;
                    i++;
                }
            }
            return prime;
        }
    }
```
