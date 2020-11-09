# 题目

leetcode ： [实现前缀树](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)

## 
```Java
class Trie {
    private boolean isEnd = false;
    private Trie[] next = new Trie[26];

    /** Initialize your data structure here. */
    public Trie() {

    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        Trie root = this;
        char[] words = word.toCharArray();
        for(char c: words){
            if(root.next[c-'a']==null){
                root.next[c-'a'] = new Trie();
            }
            root = root.next[c-'a'];
        }
        root.isEnd = true;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        Trie root = this;
        char[] words = word.toCharArray();
        for(char c: words){
            if(root.next[c-'a']==null){
                return false;
            }
            root = root.next[c-'a'];
        }
        return root.isEnd;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        Trie root = this;
        char[] words = prefix.toCharArray();
        for(char c: words){
            if(root.next[c-'a']==null){
                return false;
            }
            root = root.next[c-'a'];
        }
        return true;
    }
}
```
