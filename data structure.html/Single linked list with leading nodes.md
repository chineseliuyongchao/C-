```C
#include<stdio.h>
#include<stdlib.h>
typedef int datatype;
typedef struct link_node
{
	datatype info;
	struct link_node *next;
}node;
//建立一个空的带头结点的单链表
node *init()
{
	node *head;
	head = (node*)malloc(sizeof(node));
	head->next=NULL;
	return head;
}
//输出带头结点的单链表中各个结点的值
void display(node *head)
{
	node *p;
	p = head->next;//从第一个（实际）结点开始
	if (!p)
	{
		printf("\n带头结点的单链表是空的！");
	}
	else
	{
		printf("带头结点的单链表中各个结点的值为：\n");
		while(p)
		{
			printf("%5d", p->info);
			p = p->next;
		}
	}
}
//在带头结点的单链表中查找第i个结点
node *find(node *head, int i)
{
	int j = 0;
	node *p = head;
	if (i < 0)
	{
		printf("\n带头结点的单链表中不存在第%d个结点！", i);
		return NULL;
	}
	else if (i == 0)//此时p指向的是头结点
		return p;
	while (p&&i != j) //没有查找完并且还没有找到
	{
		p = p->next;//继续向后查找，计数器加一
		j++;
	}
	return p;//返回结果，i=0时，p指示的是头结点
}
//在带头结点的单链表中第i个结点后插入一个值为x的新结点
node *insert(node *head, datatype x, int i)
{
	node *p, *q;
	q = find(head, i);//查找带头结点的单链表中的第i个结点，i=0，表示新结点插入在头结点之后，此时q指向的是头结点
	if (!q)//没有找到
	{
		printf("\n带头结点的单链表中不存在第%d个结点！不能插入%d", i, x);
		return head;
	}
	p = (node*)malloc(sizeof(node));//为准备插入的新结点分配空间
	p->info = x;//为新结点设置值
	p->next = q->next;//插入
	q->next = p;//当i=0时，由于q指向的是头结点，本语句等价于head->next=p
	return head;
}
//在带头结点的单链表中删除一个值为x的结点
node *dele(node *head, datatype x)
{
	node *pre = head, *q;//首先pre指向头结点
	q = head->next;//q从带头结点的第一个实际结点开始找值为x的结点
	while (q&&q->info != x)//没有找完并且还没有找到
	{
		pre = q;//继续查找，pre指向q的前驱
		q = q->next;
	}
	if (q)
	{
		pre->next = q->next;//删除
		free(q);//释放空间
	}
	return head;
}
//给链表里面输入数据
node *scan(node *head)
{
	node *q,*p;
	int i, j = 1, x;
	printf("请输入链表个数：");
	scanf_s("%d", &i);
	printf("\n请输入链表数据：");
	while (j <= i)
	{
		p = (node*)malloc(sizeof(node));
		scanf_s("%d", &x);
		p->info = x;
		p->next = NULL;
		if (j == 1)
		{
			head->next = p;
			q = p;
		}
		else
		{
			q->next = p;
			q = p;
		}
		j++;
	}
	return head;
}
int main()
{
	node *init();
	node *head;
	int i, x;
	head = init();
	head = scan(head);
	printf("\n请输入要查找的结点：");
	scanf_s("%d", &i);
	if (find(head, i))
	{
		printf("该结点值为：%d", find(head, i)->info);
	}
	else
	{
		printf("该结点不存在！\n");
	}
	printf("\n请输入要插入的结点位置：");
	scanf_s("%d", &i);
	printf("请输入该结点值：");
	scanf_s("%d", &x);
	head = insert(head, x, i);
	printf("结点插入后");
	display(head);
	printf("\n请输入要删除的结点值：");
	scanf_s("%d", &x);
	head = dele(head, x);
	printf("删除该结点后");
	display(head);
	printf("\n");
	return 0;
}
```
