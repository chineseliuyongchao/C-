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
