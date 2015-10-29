# Develop-a-program-that-performs-some-basic-file-operations
#copy, interleave , more, grep , wordcount
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int main(int argc, char * argv[])
  {//declaration of all buffers and variables 
char ch,*ch1;
FILE *from,*to,*from1;
FILE *from2,*fp,*fp1 ;
char line1[256]={};
char line2[256]={};
int end1=0,end2=0,end=0,i;
char line3[256]={0};
int count =0;
char choice;
char line[256]={};
char search[10]={};
int x = atoi(argv[1]);
int ch2;
int j=0;
int c=0,count1=0;
char a[10000]={};
char buf[101] = {0};
char line_val[101] = {0};
  int line_len = 101;
  int line_num = -1;
  int cur_line = 1;
  char buff[101] = {0};
  char shortline[101]={0};
  int wordcount=0;
  int wc = 31;
  int wordlen=0;
  int wl[3]= {0};
  char word[31]={0};
  int k=0,p=0;
  long size;
  char longword[3][30];
if (x>4 || x<0)//to check for exceptions
{printf("Usage: wrong choice \n");
exit(0);
}
//from = fopen(argv[2], "r"); 
switch (x)//switch case for the different options 
{

case 0:// copy one file to the other
from = fopen(argv[2], "r");// check for empty file 
if(from==NULL){printf("no file exists");exit(0);}
to = fopen(argv[3], "w");
if(to==NULL){printf("no file exists");exit(0);}
if (argc != 4)
  { printf("Usage: executable input_file output_file\n");
    exit(0);
  }

while (fscanf(from, "%c", &ch) != EOF)
  { fprintf(to, "%c", ch);
    //printf("%c", ch);
  }
  fclose(from);
  fclose(to);
   break;

   
case 1://interleave one file with the other
if (argc != 5)// if enough aguments are not defined
  { printf("Usage: executable input_file output_file\n");
    exit(0);
  }
  from = fopen(argv[2], "r");
  from1=fopen(argv[3],"r");
  to = fopen(argv[4], "w");
if(from==NULL){printf("no file exists");exit (0);}
  if(from1==NULL){printf("no file exists");exit (0);}

while (end != 2) {
   ch1 =  fgets(line1, 256, from);
    if (ch1 != NULL) {
      fprintf(to, "%s", line1);
    } else if (ch1 == NULL) {
      end1 = 1;
    }

   ch1 =  fgets(line2, 256, from1);
    if (ch1 != NULL) {
      fprintf(to, "%s", line2);
    } else if (ch1 == NULL) {
      end2 = 1;
    }
    end = end1 + end2;
  }
  fclose(from);
  fclose(from1);
  fclose(to);
break;



case 2:// more command that prints first ten lines then asks for option
if (argc != 3)
  { printf("Usage: executable input_file output_file\n");
    exit(0);
  }

from = fopen(argv[2], "r");
if(from==NULL){printf("no file exists");exit(0);}
while (fscanf(from, "%c", &ch) != EOF)
{if(count<10)
 printf("%c",ch);
if (ch=='\n')
count=count++;
 if(count==10)
	break;
}
while(1)
{printf("enter the choice you would like to make");
scanf("%c",&choice);
if(choice=='n')
{ch1=fgets(line1,256,from);
printf("%s \n ",line1);
if(ch1==NULL)
	return(0);
}
else if(choice=='p')
{for(i=0;i<10;i++)
	{ch1=fgets(line1,256,from);
	if(ch1!=NULL)
	printf("%s \n",line1);
else
	return 0;
    }
}
else if(choice=='q')
return 0;
}
fclose(from);
break; 



case 3:// grep command to search for a word in a line 
if (argc != 3)
  { printf("Usage: executable input_file output_file\n");
    exit(0);
  }
if(from==NULL){printf("no file exists");exit (0);}
from = fopen(argv[2], "r");
count =0;
printf("enter the search term in the file");
scanf("%s",search);
while (fgets(line , sizeof(line) ,from )!= NULL)
   {
      if (strstr(line, search)!= NULL)// the following function compares each str2 in str1 and returns either the pointer to the first occurance of str2 or a null if it does not exist
      {
         printf("%s",line);
      }
   }
   fclose(from);
   break;
case 4:// word count 
if (argc != 3)
  { printf("Usage: executable input_file output_file\n");
    exit(0);
  }
from2 = fopen(argv[2], "r");
if(from2==NULL){printf("no file exists");exit(0);}
i=0;
do{
ch2=fgetc(from2);
// to count the number of sentences 
if (ch2=='\n')
c++;
a[i]=ch2;
// to count the number of words 
if (!((a[i]>='0' && a[i]<='9')||(a[i]>='a' && a[i]<='z')||(a[i]>='A' && a[i]<='Z'))&&((a[i-1]>='0' && a[i-1]<='9')||(a[i-1]>='a' && a[i-1]<='z')||(a[i-1]>='A' && a[i-1]<='Z')))
{
	count1++;
			}
i++;}while(ch2!=EOF);
// to count the number of characters in a file
size=ftell(from2);
printf("the number of characters is %ld \n",size);
printf("the number of lines is %d \n",c);
printf("the number of words is %d \n",count1);
fclose(from2);

fp= fopen(argv[2], "r"); ;

if(fp==NULL){printf("no file exists");exit(0);}
  while(fgets(buf, 101, fp) != NULL) {
    int len_tmp = strlen(buf) - 1;

    if(buf[len_tmp] == '\n')
      buf[len_tmp]='\0';

    if(len_tmp<line_len) {// checking for line length in terms of number of characters, the shortest one is stored in line_temp
      strncpy(line_val, buf, len_tmp + 1);
      line_len = len_tmp;
      line_num = cur_line;
    }

    cur_line++;
  }
printf("the shortest line:( %d ) %s \n ",line_len,line_val);
fclose(fp); 
//  FILE *fp1;
 // fp1= from;
  fp1=fopen(argv[2], "r");
  if(fp1==NULL){printf("no file exists");exit(0);}
  while((fgets(buff, 101, fp1)) != NULL) // to store each line into a buffer
  {int len_tmp = strlen(buff) - 1;
   	do{
			word[p]=buff[k];// to obtain each word in a line 
		if (!((buff[k]>='0' && buff[k]<='9')||(buff[k]>='a' && buff[k]<='z')||(buff[k]>='A' && buff[k]<='Z'))&&((buff[k-1]>='0' && buff[k-1]<='9')||(buff[k-1]>='a' && buff[k-1]<='z')||(buff[k-1]>='A' && buff[k-1]<='Z')))
	    {wordcount++;// to count the number of words in each line 
	    word[p]='\0';
		wordlen=p;
        p=0;// reinitializing the word buffer 
            if(wordlen>wl[0])// to select the three longest words in a file 
		{  wl[2]=wl[1];
	       strcpy(longword[2],longword[1]);
		   wl[1]=wl[0];
	       strcpy(longword[1],longword[0]);
	       wl[0]=wordlen;
	       strcpy(longword[0],word);
	       //printf("0%s",longword[0]);
		 }
		else if(wordlen<=wl[0] && wordlen>wl[1])
		{  wl[2]=wl[1];
	       strcpy((longword[2]),(longword[1]));
	       wl[1]=wordlen;
		   strcpy((longword[1]),word);
		   //printf("1%s",longword[1]);
		}
	else if(wordlen<=wl[1] && wordlen>wl[2])
		{ wl[2]=wordlen;
		  strcpy((longword[2]),word);
		  //printf("2%s",longword[2]);
		
		}	
		}
		else 
			p++;
k++;
    }while(k<strlen(buff));//operating on each character of the line 
	
 if(buff[len_tmp] == '\n')
 buff[len_tmp]='\0';
if (wordcount<wc)
{wc=wordcount;
strncpy(shortline,buff,len_tmp+ 1);// obtaining the shortest lines in terms of number of words  
}
k=0;
wordcount=0;
  }      
 printf("the shortest line:( %d ) %s \n ",wc,shortline);
 // printing the longest three words in the file
printf("The top three longest words are :%s , %s , %s. ",(longword[0]),longword[1],longword[2]);
 fclose(fp1);  
 
break;
} // end of switch case
 
//fclose(from);
 return 0;

}


