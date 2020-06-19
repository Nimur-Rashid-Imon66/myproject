#include<stdio.h>
#include<string.h>
#include<conio.h>
char filepathlog[100]="lofinINFO.txt";
int enterchoice()
{
    int choice;
    printf("**************************************************");
    system("color 05");
    printf("\n\n\n\t\t");
    printf("WELCOME TO IIUC TRANSPORTS ");
    printf("\n\t1.Log in .");
    printf("\n\t2.Registration .");
    printf("\n\t3.Complain .");
    printf("\n\t4.Help .");
    printf("\n\t5.Update my Information .");
    printf("\n\t6. Admin .\n");
    printf("**************************************************");
    printf("\n\tEnter your choice : ");
    scanf("%d",&choice);
    return choice;
}



struct login
{
    char number[15],password[50],name[20];

};


struct mainFile
{
    int serial;
    char Number[15],Name[20],Gender[8],position[10],location[100],Password[50];
};



void error()
{
    printf("File openning error\n Please try again or contact distributor\n\n");
}




int welcome(char n[])
{
    int choice;
    system("cls");
    system("color 09");
    printf("\n\n\n\t\tWelcome %s\n",n);
    printf("\t\tWhere are you now ?\n\t\t1.IIUC Campus\n\t\t2.At your location\n\t\t3.New location\n");
    printf("Enter your Choice : ");
    scanf("%d",&choice);
    switch(choice)
    {
    case 1 :
        IIUC();
        break;
    case 2:
        my_location();
        break;
    case 3:
        new_location();
    }
}



void IIUC()
{

    int h,m;
    char AmPm[3];

     system("cls");
    printf("\n\n\n\t\t");
    printf("Enter time(hh:mm AM/Pm) : ");
    scanf("%d:%d%s",&h,&m,&AmPm);
    printf("\n\t\tOh it's %d:%d %s",h,m,AmPm);


}



void my_location()
{
}



void new_location()
{

}




void login()
{
    struct login entry[10000];
    char ch,num[15],pass[50];
    int i,noc,cmp;
    FILE *loginINFO ;


    i=0;
    loginINFO=fopen(filepathlog,"r");
    if(!loginINFO)
    {
        error();
        return;
    }
    while(fscanf(loginINFO,"%s",&entry[i].number)==1)
    {
        fscanf(loginINFO,"%s%s",&entry[i].password,&entry[i].name);
        i++;
    }
    fclose(loginINFO);
    noc=i;

    system("cls");
    system("color 01");
    printf("\n\n\n\t\tEnter your Number : ");
    scanf("%s",num);
start :
    printf("\n\t\tEnten your password : ");

    while(1)
    {
        ch=getch();
        if(ch==13)
        {
            pass[i]='\0';
            break;
        }
        else if(ch=='\b')
        {
            i--;
            printf("\b \b");

        }
        else if(ch=='\t'||ch==' ')
        {
            continue ;
        }
        else
        {
            pass[i]=ch;
            i++;
            printf("*");
        }
    }

    for(i=0; i<noc; i++)
    {
        if(strcmp(num,entry[i].number)==0)
        {
            if(strcmp(pass,entry[i].password)==0)
                welcome(entry[i].name);
            else
            {
                printf("Wrong password.Try again.");
                goto start;
            }

        }
    }


}





void registration()
{
    system("cls");
    system("color 0A");
    FILE *registry ;
    struct mainFile New;
    char ConPass[50], ch;
    int i=0;
printf("\n\n\n\t\tStep 1\n");
    printf("Enter your Name : ");
    scanf("%s",New.Name);
    printf("Enter your Gender (Male/Female) : ");
    scanf("%s",New.Gender);
    printf("Enter your position in IIUC(Student,Teacher,Staff,Newcomer) : ");
    scanf("%s",New.position);
   printf("Enter your location which one is nearest at your home : ");
    ///suggested location
   // printf("dew");
   scanf("%s",New.location);
    if(strcmp(New.Gender,"Male")==0)
    {
        char filepath[100]="male.txt" ;
        registry=fopen(filepath,"a");
    }
    else if(strcmp(New.Gender,"Female")==0)
    {
        char filepath[100]="Female.txt" ;
        registry=fopen(filepath,"a");
    }
    printf("Press Enter Bar Go to next Step .");
    getch();
    system("cls");
    system("color 0A");
    printf("\n\n\n\t\tStep 2\n");
    printf("Enter your Mobile Number : ");
    scanf("%s",New.Number);
    printf("Enter a Password :");
    while(1)
    {
        ch=getch();
        if(ch==13)
        {
            ConPass[i]='\0';
            break;
        }
        else if(ch=='\b')
        {
            i--;
            printf("\b \b");

        }
        else if(ch=='\t'||ch==' ')
        {
            continue ;
        }
        else
        {
           ConPass[i]=ch;
            i++;
            printf("*");
        }
    }

    start :
        printf("\n");
        i=0;
    printf("Confirm your password : ");
    while(1)
    {
        ch=getch();
        if(ch==13)
        {
            New.Password[i]='\0';
            break;
        }
        else if(ch=='\b')
        {
            i--;
            printf("\b \b");

        }
        else if(ch=='\t'||ch==' ')
        {
            continue ;
        }
        else
        {
           New.Password[i]=ch;
            i++;
            printf("*");
        }
    }
    if(strcmp(New.Password,ConPass)==0)
    {
         fprintf(registry,"%s\n%s %s\n%s\n%s\n%s\n",New.Name,New.Gender,New.position,New.Number,New.location,New.Password);
    }

    else
    {
       printf("\n!Password not match .Try again the right one .");
        goto start ;
    }

 printf("\n\n****************** Registration Complete ******************\n");


}




void complain()
{

}






void help()
{

}



void updateMyInfo()
{

}



void admin()
{

}


int main()
{
    int choice;
    choice=enterchoice();
    switch(choice)
    {
    case 1:
        login();
        break;
    case 2:
        registration();
        break;
    case 3:
        complain();
        break;
    case 4:
        help();
        break;
    case 5:
        updateMyInfo();
        break;
    case 6:
        admin();
        break;

    }
    return 0;
}
