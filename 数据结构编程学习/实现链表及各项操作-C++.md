# 实现链表及各项操作-C++
```
//C++链表
//由于是模板类，其定义和声明不能在两个文件中；
// Node.h

#ifndef NODE_H
#define NODE_H

template<class T>
class Node
{
public:
	Node<T>*next;
	Node<T>prev;
	T data;

};

#endif

#ifndef LINK_H
#define LINK_H
#include "Node.h"
#include <iostrem>
using namespace std;
class List
{
public:
	List();
	List(const List&lst); //拷贝构造函数
	~List();

	void add(T e);
	void remove(T, index);//移除结点
	T find(int, index);//查找结点
	bool isEmpty();
	int size();
	void show();
	void reverse();
	void removeAll();
private:
	Node<T> *head;
	Node<T> *tail;
	int length;
};

template<class T>
List<T>::List()
{
	head = new Node<T>;
	tail = new Node<T>;
	head->next = tail;
	head->prev = nullptr;
	tail->next = nullptr;
	tail->prev = head;
	length = 0;
}

//拷贝构造函数
template <class T>
List<T>::List(const List &lst)
{
	head = new Node<T>;
	head->prev = nullptr;
	tail = new Node<T>;
	head->next = tail;
	tail->prev = head;
	length = 0;
	Node<T> *p = new Node<T>;
	while(temp->next!=lst.tail)
	{
		temp = temp->next;
		tail->data = temp->data;
		Node<T> *p = new Node<T>;
		p->prev = tail;
		tail->next = p;
		tail = p;
		length++;


	}
	tail->next = nullptr;

}

template <class T>
void List<T>::add(T e)
{
	Node<T>* temp = this->tail;
	tail->data = e;
	tail->next = new Node<T>;
	Node<T> *p = tail;
	tail =  tail->next;
	tail->prev = p;
	tail->next = nullptr;
	length++;
}

template <class T>
T List<T>::find(int index)
{
	if(length == 0)
		return NULL;
	if (index >=length)
	{
		cout<<"out of bounds"<<endl;
		return NULL;
	}
	int x = 0;
	T data;
	Node<T> *p;
	if (x<length/2)
	{
		p = head->next;
		while (p->next !=nullptr && x++ !=index)
		{
			p = p->next;
		}
	}
	else
	{
		p = tail->prev;
		while (p->prev!=nullptr && x++!=index)
		{
			p = p->prev;
		}
	}
	return p->data;
}


template <class T>
void List<T>::reverse()
{
	if (length ==0)
		return NULL;
	Node<T>*p = tail->prev;
	while(p != head)
	{
		cout<<p->data<<" " <<endl;
		p= p->prev;
	}
	cout<<endl;
}