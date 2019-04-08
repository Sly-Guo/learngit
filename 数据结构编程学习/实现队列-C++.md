# 实现队列-C++
>queue遵循’先进先出‘原则：First in first out
>

* 队列的5种基本操作

>1. CREATE 创建空队列  
>
>2. ADD 将数据加入队列的末尾，返回新队列  
>
>3. DELETE 删除队列前端的数据 
>
>4. FRONT 返回队列前端的值
>
>5. EMPTY 判断队列是否为空
>

## 数组实现
```
//c++数组实现队列
#define maxsize = 4
#include <iostream>
using namespace std;
typedef int datatype;

typedef struct Queue
{
	datatype data[maxsize];
	int front,rear;//队列的头尾位置
	
};

//置空队列
bool Set_NULL(Queue &Q);

//判断队列是否为空
bool Is_NULL(Queue Q);

//入队
bool En_Queue(Queue &Q, datatype a);

//出队
bool De_Queue(Queue &Q);

//获取队列头元素
datatype front_element(Queue Q);

//Queue.cpp
#include <iostream>
#include "Queue.h"
using namespace std;

bool Set_NULL(Queue &Q)
{
	Q.front = -1;
	Q.rear = -1;
	return true;
}

bool Is_NULL(Queue Q)
{
	if (Q.front == Q.rear)
	{
		return true;
	}
	return false;
}


bool En_Queue(Queue &Q,datatype a)
{
	if((Q.rear - Q.front) >= maxsize-1)
	{
		cout<<"The queue is full "<<endl;
		return false;
	}
	else
	{
		Q.rear +=1;
		Q.data[Q.rear] = a;
		return true;
	}
}


bool De_Queue(Queue &Q)
{
	if(Is_NULL(Q))
	{
		cout<<"the queue is empty"<<endl;
		return false;
	}
	else
	{
		Q.front+=1;
		return true;
	}
}



datatype front_element(Queue Q)
{
	if (Is_NULL(Q))
	{
		cout<<"the queue is empty"<<endl;
		return NULL;
	}
	else
		return Q.data[Q.front]
}



//main.cpp
//
#include "Queue.h"
#include <iostream>
using namespace std;

int main()
{
	Queue Q;
	Set_NULL(Q);

	En_Queue(Q,2);
	En_Queue(Q,3);
	En_Queue(Q,0);
	En_Queue(Q,8);

	De_Queue(Q);

}
```
## 链表实现
```
//c++链表实现队列

#include <iostream>
using namespace std;

struct Qnode //定义队列结点的数据结构
{
	Qnode *next; //指针域，指向下一个结点
	double data;
};
struct Linknode //定义队列的数据结构
{
	Qnode *front;
	Qnode *rear;
	
};

void InitQueue(Linknode &Q)
//构造一个空的队列
{
	Qnode *q;
	q = new Qnode;//申请一个节点的空间
	q->next = NULL; //头结点
	Q.front = q;
	Q.rear = q;
}


bool isEmpty(Linknode Q)
{
	if(Q.front == Q.rear)
		return true;
	return false;

}


void EnQueue(Linknode &Q, double e)
//队列尾部插入元素
{
	Qnode *q;
	q = new Qnode;
	q->next = NULL;
	q->data = e;

	Q.rear->next = q;
	Q.rear = q;

}

void DeQueue(Linknode &Q, double &e)
//队列头部删除一个结点
{
	Qnode *q;
	q = Q.front->next;
	e= q->data; //保存要出列的数据

	Q.front->next = q->next;
	if (Q.rear == q) //若要删除的元素为尾结点，则头结点指向尾节点
	{
		Q.rear = Q.front;
	}
	delete q;


}

void DestroyQueue(Linknode &Q)
{
	while(Q.front)
	{
		Q.rear = Q.front->next;
		delete Q.front;
		Q.front = Q.rear;
	}
}



int main()
{
	Linknode *Q;
	Q = new Linknode;
	InitQueue(*Q);
	return 0;
	
}
```

## 循环队列
