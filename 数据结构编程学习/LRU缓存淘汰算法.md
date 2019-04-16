# LRU缓存淘汰算法
* Least Rencently Used
* 使用双端链表加哈希表实现

```
//LRU least recently used  缓存淘汰算法

#include<iostream>
#include<map>

using namespace std;


/* Definiton of cachelist node, it's double linked list node */
struct CacheNode
{
	int key;
	int value;
	CacheNode *pre, *next;
	CacheNode(int k, int v): key(k),value(v),pre(NULL),next(NULL){}
};

class LRUCache
{
	private:
		int size;// Maxmum of the cachelist
		CacheNode *head, *tail;
		map<int,CacheNode *>mp;// use hashmap to store
	public:
		LRUCache(int capacity)
		{
			size = capacity;
			head = NULL;
			tail = NULL;

		}

		int get(int key)
		{
			map<int, CacheNode *>::iterator it = mp.find(key);
			if(it!=mp.end())
			{
				CacheNode *node = it->second;
				remove(node);
				setHead(node);
				return node->value;
			}
			else
				return -1;
		}

		void set(int key, int value)
		{
			map<int,CacheNode *>::iterator it = mp.find(key);
			if(it != mp.end())
			{
				CacheNode *node = it->second;
				node->value = value;
				remove(node);
				setHead(node);

			}
			else
			{
				CacheNode *newnode = new CacheNode(key,value);
				if(mp.size()>=size)
				{
					map<int, CacheNode *>::iterator iter = map.find(tail->key);
					remove(tail);
					mp.erase(iter);
				}
				setHead(newnode);
				mp[key] = newnode;
			}
		}

		void remove(CacheNode *node)
		{
			if(node->pre != NULL)
				node->pre->next = node->next;
			else
				head = node->next;
			if (node->next != NULL)
				node->next->pre = node->pre;
			else
				tail = node->pre;
		}
		void setHead(CacheNode *node)
		{
			node->next = head;
			node->pre =NULL;

			if(head != NULL)
			{
				head->pre = node;
			}
			head = node;

			if (tail ==NULL)
			{
				tail = head;
			}
		}
} ;


int main()
{
	LRUCache *lru = new LRUCache(2);
	lru->set(2,1);
	leu->set(1,1);
	cout<<lru->get(2)<<endl;
	lru->set(4,1);
	cout<<lru->get(1)<<endl;
	cout<<lru->get(2)<<endl;

	return 0;
	
}
```