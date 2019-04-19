#  二叉树部分（Binary Tree)
## 链表实现二叉树
```
// 二叉树 Binary Tree链表实现
#include<iostream>
#include<cstdlib>
#include<iomanip>
using namespace std;
#define Arraysize 10

class Node//二叉树节点数据结构的声明
{
public:
	int value;
	struct Node *left_Node;
	struct Node *right_Node;

};

typedef class Node TreeNode;
typedef TreeNode *BinaryTree;
BinaryTree rootNode;

//将指定的值加入二叉树中适当的节点
void Add(int value)
{
	BinaryTree currentNode;
	BinaryTree newnode;
	int flag = 0;//用来记录是否插入新的节点
	newnode = (BinaryTree)malloc(sizeof(TreeNode));
	newnode->value = value;
	newnode->left_Node = NULL;
	newnode->right_Node = NULL;
	//如果为空的二叉树，便将新的节点设为根节点
	if(rootNode==NULL)
	{
		rootNode = newnode;
	}
	else
	{
		currentNode = rootNode;
		while(!flag)
		{
			if(value<currentNode->value)//移向左子树这边
			{
				if(currentNode->left_Node == NULL)
				{
					currentNode->left_Node = newnode;
				    flag = 1;
			     }
			     else
			     		currentNode = currentNode->left_Node;
			}
			else//移向右子树这边
			{
				if(currentNode->right_Node == NULL)
				{
					currentNode->right_Node = newnode;
					flag = 1;
				}
				else
					currentNode = currentNode->right_Node;
			}

		}
	}

}




int main()
{
	int tempdata;
	int content(Arraysize);
	int i = 0;
	rootNode = (BinaryTree)malloc(sizeof(TreeNode));
	
}
```

## 遍历

> 前中后

```
#include <iostream>
#include <iomanip>
using namespace std;
class tree //节点链表结构的声明
{  
	public :
	int data; //节点数据
	class tree *left,*right; //节点左指针和右指针 
};
typedef class tree node;
typedef node *btree;
btree creat_tree(btree,int);
void pre(btree);
void in(btree);
void post(btree);
int main(void)
{  
	int arr[]={7,4,1,5,16,8,11,12,15,9,2};//原始数组内容 
	btree ptr=NULL; //声明树根 
	cout<<"[原始数组内容]"<<endl;
	for (int i=0;i<11;i++)//建立二叉树，并将二叉树内容打印出来 
	{  
		ptr=creat_tree(ptr,arr[i]);
		cout<<"["<<setw(2)<<arr[i]<<"] ";
	}
	cout<<endl;
	cout<<"[二叉树的内容]"<<endl;
	cout<<"前序遍历结果："<<endl;//打印前、中、后序遍历结果 
	pre(ptr);
	cout<<endl;
	cout<<"中序遍历结果："<<endl;
	in(ptr);
	cout<<endl;
	cout<<"后序遍历结果："<<endl;
	post(ptr);
	cout<<endl;
	system("pause");
	return 0;
}
btree creat_tree(btree root,int val)//建立二叉树的子程序 
{  
	btree newnode,current,backup;   //声明一个新节点newnode存放数组数据 
	newnode = new node; //current和backup存放暂存指针 
	newnode->data=val;  //指定新节点的数据和左右指针 
	newnode->left=NULL;
	newnode->right=NULL;
	if (root==NULL)//如果root为空值，把新节点返回当作树根 
	{  
		root=newnode;
		return root;
	}
	else //若root不是树根，则建立二叉树 
	{  
		for(current=root;current!=NULL;) //current复制root，以保留当前的树根值 
		{  
			backup=current; //保留父节点 
			if(current->data > val)//比较树根节点和新节点数据 
				current=current->left;
			else
				current=current->right;
		}
		if(backup->data >val)//把新节点和树根连接起来 
			backup->left=newnode;
		else
			backup->right=newnode;
	}
	return root; //返回树指针 
}
void pre(btree ptr) //前序遍历 
{  
	if (ptr != NULL)
	{  
		cout<<"["<<setw(2)<<ptr->data<<"] ";
		pre(ptr->left);
		pre(ptr->right);
	}
}
void in(btree ptr) //中序遍历 
{  
	if (ptr != NULL)
	{  
		in(ptr->left);
		cout<<"["<<setw(2)<<ptr->data<<"] ";
		in(ptr->right);
	}
}
void post(btree ptr)//后序遍历
{  
	if (ptr != NULL)
	{  
		post(ptr->left);
		post(ptr->right);
		cout<<"["<<setw(2)<<ptr->data<<"] ";
	}
}
```
> 队列实现层序遍历

```
// 队列实现二叉树层序遍历

#include<iostream>
#include<queue>

using namespace std;

struct BinaryTree
{
	int val;
	BinaryTree *left;
	BinaryTree * right;
	BinaryTree(int data):val(data),left(nullptr),right(nullptr){}

};
//队列实现层序遍历
//
void prinTree(BinaryTree *arr[])
{
	queue<BinaryTree*> rel;//定义一个队列，数据类型是二叉树指针
	rel.push(arr[0]);
	while(!rel.empty())
	{
		BinaryTree* front = rel.front();
		cout<<front->val<<" ";
		rel.pop();
		if(front->left != nullptr)
			rel.push(front->left);
		if(front->right != nullptr)
		{
			rel.push(front->right);
		}



	}
}

}
int main()
{
	//构建二叉树
	BinaryTree* s_arr[6];
    s_arr[0] = new BinaryTree(0);
    s_arr[1] = new BinaryTree(1);
    s_arr[2] = new BinaryTree(2);
    s_arr[3] = new BinaryTree(3);
    s_arr[4] = new BinaryTree(4);
    s_arr[5] = new BinaryTree(5);
    s_arr[0]->left = s_arr[1];  //   0
    s_arr[0]->right = s_arr[2]; //  1  2
    s_arr[1]->left = s_arr[3];  // 3     5
    s_arr[3]->left = s_arr[4];  //4
    s_arr[2]->right = s_arr[5]; //所以层序遍历的结果为：0 1 2 3 5 4

    printTree(s_arr);
    delete [] s_arr;
    return 0;
	

}
```
## leetcode 98 
### description
> Given a binary tree, determine if it is a valid binary search tree (BST).

> Assume a BST is defined as follows:

> The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.

### Solution
> C++

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
// class Solution {
// public:
//     bool isValidBST(TreeNode* root) {
//         return isValidBST(root, NULL, NULL);
//     }

//     bool isValidBST(TreeNode* root, TreeNode* minNode, TreeNode* maxNode) {
//         if(!root) return true;
//         if(minNode && root->val <= minNode->val || maxNode && root->val >= maxNode->val)
//             return false;
//         return isValidBST(root->left, minNode, root) && isValidBST(root->right, root, maxNode);
// }
// }

class Solution
{
public:
    bool isValidBST(TreeNode* root)
    {
        if(root == NULL) return true;
        TreeNode* prev;
        return validate(root, prev);
    }
    
    bool validate(TreeNode* node, TreeNode *&prev)
    {
        if(node == NULL) return true;
        if(!validate(node->left, prev)) return false;
        if(prev!=NULL && prev->val > node->val) return false;
         
           prev = node;
           return (validate(node->right, prev));
    }
        
};
```