* 第十四届中北大学ACM程序设计竞赛题
* 问题描述
** LYF是一个篮球高手，为了展现自己的篮球技艺，他总和学弟们打篮球，希望通过虐小菜鸡们获得满足感，长久以来终于引起了公愤。
** 为了制裁LYF，大家在暑假集训时进行了疯狂特训，如今已是今非昔比，现在的他们决定要选出他们中的绝对强者去制裁LYF，绝对强者要求：得分、篮板、助攻、抢断、封盖，五项数据都没有人比他高才行。你可以选出绝对强者吗？
* 输入描述
** 输入第一行包含整数 n （1 <= n <= 1000），表示人数。
** 接下来输入 n 行，每行 5 个数，分别表示得分、篮板、助攻、抢断、封盖的成绩。
* 输出描述
** 输出包含一行，如果存在绝对强者，输出绝对强者的编号，即输入顺序（编号从 1 开始），如果有多个绝对强者，输出编号最小的，如果不存在绝对强者，输出 "WO LYF MEI YOU KAI GUA !"（不输出引号）。
```C++
#include<iostream>
using namespace std;
void function1(int a[1000][6],int left,int right,int num){//通过快速排序按照某一种指标将队员排序 
	int i,j,b[6];
	if(left<right){
		i=left;
		j=right;
		b[0]=a[i][0];
		b[1]=a[i][1];
		b[2]=a[i][2];
		b[3]=a[i][3];
		b[4]=a[i][4];
		b[5]=a[i][5];
		while(i<j){
			while(i<j&&b[num]<=a[j][num]){
				j--;
			}
			if(i<j){
				a[i][0]=a[j][0];
				a[i][1]=a[j][1];
				a[i][2]=a[j][2];
				a[i][3]=a[j][3];
				a[i][4]=a[j][4];
				a[i][5]=a[j][5];
				i++;
			}
			while(i<j&&b[num]>a[i][num]){
				i++;
			}
			if(i<j){
				a[j][0]=a[i][0];
				a[j][1]=a[i][1];
				a[j][2]=a[i][2];
				a[j][3]=a[i][3];
				a[j][4]=a[i][4];
				a[j][5]=a[i][5];
			}
		}
		a[i][0]=b[0];
		a[i][1]=b[1];
		a[i][2]=b[2];
		a[i][3]=b[3];
		a[i][4]=b[4];
		a[i][5]=b[5];
		function1(a,left,i-1,num);
		function1(a,i+1,right,num);
	}
}
int function2(int a[1000][6],int n,int num){//按照某一种指标将指标值最大的人群中标号最小的找出来 
	int m=a[n][num],i;
	for(i=n;i>=0;i--){
		if(a[i][num]>a[i-1][num]){
			break;
		}
	}
	return i;
}
int function3(int a[1000][6],int num,int n){//判断当前队员是不是各项能力均最强 
	for(int i=0;i<n;i++){
		for(int j=1;j<=5;j++){
			if(a[num][j]<a[i][j]){
				return 0;
			}
		}
	}
	return 1;
}
int main(){
	int n,a[1000][6],left,right;//数组第一个值存放队员编号，后五个编号依次存放指标 
	cin>>n;
	for(int i=0;i<n;i++){
		a[i][0]=i+1;
		cin>>a[i][1]>>a[i][2]>>a[i][3]>>a[i][4]>>a[i][5];
	}
	left=0;
	right=n-1;
	for(int i=0;i<5;i++){
		function1(a,left,right,i+1);
		left=function2(a,n-1,i+1);
	}
	right=function3(a,left,n);
	if(right==0){
		cout<<"WO LYF MEI YOU KAI GUA !"<<endl;
	}
	else{
		cout<<a[left][0]<<endl;
	}
	return 0;
}
```
