```C
#include<stdio.h>
#include<stdlib.h>
#define MAXSIZE 100
typedef int datatype;
typedef struct{
	datatype a[MAXSIZE];
	int top;
}sequence_stack;
//栈的初始化
void init(sequence_stack *st)
{
	st->top=0;
}
//判断栈是否为空
int empty(sequence_stack *st)
{
	return(st->top?0:1);
}
//取得栈顶结点值
datatype read(sequence_stack *st)
{
	if(empty(st))
	{
		printf("\n栈是空的!");
		exit(1);
	}
	else
	{
		return st->a[st->top-1];
	}
}
//栈的插入操作
void push(sequence_stack *st,datatype x)
{
	if(st->top==MAXSIZE)
	{
		printf("栈已经满了");
		exit(1);
	}
	else
	{
		st->a[st->top]=x;
		st->top++;
	}
}
//栈的删除操作
void pop(sequence_stack *st)
{
	if(st->top==0)
	{
		printf("栈已经空了");
		exit(1);
	}
	else
	{
		st->top--;
	}
}
```
