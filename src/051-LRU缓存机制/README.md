# 题目

leetcode ： [LRU缓存机制](https://leetcode-cn.com/problems/lru-cache/)

## 链表的细节操作
```Java
class LRUCache {

    class LRUNode{
        LRUNode pre;
        LRUNode next;
        int key;
        int value;
        public  LRUNode(){};
        public LRUNode(int key, int value){
            this.key = key;
            this.value = value;
        }
    }

    private int size;
    private Map<Integer, LRUNode> cache;
    private LRUNode HEAD;
    private LRUNode TAIL;

    public LRUCache(int capacity) {
        size = capacity;
        cache = new HashMap<Integer, LRUNode>();
        HEAD= new LRUNode();
        TAIL= new LRUNode();
        HEAD.next = TAIL;
        TAIL.pre = HEAD;
    }

    public int get(int key) {
        LRUNode node = cache.get(key);
        if(node==null){
            return -1;
        }
        moveToHead(node);
        return node.value;
    }

    public void put(int key, int value) {
        LRUNode node = cache.get(key);
        if(node==null){
            node = new LRUNode(key, value);
            addToHead(node);
            if(size==0){
                LRUNode removenode = rmoveTail();
                cache.remove(removenode.key);
            }
            else{
                size--;
            }
        }
        else{
            node.value = value;
            moveToHead(node);
        }
        cache.put(key, node);
    }

    private void addToHead(LRUNode node) {
        node.pre = HEAD;
        node.next = HEAD.next;
        HEAD.next.pre = node;
        HEAD.next = node;
    }


    private void removeNode(LRUNode node) {
        node.pre.next = node.next;
        node.next.pre = node.pre;
    }

    private void moveToHead(LRUNode node){
        removeNode(node);
        addToHead(node);
    }

    private LRUNode rmoveTail(){
        LRUNode node = TAIL.pre;
        removeNode(node);
        return node;
    }
}


```
