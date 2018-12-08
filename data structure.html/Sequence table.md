```C
#include<stdio.h>
#include<stdlib.h>
#define MAXSIZE 100
typedef int datatype;
typedef struct{
	datatype a[MAXSIZE];
	int size;
}sequence_list;
//顺序表的初始化
void init(sequence_list *sit)
{
	sit->size=0;
}
//在顺序表后部进行插入操作
void append(sequence_list *sit,datatype x)
{
	if(sit->size==MAXSIZE)
	{
		printf("顺序表已经满了");
		exit(1);
	}
	sit->a[sit->size]=x;
	sit->size=sit->size+1;
}
//打印顺序表的各结点值
void display(sequence_list *sit)
{
	int i;
	if(sit->size==0){
		printf("顺序表是空的");
	}
	for(i=0;i<sit->size;i++)
	{
		printf("%5d",sit->a[i]);
	}
}
//判断顺序表是否为空
int empty(sequence_list *sit)
{
	return(sit->size==0?1:0);
}
//查找顺序表中值为x的结点位置
int find(sequence_list *sit,datatype x)
{
	int i=0;
	while(i<sit->size&&sit->a[i]!=x)
	{
		i++;
	}
	return(i<sit->size?i+1:-1);
}
//取得顺序表中第i个结点的值
datatype get(sequence_list *sit,int i)
{
	if(i<0||i>=sit->size)
	{
		printf("指定位置的结点不存在");
		exit(1);
	}
	else
	{
		return sit->a[i-1];
	}
}
//在顺序表的position位置插入值为x的结点
void insert(sequence_list *sit,datatype x,int position)
{
	int i;
	if(sit->size==MAXSIZE)
	{
		printf("顺序表是满的，无法输入");
		exit(1);
	}
	if(position<0||position>sit->size)
	{
		printf("指定的位置不存在");
		exit(1);
	}
	for(i=sit->size;i>=position;i--)
	{
		sit->a[i]=sit->a[i-1];
	}
	sit->a[position-1]=x;
	sit->size++;
}
//删除顺序表中第position位置的结点
void dele(sequence_list *sit,int position)
{
	int i;
	if(sit->size==0)
	{
		printf("顺序表是空的");
		exit(1);
	}
	if(position<0||position>=sit->size)
	{
		printf("想要删除的位置不存在");
		exit(1);
	}
	for(i=position-1;i<sit->size;i++)
	{
		sit->a[i]=sit->a[i+1];
	}
	sit->size--;
}
//主函数
int main()
{
	int i,j,l=1,k;
	sequence_list *sit;
	sit=(sequence_list*)malloc(sizeof(sequence_list));
	init(sit);
	printf("请输入要创建的顺序表的长度");
	scanf("%d",&sit->size);
	printf("请输入要创建的顺序表的%d个数据",sit->size);
	for(i=0;i<sit->size;i++)
	{
		scanf("%d",&sit->a[i]);
	}
	printf("*************************************************************************************\n");
	printf("*****在顺序表后部进行插入：1                 打印顺序表的各结点值：2            *****\n");
	printf("*****查找顺序表中指为x的结点位置:3           取得顺序表中第i个结点的值：4       *****\n");
	printf("*****在顺序表的position位置插入值为x的结点：5删除顺序表中第position位置的结点：6*****\n");
	printf("*****退出：7                                                                    *****\n");
	printf("*************************************************************************************\n");
	while(l==1)
	{
		printf("\n请输入要进行的指令");
		scanf("%d",&i);
		switch(i)
		{
		case 1:
			printf("请输入要插入的数据");
			scanf("%d",&j);
			append(sit,j);
			display(sit);
			break;
		case 2:
			display(sit);
			break;
		case 3:
			printf("请输入要查找的结点的值");
			scanf("%d",&k);
			j=find(sit,k);
			printf("该结点的位置是%d",j);
			break;
		case 4:
			printf("请输入要查找的结点的位置");
			scanf("%d",&j);
			k=get(sit,j);
			printf("该结点的值是%d",k);
			break;
		case 5:
			printf("请输入要插入的结点值和位置");
			scanf("%d%d",&k,&j);
			insert(sit,k,j);
			display(sit);
			break;
		case 6:
			printf("请输入要删除的结点位置");
			scanf("%d",&j);
			dele(sit,j);
			display(sit);
			break;
		case 7:
			l=0;
		}
	}
	return 0;
}
```
