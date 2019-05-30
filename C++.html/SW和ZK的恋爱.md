* 第十四届中北大学ACM程序设计竞赛
* 问题描述
** SW和ZK是一对令人羡慕的神仙眷侣，他们之间总是充满着甜蜜如初恋的感觉。当然，再幸福的恋爱，也难免少不了磕磕绊绊，吵闹是青春朦胧情感的调味剂。
** 在他们恋爱的第1314天，SW买了一个蛋糕，他深情对ZK说：“I　LOVE　YOU　1314 ！”，ZK十分感动，却又开始了自怜自艾，
** ZK说：“你永远想象不到我有多么爱你，比你爱我还有多3000倍！”。SW立刻就不乐意了，觉得自己的爱要更多一点。直男的脾气来了，SW说：“我爱你是你爱我的 N 倍！”
** ZK立刻回击：“我的爱是你的 N + 1 倍！”SW又说：“我的爱是你的 N 倍后面至少还有 K 个 0 ！”ZK说：“亲爱的，你真好 ！”
** 可是问题来了，假设ZK的爱是一个整数 N，那么最小的正整数是 N 的倍数且至少以 K 个 0 结尾的这个数是多少？
* 输入描述
** 包含一行输入两个整数 N（1 <= N <= 1000000000），K（0 <= K <= 8）。
* 输出描述
** 输出包含一个正整数，表示答案。
```C++
#include<iostream>
using namespace std;
int main(){
	long long int n,k,num1=1,num2,num3;
	cin>>n>>k;
	for(int i=0;i<k;i++){
		num1*=10;
	}
	if(num1>=n){
		num2=n;
	}
	else{
		num2=num1;
		num1=n;
	}
	n=num1;
	k=num2;
	while((num1/num2)*num2!=num1){
		num3=num1%num2;
		num1=num2;
		num2=num3;
	}
	num1=(n*k)/num2;
	cout<<num1<<endl;
	return 0;
}
```
