```C
#include<stdio.h>
#include<math.h>
int main(){
	int n,a[100][2],i,j,showtime[10][2],bi=0,than=1,thindspeed,peoplespeed,peoplevector[2],place[2];
	double time,thingtime,thinglength,peopletime,peoplelength,length1;
	while(than!=0){
		scanf("%d",&n);
		for(i=0;i<n;i++){
			scanf("%d%d",&a[100][0],&a[100][1]);
		}
		scanf("%d%d",&peoplevector[0],&peoplevector[1]);
		scanf("%d",&thingspeed);
		scanf("%d",&peoplespeed);
		scanf("%d",&than);
		i=0,j=1,thinglength=0,peoplelength=0,thingtime=0,peopletime=0;
		while(true){
			thinglength=sqrt((a[i][0]-a[j][0])*(a[i][0]-a[j][0])+(a[i][1]-a[j][1])*(a[i][1]-a[j][1]));
			peoplelength=sqrt((peoplevector[0]-a[j][0])*(peoplevector[0]-a[j][0])+(peoplevector[1]-a[j][1])*(peoplevector[1]-a[j][1]));
			i++;
			j++;
			if(i>=n){
				i-=n;
			}
			if(j>=n){
				j-=n;
			}
			thingtime+=thinglength/thingspeed;
			peopletime=peoplelength/peoplespeed;
			if(thingtime>peopletime){
				continue;
			}
			else if(thingtime==peopletime){
				showtime[bi][1]=(int)((thingtime%1)*60);
				showtime[bi][0]=(int)(thingtime);
				bi++;
			}
			else{
				if(a[i][0]==a[j][0]){
					place[0]=a[i][0];
					length1=fabs(a[i][1]-a[j][1]);
				}
				else{
					place[1]=a[i][1];
					length1=fabs(a[i][0]-a[j][0]);
				}
				
			}
		}
	}
}
```
