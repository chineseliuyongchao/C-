## 树的双亲表示法
```C
#define MAXSIZE 100//树中结点个数的最大值
typedef char datatype;//结点值的类型
typedef struct node//结点的类型
{
	datatype data;
	int parent;//结点双亲的下标
}node;
typedef struct tree
{
	node treelist[MAXSIZE];//存放结点的数组
	int length,root;//树中实际所含的结点个数及根结点的位置
}tree;//树的类型
```
## 树的孩子表示法
```C
#define m 3//树的度数
typedef char datatype;//结点值的类型
typedef struct node//结点的类型
{
	datatype data;
	struct node *child[m];//指向子女的指针数组
}node,*tree;
tree root;
```
## 树的孩子表示法（数组方式）
```C
# define m 3//树的度数
#define MAXSIZE 20//存放树结点的数组大小
typedef char datatype;//树中结点值的类型
typedef struct node//树中结点的类型
{
	datatype data;
	int child[m];
}treenode;
treenode tree[MAXSIZE];//存储树结点的数组
int root;//根结点的下标
int length;//树中实际所含结点的个数
```
## 树的孩子表示法
```C
#define MAXSIZE 50
typedef char datatype;
typedef struct chnode//孩子结点的类型
{
	int child;
	struct chnode *next;
}chnode,*chpoint;
typedef struct//树中每个结点的类型
{
	datatype data;
	chpoint firstchild;//指向第1个子女结点的指针
}node;
typedef struct//树的类型
{
	node treelist[MAXSIZE];
	int length,root;//树中实际所包含结点的个数和根结点的位置
}tree;
```
## 孩子兄弟表示法
```C
typedef char datatype;//树中结点值的类型
typedef struct node//树中每个结点的类型
{
	datatype data;
	struct node *firstchild,*rightchild;
}node,*pnode;
pnode root;//指向树根结点的指针
```
## 树的遍历
#include<stdio.h>
#include<stdlib.h>
//树的孩子表示法
#define m 3//树的度数
typedef char datatype;//结点值的类型
typedef struct node//结点的类型
{
	datatype data;
	struct node *child[m];//指向子女的指针数组
}node,*tree;
tree root;
//树的前序遍历算法
void preorder(tree p)//P为指向树根结点的指针
{
	int i;
	if(p!=NULL)//树不为空
	{
		printf("%c",p->data);//输出根结点的值
		for(i=0;i<m;i++)//依次递归实现各子树的前序遍历
		{
			preorder(p->child[i]);
		}
	}
}
//树的后序遍历算法
void postorder(tree p)//p为指向树根节点的指针
{
	int i;
	if(p!=NULL)//树不为空
	{
		for(i=0;i<m;i++)//依次递归实现各子树的后序遍历
		{
			postorder(p->child[i]);
		}
		printf("%c",p->data);//输出根结点的值
	}
}
//按前序遍历顺序建立一棵3度树
tree createtee()
{
	int i;
	char ch;
	tree t;
	if((ch=getchar())=='#')
	{
		t=NULL;
	}
	else
	{
		t=(tree)malloc(sizeof(node));
		t->data=ch;
		for(i=0;i<m;i++)
		{
			t->child[i]=createtee();
		}
	}
	return t;
}
//树的层次遍历算法
void levelorder(tree t)//t为指向树根结点的指针
{
	tree queue[100];//存放等待访问的结点队列
	int f,r,i;//f，r分别为队头，队尾指针
	tree p;
	f=0;
	r=1;
	queue[0]=t;
	while(f<r)//队列不为空
	{
		p=queue[f];//访问队头元素
		f++;
		printf("%c",p->data);
		for(i=0;i<m;i++)//将刚被访问的元素是所有子女结点依次进队
		{
			if(p->child[i])
			{
				queue[r]=p->child[i];
				r++;
			}
		}
	}
}
