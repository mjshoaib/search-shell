# search-shell
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<string.h>
char *buff,*t1,*t2,*t3,*t4,ch;
FILE *fp;
int pid;

void search(char *t2,char *t3,char *t4)
{
    int i=1,count=0;
    char *p;

    if((fp=fopen(t4,"r"))==NULL)
        printf("File not found\n");
    else
    {
        if(strcmp(t2,"f")==0)
        {
            while(fgets(buff,80,fp))
            {
                if((strstr(buff,t3))!=NULL)
                {
                    printf("%d: %s\n",i,buff);
                    break;
                }
            }
            i++;
        }
        else if(strcmp(t2,"c")==0)
        {
            while(fgets(buff,80,fp))
            {
                if((strstr(buff,t3))!=NULL)
                {
                    count++;
                    
                }
                
            }
            printf("No of occurences of %s= %d\n",t3,count);
            
        }
        else if(strcmp(t2,"a")==0)
        {
            while(fgets(buff,80,fp))
            {
                if((strstr(buff,t3))!=NULL)
                {
                    printf("%d: %s\n",i,buff);
                    
                }
                i++;
                
            }
            
        }
        else
        printf("Command not found\n");
        fclose(fp);
        
    }
    
}

main()
{
    while(1)
    {
        printf("myshell$");
        fflush(stdin);
        t1=(char *)malloc(80);
        t2=(char *)malloc(80);
        t3=(char *)malloc(80);
        t4=(char *)malloc(80);
        buff=(char *)malloc(80);
        fgets(buff,80,stdin);
        sscanf(buff,"%s %s %s %s",t1,t2,t3,t4);
        if(strcmp(t1,"pause")==0)
            exit(0);
        else if(strcmp(t1,"search")==0)
            search(t2,t3,t4);
        else
        {
            pid=fork();
            if(pid<0)
                printf("Child process is not created\n");
            else if(pid==0)
            {
                execlp("/bin",NULL);
                if(strcmp(t1,"exit")==0)
                    exit(0);
                    system(buff);
            }
            else
            {
                wait(NULL);
                exit(0);
                
            }
            
        }
        
    }
    
}
