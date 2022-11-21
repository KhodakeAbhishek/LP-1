CPU SCHEDULING

#include<stdio.h>
#include<conio.h>
#include<stdlib.h>

void fcfs()
{
    int p[10],bt[10],tt[10],tat[10];
    int wt[10],sum,i,no;
    int awt,att,at=0,gc[10]; 
    printf("\nEnter the no of process:-");
    scanf("%d",&no);
    for(i=0;i<no;i++)
    {
        printf("\nEnter burst time of the process p%d:-",i);
        scanf("%d",&bt[i]);
    }
    gc[0]=0;
    for(i=1;i<=no;i++)
    {
        gc[i]=gc[i-1]+bt[i-1];
    }   
    for(i=0;i<no;i++)
    {
        wt[i]=gc[i]-at;
    }

//Gantt chart of FIFO

    printf("\n\n Gantt chart:");
    printf("\n \n");
    for(i=0;i<no;i++)
    {
        printf("|p%d",i);
    }
    printf("|");
    printf("\n \n");
    
    for(i=0;i<=no;i++)
    {
        printf("%d ",gc[i]);
    }
    printf("\n\nProcess BurstTime WaitingTime TurnAroundTime");
    for(i=0;i<no;i++)
    {
        printf("\n p%d\t %d\t\t %d\t\t %d",i,bt[i],wt[i],gc[i+1]);
    }
    sum=0;
    for(i=0;i<no;i++)
    {
        sum=sum+wt[i];
    }
    awt=sum/no;
    printf("\nAverage Waitingn Time=:%d",awt);
    sum=0;
    for(i=1;i<=no;i++)
    {
        sum=sum+gc[i];
    }
    att=sum/no;
    printf("\nAverage Waitingn Time=:%d",att);
}

//Function of SJF
void sjf()
{
    int bt[10],i,j,wt[10],ft[10],temp,temp_id,p[10],st[10],tt[10];
    int no; int wat=0,att=0;
    printf("\nEnter the no of process:-");
    scanf("%d",&no);
    for(i=1;i<=no;i++)
    {
        printf("\nEnter the process id:-");
        scanf("%d",&p[i]);
    }
    for(i=1;i<=no;i++)
    {
        printf("\nEnter burst time of the process :-");
        scanf("%d",&bt[i]);
    }
    for(j=1;j<=no-1;j++)
    {
        if(bt[j+1]<bt[j])
        {
            temp=bt[j]; 
            bt[j]=bt[j+1];
            bt[j+1]=temp;
            temp_id=p[j]; 
            p[j]=p[j+1];
            p[j+1]=temp_id;
        }
    }
    printf("\n\n Gantt chart:");
    for(i=1;i<=no;i++)
    {
        printf("\np%d\t%d",p[i],bt[i]);
    }
    for(i=1;i<=no;i++)
    { 
        if(i==1)
        {
            st[i]=0;
            ft[i]=bt[i];
        }
        else
        {
            st[i]=st[i-1]+bt[i-1];
            ft[i]=st[i]+bt[i];
        }
    }
    printf("\n\n BurstTime WaitingTime TurnAroundTime");
    for(i=1;i<=no;i++)
    {
        wt[i]=st[i];
    }
    for(i=1;i<=no;i++)
    {    
        tt[i]=ft[i];
    }
    for(i=1;i<=no;i++)
    {
        printf("\n %d\t\t %d\t\t%d",bt[i],wt[i],tt[i]);
    }
    printf("\n \n");

//Average waiting time

    for(i=1;i<=no;i++)
    {
        wat=wat+wt[i];
    }
    wat=wat/no;
    printf("\n\nAverage waitng time:-%d",wat);

// Average turn around time

    printf("\n\n Average turn around time :- ");
    for(i=1;i<=no;i++)
    {
        att=att+tt[i];
    }
    att=att/no;
    printf("%d",att);
}

void priority()
{
    int bt[10],i,j,wt[10],ft[10],temp,temp_id,p[10],st[10],tt[10];
    int no,pr[10],temp_p;
    int wat=0,att=0;
    printf("\nEnter the no of process:-");
    scanf("%d",&no); for(i=1;i<=no;i++)
    {
        printf("\nEnter the process id:-");
        scanf("%d",&p[i]);
    }
    for(i=1;i<=no;i++)
    {
        printf("\nEnter burst time of the process :-");
        scanf("%d",&bt[i]);
    }
    for(i=1;i<=no;i++)
    {
        printf("\nEnter priority of the process:- ");
        scanf("%d",&pr[i]);
    }
    for(j=1;j<=no-1;j++)
    {
        if(pr[j+1]<pr[j])
        {
            temp_p=pr[j];
            pr[j]=pr[j+1];  
            pr[j+1]=temp_p;
            temp=bt[j];
            bt[j]=bt[j+1];
            bt[j+1]=temp;
            temp_id=p[j]; 
            p[j]=p[j+1];
            p[j+1]=temp_id;
        }
    }

//Gantt chart

    printf("\n\nGantt chart:"); for(i=1;i<=no;i++)
    {
        printf("\np%d\t%d\t%d",p[i],bt[i],pr[i]);
    }
    for(i=1;i<=no;i++)
    {
        if(i==1)
        {
            st[i]=0;    
            ft[i]=bt[i];
        }
        else
        {
            st[i]=st[i-1]+bt[i-1]; 
            ft[i]=st[i]+bt[i];
        }
    }
    printf("\n\n BurstTime WaitingTime TurnAroundTime");
    for(i=1;i<=no;i++)
    {
        wt[i]=st[i];
    }
    for(i=1;i<=no;i++)
    {
        tt[i]=ft[i];
    }
    for(i=1;i<=no;i++)
    {
        printf("\n %d\t\t%d\t\t%d",bt[i],wt[i],tt[i]);
    }
    printf("\n ");
    
//Average waiting time

    for(i=1;i<=no;i++)
    {
        wat=wat+wt[i];
    }
    wat=wat/no;
    printf("\n\nAverage waitng time:-%d",wat);

// Average turn around time

    printf("\n\n Average turn around time :- ");
    for(i=1;i<=no;i++)
    {
        att=att+tt[i];
    }
    att=att/no;
    printf("%d",att);
}

// Function of Round Robin

void round_robin()
{
    int arr[20],awt[10],no,ch;
    int tat[30],pro[30],rr[30],pro1[30],bt[30],flag[15],
    flag1[20],gc[20]; 
    int i,j,k,at,sum,tq,rnd_up,a=0;
    float avg,temp;
    at=sum=temp=0;
    printf("\n\nEnter the number of procceses u want :");
    scanf("%d",&no); 
    printf("\nEnter the time quantum :"); 
    scanf("%d",&tq);
    
//------------Enter process burst time-----------

    for(i=0;i<no;i++)
    {
        printf("\nEnter the process number ,burst time :");
        scanf("%d%d",&pro[i],&arr[i]);
        flag[i]=flag1[i]=gc[i]=0;
        bt[i]=arr[i]; 
        if(temp<=arr[i]) 
            temp=arr[i];
    }
    temp=temp/tq;
    k=0;
    rr[k]=0;
    for(i=0;i<rnd_up;i++)
    {
        for(j=0;j<no;j++) 
        {       
            if(arr[j]!=0)
            {
                if(arr[j]>=tq)
                {
                    rr[++k]=tq;
                    pro1[k-1]=pro[j];
                    arr[j]=arr[j]-tq;
                }
                else
                {
                    rr[++k]=arr[j];
                    pro1[k-1]=pro[j];
                    arr[j]=0;
                }   
            }
        }
    }
    for(i=1;i<=k;i++)
    {
        arr[i]=arr[i-1]+rr[i];
    }
    printf("\n\tGANTT CHART");
    printf("\n \n");
    for(i=0;i<k;i++)
    {
        printf("| P%d",pro1[i]);
    }
    printf("|");
    printf("\n \n");
    for(i=0;i<=k;i++) 
    {
        printf("%d",arr[i]);
    }    
    for(i=0;i<no;i++)
    {
        a=i; 
        gc[i]=gc[i]+arr[a];
        for(j=i+1;j<k;j++)
        {
            if(pro1[j]==pro1[i])
            {
                gc[i]=gc[i]+arr[j]-arr[a+1];
                a=j;
                flag[i]=1;
            }   
        }
        tat[i]=arr[a+1];
        a=0;
    }

    for(i=0;i<no;i++)
    {
        if(flag[i]==0)
        {
            gc[i]=arr[i];
        }
    }
    printf("\n\nProcess\tBurst time\tWaiting time\t\tTurn Around Time");
    for(i=0;i<no;i++)
    {
        printf("\nP%d\t%d\t\t%d\t\t%d",pro[i],bt[i],gc[i],tat[i]);
    }
//---------Average Waiting Time-------
    sum=0;
    for(i=0;i<no;i++)
    {
        sum=sum+gc[i];
    }
    avg=sum/no;
    printf("\n\nAverage Waiting Time :%3.2f",avg);
//--------Average Turn Around Time-------
    sum=0;
    for(i=0;i<no;i++)
    {
        sum=sum+tat[i];
    }
    avg=sum/no;

    printf("\n\nThe Average Turn Around Time :%3.2f",avg);
}

// Main Function
int main()
{
    int ch;
    char ans;
// clrscr(); 
do
{
    printf("\n****MENU****** ");    
    printf("\n1.FCFS"); 
    printf("\n2.SJF");
    printf("\n3.PRIORITY");
    printf("\n4.ROUND ROBIN");
    printf("\n5.Exit");
    printf("\nEnter ur choice:-"); 
    scanf("%d",&ch);
    
    switch(ch)
    {
        case 1:
        fcfs();
        break;
        case 2:
        sjf();
        break;
        case 3:
        priority();
        break;
        case 4:
        round_robin();
        break;
        case 5:
        exit(0);
        break;
        default:
        break;
    }
    printf("\n\n Do u wann continue?");
    scanf("%c",&ans);
}
while(ans=='y');
getch();

}
