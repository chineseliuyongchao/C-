```C
#include<stdio.h>
#include<stdlib.h>
#define MAXSIZE 100
typedef int datatype;
typedef struct 
{
	datatype a[MAXSIZE];
	int front;
	int rear;
}sequence_queue;
//队列初始化
void init(sequence_queue *sq)
{
	sq->front=sq->rear=0;
}
//判断队列是否为空
int empty(sequence_queue *sq)
{
	return(sq->front==sq->rear?1:0);
}
//打印队列的结点值
void diaplay(sequence_queue *sq)
{
	int i;
	if(empty(sq))
	{
		printf("\n队列是空的");
	}
	else
	{
		for(i=sq->front;i<sq->rear;i++);
		{
			printf("%5d",sq->a[i]);
		}
	}
}
//获得队列的队首结点值
datatype get(sequence_queue *sq)
{
	if(empty(sq))
	{
		printf("\n队列是空的，无法获得队首结点值");
		exit(1);
	}
	return sq->a[sq->front];
}
//队列的插入操作
void insert(sequence_queue *sq,datatype x)
{
	int i;
	if(sq->rear==MAXSIZE)
	{
		printf("\n队列是满的");
		exit(1);
	}
	sq->a[sq->rear]=x;
	sq->rear=sq->rear+1;
}
//队列的删除操作
void dele(sequence_queue *sq)
{
	if(sq->front==sq->rear)
	{
		printf("队列是空的");
		exit(1);
	}
	sq->front++;
}
//循环队列的插入操作
void insert_sequence_cqueue(sequence_queue *sq,datatype x)
{
	if((sq->rear+1)%MAXSIZE==sq->front)
	{
		printf("循环队列已经满了");
		exit(1);
	}
	sq->a[sq->rear]=x;
	sq->rear=(sq->rear+1)%MAXSIZE;
}
//循环队列的删除操作
void dele_sequence_cqueue(sequence_queue *sq)
{
	if(sq->front==sq->rear)
	{
		printf("循环队列是空的，没啥可删的");
		exit(1);
	}
	sq->front=(sq->front+1)%MAXSIZE;
}
```
