## 稀疏矩阵的顺序存储及其实现
```C
#include<stdio.h>
#include<stdlib.h>
typedef struct
{
	int data[100][100];
	int m,n;
}matrix;
typedef int spmatrix[100][3];
//产生稀疏矩阵的三元组表示
void compressmatrix(matrix A,spmatrix B)//将稀疏矩阵转换成其三元组表示
{
	int i,j,k=1;
	for(i=0;i<A.m;i++)
	{
		for(j=0;j<A.n;j++)
		{
			if(A.data[i][j]!=0)//产生非零元素的三元组表示
			{
				B[k][0]=i;
				B[k][1]=j;
				B[k][2]=A.data[i][j];
				k++;
			}
		}
	}
	B[0][0]=A.m;//三元组数组中第i行存放稀疏矩阵行数，列数和非0元素的个数
	B[0][1]=A.n;
	B[0][2]=k-1;
}
//产生稀疏矩阵的三元组表示
void transpmatrix(spmatrix B,spmatrix C)//实现稀疏矩阵的转置
{
	int i,j,t,m,n;
	int x[100];//该数组用来存放B中每一列非零元素的个数
	int y[100];//该数组用来存放C中每一行非零三元组的起始位置
	m=B[0][0];
	n=B[0][1];
	t=B[0][1];
	C[0][0]=n;
	C[0][1]=m;
	C[0][2]=t;
	if(t>0)
	{
		for(i-0;i<n;i++)//初始化数组
		{
			x[i]=0;
		}
		for(i=1;i<=t;i++)//统计B中每一行非零元素的个数
		{
			x[B[i][1]]=x[B[i][1]]+1;
		}//求矩阵C中每一行非零元素三元组的起始位置
		y[0]=1;
		for(i=1;i<n;i++)
		{
			y[i]=y[i-1]+x[i-1];
		}
		for(i=1;i<=t;i++)
		{//将B中非零元素交换行号，列号后写入C中其最终的位置上
			j=y[B[i][1]];
			C[j][0]=B[i][1];
			C[j][1]=B[i][0];
			C[j][2]=B[i][2];
			y[B[i][1]]=j+1;
		}
	}
}
```
## 稀疏矩阵及顺序存储优化
```C
#include<stdio.h>
#include<stdlib.h>
typedef struct
{
	int data[100][100];
	int m,n;
}matrix;
typedef int spmatrix[100][3];
//产生稀疏矩阵的三元组表示
void compressmatrix(matrix A,spmatrix B)//将稀疏矩阵转换成其三元组表示
{
	int i,j,k=1;
	for(i=0;i<A.m;i++)
	{
		for(j=0;j<A.n;j++)
		{
			if(A.data[i][j]!=0)//产生非零元素的三元组表示
			{
				B[k][0]=i;
				B[k][1]=j;
				B[k][2]=A.data[i][j];
				k++;
			}
		}
	}
	B[0][0]=A.m;//三元组数组中第i行存放稀疏矩阵行数，列数和非0元素的个数
	B[0][1]=A.n;
	B[0][2]=k-1;
}
void transpmatrix(spmatrix B,spmatrix C)//实现稀疏矩阵的转置
{
	int i,j,t;
	t=B[0][2];
	C[0][0]=B[0][1];
	C[0][1]=B[0][0];
	C[0][2]=t;
	for(i=1;i<=t;i++)
	{//将B中非零元素交换行号，列号后写入C中其最终的位置上
		C[i][0]=B[i][1];
		C[i][1]=B[i][0];
		C[i][2]=B[i][2];
	}
}
int main()
{
	int i,j;
	matrix *asd;
	spmatrix gh;
	spmatrix zxc;
	asd=(matrix*)malloc(sizeof(matrix));
	printf("请输入数组的行数和列数（小于100）");
	scanf("%d%d",&asd->m,&asd->n);
	for(i=0;i<asd->m;i++)
	{
		for(j=0;j<asd->n;j++)
		{
			printf("请输入第%d行，第%d列的数据",i+1,j+1);
			scanf("%d",&asd->data[i][j]);
		}
	}
	printf("输入的稀疏矩阵是：\n");
	for(i=0;i<asd->m;i++)
	{
		for(j=0;j<asd->n;j++)
		{
			printf("%9d",asd->data[i][j]);
		}
		printf("\n");
	}
	compressmatrix(*asd,zxc);
	printf("转换为三元组表以后的矩阵：\n");
	for(i=0;i<=zxc[0][2];i++)
	{
		for(j=0;j<3;j++)
		{
			printf("%9d",zxc[i][j]);
		}
		printf("\n");
	}
	transpmatrix(zxc,gh);
	printf("转置以后的矩阵：\n");
	for(i=0;i<=gh[0][2];i++)
	{
		for(j=0;j<3;j++)
		{
			printf("%9d",gh[i][j]);
		}
		printf("\n");
	}
	return 0;
}
```
## C语言声明要放在主函数最前面
## C语言声明要放在主函数最前面
## C语言声明要放在主函数最前面


