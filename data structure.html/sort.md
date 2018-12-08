```C
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#define MAXSIZE 100
typedef struct
{
	char name[20];
	int xuehao;
	char phonenumber[20];
	char xueyuan[20];
	char zhuanye[20];
}node;
typedef struct
{
	node a[MAXSIZE+1];
	int len;
}table;
void init(table *s)
{
	s->len=0;
}
void creat(table *s,char *filename)
{
	int i,d;
	FILE *fp;
	fp=fopen(filename,"r");
	if(fp)
	{
		fscanf(fp,"%d",&s->len);
		for(i=1;i<=s->len;i++)
		{
			fscanf(fp,"%s%d%s%s%s",&s->a[i].name,&s->a[i].xuehao,&s->a[i].phonenumber,&s->a[i].xueyuan,&s->a[i].zhuanye);
		}
		fclose(fp);
	}
	else
	{
		s->len=0;
	}
}
void display(table *s)
{
	int i;
	printf("         姓名       学号          电话号          学院             专业\n");
	for(i=1;i<=s->len;i++)
	{
		printf("%15s%15d%15s%15s%15s\n",s->a[i].name,s->a[i].xuehao,s->a[i].phonenumber,s->a[i].xueyuan,s->a[i].zhuanye);
	}
}
table *quicksort(table *s,int left,int right)
{
	int i,j;
	if(left<right)
	{
		i=left;
		j=right;
		s->a[0]=s->a[i];
		do
		{
			while((s->a[j].xuehao>s->a[0].xuehao)&&i<j)
				j--;
			if(i<j)
			{
				s->a[i]=s->a[j];
				i++;
			}
			while((s->a[i].xuehao<s->a[0].xuehao)&&i<j)
				i++;
			if(i<j)
			{
				s->a[j]=s->a[i];
				j--;
			}
		}while(i!=j);
		s->a[i]=s->a[0];
		quicksort(s,left,i-1);
		quicksort(s,i+1,right);
	}
	return s;
}
node erfen(table *s,char xibiek[20])
{
	int low=1,high=s->len,mid;
	while(low<=high)
	{
		mid=(low+high)/2;
		if(strcmp(s->a[mid].zhuanye,xibiek)==0)
			printf("%15s%15d%15s%15s%15s\n",s->a[mid].name,s->a[mid].xuehao,s->a[mid].phonenumber,s->a[mid].xueyuan,s->a[mid].zhuanye);
		if(strcmp(s->a[mid].zhuanye,xibiek)==1)
			high=mid-1;
		else
			low=mid+1;
	}
}
void jiansuo(table *s,char xibiek[20])
{
	int i;
	printf("         姓名       学号          电话号          学院             专业\n");
	for(i=1;i<=s->len;i++)
	{
		if(strcmp(s->a[i].zhuanye,xibiek)==0)
			printf("%15s%15d%15s%15s%15s\n",s->a[i].name,s->a[i].xuehao,s->a[i].phonenumber,s->a[i].xueyuan,s->a[i].zhuanye);
	}
}
int main()
{
	table *s;
	char a[20],filename[20];
	int i=0;
	s=(table *)malloc(sizeof(table));
	init(s);
	printf("输入存放信息的文件名");
	gets(filename);
	creat(s,filename);
	printf("输入创建的学生借书证信息:\n");
	display(s);
	quicksort(s,1,s->len);
	printf("输出排序后的借书证信息:\n");
	display(s);
	printf("请输入检索的专业名(用第一种方法检索): ");
	scanf("%s",&a);
	erfen(s,a);
	printf("请输入检索的专业名(用第二种方法检索): ");
	scanf("%s",&a);
	jiansuo(s,a);
	return 0;
}
```
