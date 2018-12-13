```C
#include<stdio.h>
#include<stdlib.h>
typedef struct node
{
	char data;
	struct node *next;
}linkstrnode;
typedef linkstrnode *linkstring;
//输出链式串
void strshow(linkstring *S)
{
	linkstrnode *p;
	p=*S;
	while(p)
	{
		printf("%c",p->data);
		p=p->next;
	}
}
//链式串的建立算法
void strcreate(linkstring *S)
{
	char ch;
	linkstrnode *p,*r;
	*S=NULL;//用r始终指向当前链式串的最后一个字符串对应的结点
	r=NULL;
	while((ch=getchar())!='\n')
	{
		p=(linkstrnode*)malloc(sizeof(linkstrnode));//产生新结点
		p->data=ch;
		if(*S==NULL)//新结点插入空表的情况
		{
			*S=p;
		}
		else//新结点插入非空表的情况
		{
			r->next=p;
		}
		r=p;//r移向当前链式串的最后一个字符的位置
	}
	if(r!=NULL)//处理表尾结点指针域
	{
		r->next=NULL;
	}
}
//链式串的插入算法
void strinsert(linkstring *S,int i,linkstring *T)
{
	int k;
	linkstring p,q;
	p=*S,k=1;
	while(p&&k<i-1)//用p查找S中第i-1个元素的位置
	{
		p=p->next;
	}
	if(!p)//第i-1个元素不存在，则出错
	{
		printf("想要插入的位置不存在");
	}
	else
	{
		q=*T;
		while(q&&q->next)//用q查找T中最后一个元素的位置
		{
			q=q->next;
		}
		q->next=p->next;//将T连接到S中的第i个位置上
		p->next=*T;
	}
}
//链式串的删除算法
void strdelete(linkstring *S,int i,int len)
{
	int k;
	linkstring p,q,r;
	p=*S,q=NULL,k=1;
	while(p&&k<i)
	{
		q=p;//用p查找S的第i个元素，q始终跟踪p的前驱
		p=p->next;
		k++;
	}
	if(!p)//S的第i个元素不存在，则出错
	{
		printf("想要删除的地方不存在");
	}
	else
	{
		k=1;
		while(k<len&&p)//p从第i个元素开始查找长度为len子串的最后元素
		{
			p=p->next;
			k++;
		}
		if(!p)//被删除的子串位于S的最前面
		{
			printf("error2");
		}
		else//被删除的子串位于S的中间或最后面的情形
		{
			if(!q)
			{
				r=*S;
				*S=p->next;
			}
			else
			{
				r=q->next;
				q->next=p->next;
			}
			p->next=NULL;
			while(r!=NULL)//回收被删除的子串所占用的空间 
			{
				p=r;r=r->next;
				free(p);
			}
		}
	}
}
//链式串的连接算法
void strconcat(linkstring *S1,linkstring *S2)
{
	linkstring p;
	if(!(*S1))//考虑穿S1为空串的情形
	{
		S1=S2;
		return;
	}
	else
	{
		if(S2)//S1和S2均不为空串的情形
		{
			p=*S1;//用p查找S1的最后一个字符的位置
			while(p->next)
			{
				p=p->next;
			}
			p->next=*S2;//将串S2连接到S1之后
		}
	}
}
//求链式子串的算法
linkstring substring(linkstring *S,int i,int len)
{
	int k;
	linkstring p,q,r,t;
	p=*S,k=1;
	while(p&&k<i)//用p查找S中的第i个字符
	{
		p=p->next;k++;
	}
	if(!p)
	{
		printf("第i个字符不存在");
		return NULL;
	}
	else
	{
		r=(linkstring)malloc(sizeof(linkstring));
		r->data=p->data;
		r->next=NULL;
		k=1;//用q始终指向子串的最后一个字符的位置
		q=r;
		while(p->next&&k<len)//取长度为len的子串
		{
			p=p->next;
			k++;
			t=(linkstring)malloc(sizeof(linkstring));
			t->data=p->data;
			q->next=t;
			q=t;
		}
		if(k<len)
		{
			printf("error");
		}
		else//处理子串的尾部
		{
			q->next=NULL;
			return r;
		}
	}
}
int main()
{
	int i,j,l=1;
	linkstring *asd,*p,*q;
	asd=(linkstring*)malloc(sizeof(linkstring));
	p=(linkstring*)malloc(sizeof(linkstring));
	printf("请输入主字符串");
	strcreate(asd);
	printf("*************************************************************************************\n");
	printf("*****链式串插入：1                           链式串删除：2                      *****\n");
	printf("*****链式串连接:3                            求链式串子串：4                    *****\n");
	printf("*****退出：5                                                                    *****\n");
	printf("*************************************************************************************\n");
	while(l==1)
	{
		printf("\n请输入要进行的指令");
		scanf("%d",&i);
		switch(i)
		{
		case 1:
			getchar();
			printf("请输入要插入的字符串:");
			strcreate(p);
			printf("请输入要插入的位置:");
			scanf("%d",&i);
			strinsert(asd,i,p);
			printf("操作以后的字符串是：");
			strshow(asd);
			break;
		case 2:
			printf("请输入要删除的位置");
			scanf("%d",&i);
			printf("请输入要删除的长度");
			scanf("%d",&j);
			strdelete(asd,i,j);
			printf("操作以后的字符串是：");
			strshow(asd);
			break;
		case 3:
			getchar();
			printf("请输入要连接的字符串");
			strcreate(p);
			strconcat(asd,p);
			printf("操作以后的字符串是：");
			strshow(asd);
			break;
		case 4:
			printf("请输入子串生成的位置");
			scanf("%d",&i);
			printf("请输入子串生成的长度");
			scanf("%d",&j);
			*p=substring(asd,i,j);
			printf("操作以后的字符串是：");
			strshow(p);
			break;
		case 5:
			l=0;
			break;
		}
	}
	return 0;
}
```
