```C
#include<stdio.h>
#include<stdlib.h>
# define MAXSIZE 100
typedef struct
{
	char str[MAXSIZE];
	int length;
}seqstring;
//顺序串的插入算法
void strinsert(seqstring *S,int i,seqstring *T)
{
	int k;
	if(i<1||i>S->length+1||S->length+T->length>MAXSIZE)//非法情况的处理
	{
		printf("无法插入");
	}
	else
	{
		for(k=S->length-1;k>=i-1;k--)//S中从第i个元素开始后移
		{
			S->str[k+T->length]=S->str[k];
		}
		for(k=0;k<T->length;k++)//将T写入S中第i个字符开始的位置
		{
			S->str[k+i-1]=T->str[k];
		}
		S->length=S->length+T->length;
		S->str[S->length]='\0';//设置字符串S新的结束符
	}
}
//顺序串的删除算法
void strdelete(seqstring *S,int i,int len)
{
	int k;
	if(1<1||i>S->length||i+len-1>S->length)//非法情况的处理
	{
		printf("无法删除");
	}
	else
	{
		for(k=i+len-1;k<S->length;k++)//S中从下标为i+len-1开始的元素前移
		{
			S->str[k-len]=S->str[k];
		}
		S->length=S->length-len;
		S->str[S->length]='\0';//设置字符串S新的结束符
	}
}
//字符串的连接运算算法
seqstring *strconcat(seqstring *S1,seqstring *S2)
{
	int i;
	seqstring *r;
	if(S1->length+S2->length>MAXSIZE-1)//处理字符数组空间不够使用的情况
	{
		printf("无法连接");
		return NULL;
	}
	else
	{
		r=(seqstring*)malloc(sizeof(seqstring));
		for(i=0;i<S1->length;i++)//将S1复制到r字符数组的前端
		{
			r->str[i]=S1->str[i];
		}
		for(i=0;i<S2->length;i++)//将S2复制到r字符数组的后端
		{
			r->str[i+S1->length]=S2->str[i];
		}
		r->length=S1->length+S2->length;
		r->str[r->length]='\0';
	}
	return r;
}
//求字符串的子串的算法
seqstring *substring(seqstring *S,int i,int len)
{
	int k;
	seqstring *r;
	if(i<1||i>S->length||i+len-1>S->length)//处理非法情况
	{
		printf("无法操作");
		return NULL;
	}
	else
	{
		r=(seqstring*)malloc(sizeof(seqstring));
		for(k=0;k<len;k++)//复制子串到r的字符串数组中
		{
			r->str[k]=S->str[i+k-1];
		}
		r->length=len;
		r->str[r->length]='\0';
	}
	return r;
}
int main()
{
	int i,j,l=1;
	seqstring *asd,*p,*q;
	asd=(seqstring*)malloc(sizeof(seqstring));
	p=(seqstring*)malloc(sizeof(seqstring));
	q=(seqstring*)malloc(sizeof(seqstring));
	printf("请输入要输入字符串的长度");
	scanf("%d",&asd->length);
	getchar();
	printf("请输入主字符串");
	gets(asd->str);
	printf("*************************************************************************************\n");
	printf("*****顺序串插入：1                           顺序串删除：2                      *****\n");
	printf("*****顺序串连接:3                            求顺序串子串：4                    *****\n");
	printf("*****退出：5                                                                    *****\n");
	printf("*************************************************************************************\n");
	while(l==1)
	{
		printf("\n请输入要进行的指令");
		scanf("%d",&i);
		switch(i)
		{
		case 1:
			printf("请输入要输入字符串的长度");
			scanf("%d",&p->length);
			getchar();
			printf("请输入要插入的字符串:");
			gets(p->str);
			printf("请输入要插入的位置:");
			scanf("%d",&i);
			strinsert(asd,i,p);
			printf("操作以后的字符串是：");
			puts(asd->str);
			break;
		case 2:
			printf("请输入要删除的位置");
			scanf("%d",&i);
			printf("请输入要删除的长度");
			scanf("%d",&j);
			strdelete(asd,i,j);
			printf("操作以后的字符串是：");
			puts(asd->str);
			break;
		case 3:
			printf("请输入要连接的字符串的长度");
			scanf("%d",&p->length);
			getchar();
			printf("请输入要连接的字符串");
			gets(p->str);
			//puts(asd->str);
			q=strconcat(asd,p);
			printf("操作以后的字符串是：");
			puts(q->str);
			break;
		case 4:
			printf("请输入子串生成的位置");
			scanf("%d",&i);
			printf("请输入子串生成的长度");
			scanf("%d",&j);
			p=substring(asd,i,j);
			printf("操作以后的字符串是：");
			puts(p->str);
			break;
		case 5:
			l=0;
			break;
		}
	}
	return 0;
}
```
