# 题目

leetcode : [字符串转整数（atoi）](https://leetcode-cn.com/problems/string-to-integer-atoi/)

##  状态机

状态机的基本定义：状态机是有限状态自动机的简称，是现实事物运行规则抽线而成的一个数学模型

状态机里的4个概念
- State 状态 ： 一个状态机必须要包含两个状态，每次都是从 开始态开始。
- Event 事件 ： 执行某个操作的触发条件
- Action 动作： 事件发生以后要执行的动作
- Transition 转换： 状态的变化


在这道题里， 程序在每个时刻有一个状态 S ，每次从字符串中读取一个字串 C ，并根据字符 C 进行相应的动作，然后转移到下一个动作S`。

![Alt text](https://github.com/willow-D/leetocode/blob/master/005-%E5%AD%97%E7%AC%A6%E4%B8%B2%E8%BD%AC%E6%95%B4%E6%95%B0%EF%BC%88atoi%EF%BC%89/%E7%8A%B6%E6%80%81%E6%9C%BA.png)


```
class Solution {
    public int myAtoi(String s) {
        Automation automation = new Automation();
        for(int i=0;i<s.length();i++){
            automation.next(s.charAt(i));
        }
        return (int)(automation.num * automation.sign);

    }

    
}

public class Automation{
    public long num;
    private String state;
    public int sign;

    private Map<String, String[]> table = new HashMap<>();

    public Automation(){
        this.num = 0;
        this.state = "start";
        this.sign = 1;
        table.put("start",new String[]{"start", "sign", "add_num", "end"});
        table.put("sign",new String[]{"end", "end", "add_num", "end"});
        table.put("add_num",new String[]{"end", "end", "add_num", "end"});
        table.put("end",new String[]{"end", "end", "end", "end"});
    }
    public void next(char c){
        state = table.get(state)[getCol(c)];
        if(state.equals("add_num")){
            num = num*10 + (c-'0');
            num = sign==1 ? Math.min(num, (long)Integer.MAX_VALUE) : Math.min(num, -(long)Integer.MIN_VALUE);
        }
        else if(state.equals("sign")){
            sign = c=='+' ? 1 : -1;
        }

    }
    public int getCol(char c){
        if(c==' '){
            return 0;
        }
        if(c=='+'||c=='-'){
            return 1;
        }
        if(c>='0'&&c<='9'){
            return 2;
        }
        return 3;
    }

}
```
