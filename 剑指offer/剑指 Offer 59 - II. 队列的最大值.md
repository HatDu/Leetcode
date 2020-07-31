#### [剑指 Offer 59 - II. 队列的最大值](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

难度中等127

请定义一个队列并实现函数 `max_value` 得到队列里的最大值，要求函数`max_value`、`push_back` 和 `pop_front` 的**均摊**时间复杂度都是O(1)。

若队列为空，`pop_front` 和 `max_value` 需要返回 -1

**示例 1：**

```
输入: 
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
输出: [null,null,null,2,1,2]
```

**示例 2：**

```
输入: 
["MaxQueue","pop_front","max_value"]
[[],[],[]]
输出: [null,-1,-1]
```

 

**限制：**

- `1 <= push_back,pop_front,max_value的总操作数 <= 10000`
- `1 <= value <= 10^5`



**思路：**

使用两个队列，一个先进先出fifoQueue，另一个队列maxQueue用来存储当前的最大值。



maxQueue有如下特性：例如输入队列1115224，当入队执行到5其前面的1可以被删除，因为5不会在1之前出队，同理，4也不会在2之前出队。

- 入队：fifoQueue入队；从后向前比较插入值与队列尾端的值，若小于插入值则弹出（保存重复的值）
- 出队：判断fifoQueue队首是否等于maxQueue队首，若等于两个队列军弹出一次，否则只弹出fifoQueue队首

**代码：**

注意：Java中的Integer对象比较要用equals

```java
class MaxQueue {
    private LinkedList<Integer> fifoQueue;
    private LinkedList<Integer> maxQueue;
    public MaxQueue() {
        fifoQueue = new LinkedList<>();
        maxQueue = new LinkedList<>();
    }  
    
    public int max_value() {
        if(maxQueue.size() !=0){
            return maxQueue.peekFirst();
        }
        return -1;
    }
    
    public void push_back(int value) {
        while(maxQueue.size() != 0 && maxQueue.peekLast() < value){
            maxQueue.pollLast();
        }
        maxQueue.offerLast(value);
        fifoQueue.offerLast(value);
    }
    
    public int pop_front() {
        if(maxQueue.size() != 0 && maxQueue.peekFirst().equals(fifoQueue.peekFirst())){
            maxQueue.pollFirst();
        }
        return fifoQueue.size() == 0 ? -1 : fifoQueue.pollFirst();
    }
}

/**
 * Your MaxQueue object will be instantiated and called as such:
 * MaxQueue obj = new MaxQueue();
 * int param_1 = obj.max_value();
 * obj.push_back(value);
 * int param_3 = obj.pop_front();
 */
```

