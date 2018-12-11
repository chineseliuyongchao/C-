```C
#include<stdlib.h>
#include<stdio.h>
typedef int datatype;
typedef struct link_node
{
	datatype info;
	struct link_node *next;
}node;
//建立一个空的单链表
node *init()
{
	return NULL;
}
//输出单链表中各个结点的值
void display(node *head)
{
	node *p;
	p = head;
	if (!p)printf("\n单链表是空的！");
	else
	{
		printf("\n单链表各个结点的值为：\n");
		while (p)
		{
			printf("%5d", p->info); 
			p = p->next;
		}
	}
}
//在单链表中查找第i个结点
node *find(node *head, int i)
{
	int j = 1;
	node *p = head;
	if (i < 1)
		return NULL;
	while (p&&i != j)
	{
		p = p->next;
		j++;
	}
	return p;
}
//在单链表中第i个结点后插入一个值为x的新结点
node *insert(node *head, datatype x, int i)
{
	node *p, *q;
	q = find(head, i);//查找i个结点
	if (!q&&i != 0)
		printf("\n找不到第%d个结点，不能插入%d！", i, x);
	else
	{
		p = (node*)malloc(sizeof(node));//分配空间
		p->info = x;//设置新结点
		if (i == 0)//插入的结点作为单链表的第一个结点
		{
			p->next = head;//插入
			head = p;
		}
		else
		{
			p->next = q->next;//插入
			q->next = p;
		}
	}
	return head;
}
//在单链表中删除一个值为x的结点
node *dele(node *head, datatype x)
{
	node *pre = NULL, *p;
	if (!head)
	{
		printf("单链表是空的！");
		return head;
	}
	p = head;
	while (p&&p->info != x)//没有找到并且没有找完
	{
		pre = p;//pre指向p的前驱结点
		p = p->next;
	}
	if (p)//找到了被删除结点
	{
		if (!pre)//要删除的是第一个结点
			head = head->next;
		else
			pre->next = p->next;
		free(p);
	}
	return head;
}
node *scan(node *p)//给链表里面输入数据
{
	node *q, *head;
	int i, j = 1, x;
	q = head = init();
	printf("请输入链表个数：");
	scanf("%d", &i);
	printf("\n请输入链表数据：");
	while (j <= i)
	{
		p = (node*)malloc(sizeof(node));
		scanf_s("%d", &x);
		p->info = x;
		p->next = init();
		if (j == 1)
		{
			head = p;
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
	node *p, *q;
	int i, x;
	q = p = init();
	q = scan(p);
	printf("\n请输入要查找的结点：");
	scanf("%d", &i);
	if (find(q, i))
	{
		printf("该结点值为：%d", find(q, i)->info);
	}
	else
	{
		printf("该结点不存在！\n");
	}
	printf("\n请输入要插入的结点位置：");
	scanf_s("%d", &i);
	printf("请输入该结点值：");
	scanf_s("%d", &x);
	q = insert(q, x, i);
	printf("结点插入后");
	display(q);
	printf("\n请输入要删除的结点值：");
	scanf_s("%d", &x);
	q = dele(q, x);
	printf("删除该结点后");
	display(q);
	printf("\n");
	return 0;
}
```
