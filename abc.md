8# 队列
## 基本知识点
1. 队列
队列是一种**先进先出**的数据结构
元素从队尾入队，从队头出队

2. 基本操作
入队（enqueue）：向队尾添加元素。

出队（dequeue）：从队头移除元素。

查看队头（front/peek）：查看队头元素，但不移除。

判空（isEmpty）：判断队列是否为空。

判满（isFull）：判断队列是否已满（对于固定大小的队列）。

队列大小（size）：返回当前队列中元素个数。

3. 实现方式
顺序存储 （数组）
**优点** 访问快
**缺点** 出队浪费空间。常用循环队列
链式存储 （链表实现）
**优点** 动态大小，入队出队时间复杂度均为O(1)。
**缺点** 需要额外存储指针

4. 循环队列
解决数组实现队列“假溢出”
利用取模运算，实现队尾指针绕回数组七点
有时需区别满和空状态，常用“留一个空位”策略

5. 类型
普通队列：先进先出。

循环队列：数组实现，空间利用更高。

双端队列（Deque）：两端都可入队和出队。

优先队列（Priority Queue）：元素有优先级，优先级高的先出队。

阻塞队列：多线程环境下的队列，支持等待和通知。


## 练习题
1. 练习一
约瑟夫环问题（变形）

用队列模拟约瑟夫环，n个人围成一圈，每数到m的人出队，直到剩下最后一人，输出他的编号。
 ```
#include <iostream>
#include <queue>
using namespace std;

int main() {
    int n = 7; 
    int m = 3; //每组数列的第三个出队
    queue<int> q; // 创建队列
    for (int i = 1; i <= n; i++) q.push(i);

    while (q.size() > 1) {
        for (int i = 1; i < m; i++) {
            q.push(q.front());
            q.pop(); //删去离队数据
        }
        cout << "remove：" << q.front() << endl;
        q.pop();
    }
    cout << "remain：" << q.front() << endl;
    return 0;
}


 ```


 2. 练习二
 打印机任务调度

模拟一个打印机的任务队列：每个任务包含 任务ID 和 页数。每秒处理一页。当任务完成时，打印 “任务X完成”。
使用队列存储任务，并按顺序处理。
```
#include <iostream>
#include <queue>
#include <string>
using namespace std;

struct Task {
    int id;
    int pages;
};

int main() {
    queue<Task> printer;
    printer.push({1, 5});
    printer.push({2, 3});
    printer.push({3, 4});

    while (!printer.empty()) {
        Task t = printer.front();
        printer.pop();
        for (int i = 1; i <= t.pages; i++) {
            cout << "text" << t.id << " paging " << i << " page" << endl;
        }
        cout << "text" << t.id << " finish" << endl;
    }
    return 0;
}



```
