---
layout:     post
title:      min stack-java
description: 155 leetcode
categories: algorithms
keywords: leetcode, algorithm
---

### 0X00:问题描述  
&emsp;&emsp;Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.
it's an algorithm problem from the leetcode 155.  

### 0X01:minstack <br>
&emsp;&emsp;使用链表实现栈结构  
&emsp;&emsp;可以为每一个元素设置一个额外属性 **min**，每当进行一次压栈操作时，将压入的元素值与当前栈顶元素的min属性比较，求取最小的座位当前元素的min属性值  
这样可以保证每次需要知道当前栈内最小元素的时候只需一次就可以求解得到，实现难度也较低<br>

### 0X02:具体结构分析 
&emsp;&emsp;首先在栈对象初始化时 创建一个entry对象 head 作为栈的第一个元素 也是栈的结束标志当entry的next为空时说明栈已到底<br>		
**1.push：**
输入一个元素x 使用entry（int x，entry next）构造一个entry对象 将x输入为她的num,next输入为她的next.  
&emsp;&emsp;剩下一个min,最小值的比较与存储,由于我们的数据结构的特殊性，所以只需要比较栈顶第二个元素的min和当前元素（即栈顶元素）的num取较小的即可。<br><br>
**2.pop ：**
希望弹出一个元素，则可以直接将当前的head变成head.next 当栈为空时则弹出0<br><br>
**3.getmin ：**
到了这个问题的核心了，这也是这个数据结构设计的原因所在，得到当前的最小值，即直接输出head.min。  

### 0x03:代码实现
哇咔咔 这里贴上我的JAVA代码实现，不知道为什么，速度要比C/C++ 快很多，大神知道的留个言，多谢指导.  
<pre><code class="java">public class minstack {
	private entry head;
	public minstack() {
		// TODO Auto-generated constructor stub
		head=new entry();
	}
	public void push(int x) {
        head=new entry(x,head);
    }//压入一个x入栈。

    public void pop() {
    	if (head.next!=null) {
    		head=head.next;	
		}
    }

    public int top() {
    	 if (head.next!=null) {
         	return head.num;
 		}
         return 0;
    }

    public int getMin() {
        if (head.next!=null) {
        	return head.min;
		}
        return 0;
    }
	class entry {//每个栈元素的类，具有3个属性 ：min最小值、num栈元素所存的数值、next 栈顶第二个元素的对象索引。
		private int min; 
 		private int num=-1;
		public entry next=null;

		public entry(int num,entry next){
			this.next=next;
			this.num=num;	
			if(next.next!=null&&next.min<=num){//将两个if 压缩为一个，进行min的赋值
				this.min=next.min;
			}
			else{
				this.min=num;
			}
		}
		public entry(){}
	}
}
</code></pre>