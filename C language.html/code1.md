```C
#include<stdio.h>
#include<conio.h>
#include<time.h>
#include<string.h>
#include<stdlib.h>
#define MAXSTU 30;
void PassWord()//密码验证函数声明
{
	int i=1;
	char password[10]={0};//存放用户输入的密码
	char truepassword[10]={'4','3','9','9'};//存放真实密码
	printf("请输入密码");
	while(i==1)//判断密码是否正确，如果不正确，让用户重新输入
	{
		gets(password);//用户输入密码
		if(strcmp(password,truepassword)==0)
		{
			printf("密码正确");
			i=0;
		}
		else
		{
			printf("您输入的密码错误，请重新输入");
		}
	}
}
void MainMenu()//主菜单函数声明
{
	system("cls");//将输出框清空
	printf("\t\t|------------------------------------------|\n");
	printf("\t\t|             学生成绩统计系               |\n");
	printf("\t\t|------------------------------------------|\n");
	printf("\t\t|             1---录入学生成绩             |\n");
	printf("\t\t|             2---显示学生成绩             |\n");
	printf("\t\t|             3---统计总分和平均分         |\n");
	printf("\t\t|             4---统计最高分和最低分       |\n");
	printf("\t\t|             5---统计各分段人数           |\n");
	printf("\t\t|             0---退出                     |\n");
	printf("\t\t|------------------------------------------|\n");
}
int InputScore(int score[])//录入学生成绩函数声明
{
	int len=1;
	system("cls");
	printf("\t\t----------------录入学生成绩----------------\n");
	printf("\t\t请输入学生成绩<输入-1退出,满分为一百>\n");
	while(1==1)//让用户输入学生的成绩,如果输入-1，循环停止，并且记录学生个数
	{
		printf("\t\t第%d个学生的成绩：",len);
		scanf("%d",&score[len-1]);
		if(score[len-1]==-1)
		{
			break;
		}
		len++;
	}
	getchar();
	printf("\t\t按任意键返回菜单");
	getch();//实现按任意键退出
	return len-1;
}
void DisplayScore(int score[],int n)//显示学生成绩函数声明
{
	int i;
	system("cls");
	printf("\t\t----------------显示学生成绩----------------\n");
	printf("\t\t学生成绩显示如下：\n");
	printf("\t\t学生序号      序号\n");
	for(i=0;i<n;i++)//输出所有学生的成绩
	{
		printf("\t\t%5d%12d\n",i+1,score[i]);
	}
	getchar();
	printf("\t\t按任意键返回菜单");
	getch();
}
void SumAvgScore(int score[],int n)//统计课程总分和平均分函数声明
{
	int num1=0,i;
	float num2;
	system("cls");
	printf("\t\t--------------统计总分和平均分--------------\n");
	for(i=0;i<n;i++)//计算课程总分
	{
		num1+=score[i];
	}
	num2=((float)num1)/n;//计算课程平均分
	printf("\t\t课程的总分为%d，平均分为%f\n",num1,num2);//输出课程总分和平均分
	getchar();
	printf("\t\t按任意键返回菜单");
	getch();
}
void MaxMinScore(int score[],int n)//统计课程最高分和最低分函数声明
{
	int num1,num2,i;
	system("cls");
	printf("\t\t--------------统计最高分和最低分------------\n");
	num1=score[0];//让最高分暂时等于第一个学生的成绩
	num2=score[0];//让最高低暂时等于第一个学生的成绩
	for(i=0;i<n;i++)//计算出最高分
	{
		if(num1<score[i])
		{
			num1=score[i];
		}
	}
	for(i=0;i<n;i++)//计算出最低分
	{
		if(num2>score[i])
		{
			num2=score[i];
		}
	}
	printf("\t\t课程的最高分为%d，最低分为%d\n",num1,num2);//输出最高分和最低分
	getchar();
	printf("\t\t按任意键返回菜单");
	getch();
}
void GradeScore(int score[],int n)//统计课程各分段人数函数声明
{
	int num=0,i;
	system("cls");
	printf("\t\t--------------统计各分数段的人数------------\n");
	for(i=0;i<n;i++)//计算满分的人数
	{
		if(score[i]==100)
		{
			num++;
		}
	}
	printf("\t\t考满分的学生为%d个\n",num);//输出满分的人数
	num=0;
	for(i=0;i<n;i++)//统计优秀的人数
	{
		if(score[i]<100&&score[i]>=80)
		{
			num++;
		}
	}
	printf("\t\t优秀的学生为%d个\n",num);//输出优秀的人数
	num=0;
	for(i=0;i<n;i++)//统计及格的人数
	{
		if(score[i]<80&&score[i]>=60)
		{
			num++;
		}
	}
	printf("\t\t考及格的学生为%d个\n",num);//输出及格的人数
	num=0;
	for(i=0;i<n;i++)//统计不及格的人数
	{
		if(score[i]<60)
		{
			num++;
		}
	}
	printf("\t\t考不及格的学生为%d个\n",num);//输出不及格的人数
	getchar();
	printf("\t\t按任意键返回菜单");
	getch();
}
int main()
{
	int stu_score[30];
	int stu_count=0;
	int choose;
	int then=1;
	PassWord();//验证用户输入的密码
	while(then==1)
	{
		MainMenu();
		printf("\t\t 请选择主菜单序号（0—5）：");
		scanf("%d",&choose);//接受用户输入的数字用来判断执行什么操作
		switch(choose)//判断用户想要执行什么操作
		{
		case 1:
			stu_count=InputScore(stu_score);
			break;
		case 2:
			DisplayScore(stu_score,stu_count);
			break;
		case 3:
			SumAvgScore(stu_score,stu_count);
			break;
		case 4:
			MaxMinScore(stu_score,stu_count);
			break;
		case 5:
			GradeScore(stu_score,stu_count);
			break;
		case 0:
			then=0;
			break;
		}
	}
	return 0;
}
```
