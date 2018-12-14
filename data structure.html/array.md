```C
#include<stdio.h>
#include<stdlib.h>
typedef int datatype;//假设数组元素的值为整型
typedef struct 
{
	datatype *base;//数组存储区的首地址指针
	int index[3];//存放三维数组各维的长度
	int c[3];//存放三维数组各维的Ci值
}array;
//数组初始化运算算法
 int init(array *A,int b1,int b2,int b3)
 {
	 int elements;
	 if(b1<0||b2<0||b3<0)//处理非法情况
	 {
		 printf("输入的数字不符合条件");
	 }
	 A->index[0]=b1;
	 A->index[1]=b2;
	 A->index[2]=b3;
	 elements=b1*b2*b3;//求数组元素的个数
	 A->base=(datatype*)malloc(elements*sizeof(datatype));//为数组分配空间
	 if(!(A->base))
	 {
		 return 0;
	 }
	 A->c[0]=b2*b3;
	 A->c[1]=b3;
	 A->c[2]=1;
	 return(1);
 }
 //访问数组元素值的运算算法
 int value(array A,int i1,int i2,int i3,datatype x)
 {
	 int off;
	 if(i1<0||i1>=A.index[0]||i2<0||i2>=A.index[1]||i3<0||i3>=A.index[2])//处理下标非法的情况
	 {
		 return 0;
	 }
	 off=i1*A.c[0]+i2*A.c[1]+i3*A.c[2];//计算数组元素的位移
	 x=*(A.base+off);//赋值
	 return x;
 }
 //数组元素的赋值运算算法
 int assign(array *A,datatype e,int i1,int i2,int i3)
 {
	 int off;
	 if(i1<0||i1>=A->index[0]||i2<0||i2>=A->index[1]||i3<0||i3>=A->index[2])//处理下标非法的情况
	 {
		 return 0;
	 }
	 off=i1*A->c[0]+i2*A->c[1]+i3*A->c[2];//计算数组元素的位移
	 *(A->base+off)=e;//赋值
	 return 1;
 }
 int main()
 {
	 int i,j,k,x,y,z,op;
	 datatype num;
	 array *asd;
	 asd=(array*)malloc(sizeof(array));
	 printf("即将初始化数组，请分别输入三维数组的三维长度");
	 scanf("%d%d%d",&i,&j,&k);
	 op=init(asd,i,j,k);
	 for(x=0;x<i;x++)
	 {
		 for(y=0;y<j;y++)
		 {
			 for(z=0;z<k;z++)
			 {
				 printf("请输入数组的元素");
				 scanf("%d",&num);
				 assign(asd,num,x,y,z);
			 }
		 }
	 }
	 printf("操作后的数组为：\n");
	 for(x=0;x<i;x++)
	 {
		 for(y=0;y<j;y++)
		 {
			 for(z=0;z<k;z++)
			 {
				 num=value(*asd,x,y,z,num);
				 printf("%d\t",num);
			 }
			 printf("\n");
		 }
		 printf("\n\n");
	 }
	 return 0;
 }
 ```
