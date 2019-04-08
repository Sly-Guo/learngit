# 实现栈-C++
> stack遵循‘后进先出’规则： Last in first out
> 


* 栈的5种基本操作

> 1. CREATE 创建一个空堆栈
> 
> 2. PUSH 将数据压入栈顶，并返回新栈
> 
> 3. POP 从栈顶弹出数据，并返回新栈
> 
> 4. EMPTY 判断栈是否为空
> 
> 5. FULL 判断栈是否为满
> 

## 数组实现
```
// c++ 栈的实现


// Mystack.h
#ifndef maxstack
#define maxstack

template<class T>
class Mystack
{
public:
	Mystack(int size);//初始化栈
	~Mystack();

	void clearStack();
	bool isEmpty();
	bool isFull();
	int stackLength();
	bool push(const T& elem);
	bool pop(const T& elem);
	void stackTraverse(bool isFromBottom);

private:
	T *m_pBuffer; //栈空间指针
	int m_size;
	int m_top;

};

#endif




// Mystack.cpp
// 
#include "Mystack.h"
#include <iostream>
using namespace std;

template<class T>
Mystack<T>::Mystack(int size)
{
	m_size = size;
	m_pBuffer = new char[size];
	m_top = 0;

}

template<class T>
Mystack<T>::~Mystack()
{
	delete [] m_pBuffer;
}

template<class T>
void Mystack<T>::clearStack()
{
	m_top = 0;
}

template<class T>
void Mystack<T>::isEmpty()
{
	return m_top==0 ? true : false;
}


template<class T>
bool Mystack<T>::isFull()
{
	return m_top == m_size ? true : false;
}

template<class T>
int Mystack<T>::stackLength()
{
	return m_top;
}

template<class T>
bool Mystack<T>::push(const T& elem)
{
	if(isFull())
		return false;
	
	m_pBuffer[m_top] = elem;
	m_top ++;
	return true;

}

template<class T>
bool Mystack<T>::pop(const T& elem)
{
	if(isEmpty())
		return false;
	m_top --;
	elem = m_pBuffer[m_top];
	return true;
}

template<class T>
void Mystack<T>::stackTraverse(bool isFromBottom)
{
	if(isFromBottom)
	{
		for (int i=0;i<m_toptop;i++)
		{
			cout<<m_pBuffer[i]<<",";
		}
		cout<<endl;
	}
	else
	{
		for (int i = m_top-1;i>=0;i--)
		{
			cout<<m_pBuffer[i]<<",";
		}
		cout<<endl;
	}
}



// main.cpp 用于测试栈功能

#include "Mystack.h"
#include <iostream>
using namespace std;

int main(void)
{
	Mystack<char> *pstack = new Mystack(5);

	pstack->push('h');
	pstack->push('e');
	pstack->push('e');
	pstack->push('e');
	pstack.push('o');

	if (pstack.isFull())
		cout<<"栈满"<<endl;



	pstack->stackTraverse(1);

	char ch;
	pstack->pop(ch);
	cout<<ch<<endl;

	delete pstack;
	pstack =NULL;
	system("pause");
	return 0;
}



```
## 链表实现
```
// c++链表实现栈

#include <iostream>
using namespace std;

template<class T>
struct linknode{
	T data;
	linknode* next;
}

template<class T>
class mystack{
public:
	mystack();
	~mystack(T &data);

	bool isEmpty();
	void push(const T& data);
	void pop(T& data);
	T& getTop();
private:
	linknode<T> *head;
	linknode<T> *top;
	int length;

};


//mystack.cpp 
#include "mystack.h"
#include <iostream>
using namespace std;

template<class T>
mystack<T>::mystack()
{
	head = NULL;
	top = NULL;
	length = 0;
	cout<<"The stack is constructed"<<endl;
}


template <class T>
mystack<T>::~mystack(T& data)
{
	while(!isEmpty())
		pop(data);
	cout<<"the stack is destructed"<<endl;
}

template<class T>
bool mystack<T>::isEmpty()
{
	if(head == NULL)
		return true;
	else
		return false;

}

template <class T>
void mystack<T>::push(const T& data)
{
	if(!head)
	{
		head = new linknode<T>;
		head->data = data;
		head->next = NULL;
		top = head;
		length++:
	}
	else
	{
		linknode<T> *p = new linknode<T>;
		p->data = data;
		p->next = NULL;
		top->next = p;
		top = p;
		length++:
	}

}

template <class T>
void mystack<T>::pop(T& data)
{
	if(!isEmpty())
	{
		linknode<T> *p = head;
		if()
	}
}


template <class T>
T& mystack<T>::getTop()
{
	if(!isEmpty())
		return top->data;

}


//main.cpp
#include "mystack.h"

int main()
{
	const int n =5;
	int data;
	mystack<int> stk;
	int a[n]={4,8 6,12,9};

	for(int i =0;i<n;i++)
	{
		stk.push(a[i]);
	}
	while(!stk.isEmpty())
	{
		data = stk.getTop();
		cout<<data<<endl;
		stk->pop();
		
	}
}
```

##模拟浏览器的前进与后退
```
//编程模拟实现一个浏览器的前进、后退功能

#include<iostream>
#include<string>
#include<stack>
using namespace std;

int main()
{



	stack<string> backward,forward;
	string now = "homepage.com";
	string execution = "do nothing";
	forward.push(now);
	cout<<"you are on the homepage now"<<endl;


	while(1)
	{
		cin>>execution;

		if(execution == "do nothing")
		{
			cout<<"you are on the "<<now<<"now"<<endl;

		}

		else if(execution == "FORWARD")
		{
			if(backward.empty())
			{
				cin>>now;
				forward.push(now);
				cout<<"you are on the "<<now<<"now"<<endl;
			}
			
			else
			{
				now = backward.pop();
				forward.push(now);
				cout<<"you are on the "<<now<<"now"<<endl;
			}

		}

		else if(execution == "BACKWARD")
		{
			if(forward.empty())
			{
				cout<<"The Bottom page already!"<<endl;
			}
			
			else
			{

				now = forward.pop();
				backward.push(now);
				now = forward.gettop();
				cout<<"you are on the "<<now<<"now"<<endl;
			}



		}


		else
		{
			cout<<"WRONG COMMANDS"<<endl;
		}
	}

	delete backward,forward;

	return 0;

}










 
 while(1)
{
  cin>>b;

  if(b=="VISIT")
  {
   cin>>now;
   cout<<now<<endl;
   backward.push(c);
   while(!forward.empty())
	{
    forward.pop();
    }
  }

  if(b=="BACK"){
   if(backward.size()!=0){
    c=backward.top();
    backward.pop();
    cout<<c<<endl;
    forward.push(now);
    now=c;
   }
   else{
    cout<<"Ignored"<<endl;
    c="csw.jlu.edu.cn";
   }
  }

  if(b=="FORWARD")
{
   if(forward.size()!=0){
    c=forward.top();
    forward.pop();
    cout<<c<<endl;
    backward.push(now);
    now=c;
   }
   else{
    cout<<"Ignored"<<endl;
   }
  }
  if(b=="QUIT"){
   break; 
  }
  if(b!="VISIT"&&b!="BACK"&&b!="FORWARD"&&b!="QUIT"){
   cout<<"输入错误！"<<endl;
  }
 } 
}

```

