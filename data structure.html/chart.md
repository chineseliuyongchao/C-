```C
#include<stdio.h>
#include<stdlib.h>
#define M 20//预存图的最大定点数
int visited[M];
typedef char Datatype;
typedef struct node{
	int adjvex;//邻接点
	struct node *next;
}EdgeNode;//边表结点
typedef struct vnode{
	Datatype vertex;//顶点信息
	EdgeNode *FirstEdge;//邻接链表头指针
}VertexNode;//头结点类型
typedef struct{
	VertexNode adjlist[M];//存放头结点的顺序表
	int n,e;//图的顶点数与边数
}LinkedGraph;//邻接表类型
//图的创建
LinkedGraph *createadjgraph(LinkedGraph *g)
{
	int i,j,k;
	EdgeNode *p;
	printf("请输入图的顶点数和边数");
	scanf("%d%d",&g->n,&g->e);
	getchar();
	printf("请输入%d个顶点(无空格)",g->n);
	for(i=0;i<g->n;i++)
	{
		scanf("%c",&g->adjlist[i].vertex);//头结点
		g->adjlist[i].FirstEdge=NULL;//头结点的第一个边表结点
	}
	getchar();
	printf("请输入%d个边",g->e);
	for(k=0;k<g->e;k++)
	{
		scanf("%d%d",&i,&j);//输入无序对
		p=(EdgeNode*)malloc(sizeof(EdgeNode));
		p->adjvex=j;//邻接点序号为j
		p->next=g->adjlist[i].FirstEdge;//前插
		g->adjlist[i].FirstEdge=p;//将新结点*p插入顶点vi的边表结点头部
		p=(EdgeNode*)malloc(sizeof(EdgeNode));
		p->adjvex=i;
		p->next=g->adjlist[j].FirstEdge;//前插
		g->adjlist[j].FirstEdge=p;//将新结点*p插入顶点vi的边表结点头部
	}
	return g;
}
//图的深度优先遍历(邻接表表示法)
void dfs(LinkedGraph *g,int i)
{
	EdgeNode *p;
	printf("%c",g->adjlist[i].vertex);//访问结点
	visited[i]=1;
	p=g->adjlist[i].FirstEdge;
	while(p)//从*p的邻接表出发进行深度优先搜索
	{
		if(!visited[p->adjvex])
		{
			dfs(g,p->adjvex);
		}
		p=p->next;
	}
}
void DfsTraverse(LinkedGraph *g)
{
	int i;
	for(i=0;i<g->n;i++)
	{
		visited[i]=0;     //初始化标志数组
	}
	for(i=0;i<g->n;i++)
	{
		if(!visited[i])   //Vi从未访问过
		{
			dfs(g,i);
		}
	}
}
//图的广度优先遍历
void bfs(LinkedGraph *g,int i)
{
	int j;
	EdgeNode *p;
	int queue[M],rare=0,front=0;//队列
	printf("%c",g->adjlist[i].vertex);//访问顶点vi
	visited[i]=1;
	queue[rare++]=i;//将被访问过的结点入队
	while(rare>front)//判断队列是否为空
	{
		j=queue[front++];//出队
		p=g->adjlist[j].FirstEdge;
		while(p)//广度优先搜索邻接表
		{
			if(!visited[p->adjvex])
			{
				printf("%c",g->adjlist[p->adjvex].vertex);
				visited[p->adjvex]=1;
				queue[rare++]=p->adjvex;
			}
			p=p->next;
		}
	}
}
void BfsTraverse(LinkedGraph *g)
{
	int i,count=0;
	for(i=0;i<g->n;i++)
		visited[i]=0;      //初始化标志数组
	for(i=0;i<g->n;i++)
	{
		if(!visited[i])    //Vi未被访问过
		{
			count++;       //计数连通分量
			bfs(g,i);
		}
	}
}
int main()
{
	LinkedGraph *g,*m;
	g=(LinkedGraph*)malloc(sizeof(LinkedGraph));
	m=createadjgraph(g);
	printf("图的深度优先遍历(邻接表表示法)为：");
	DfsTraverse(m);
	printf("\n");
	printf("图的广度优先遍历(邻接表表示法)为：");
	BfsTraverse(m);
	printf("\n");
	return 0;
}
```
