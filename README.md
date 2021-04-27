# 2021-04-27
字符串训练

1、编程比较用户键盘输入的口令与内设的口令secret是否相同。若相同，则输出"Correct password! Welcome to the system...\n"，若userInput>password则输出"Invalid password!user input>password\n"，否则输出"Invalid password!user input<password\n"。
输入提示信息："Input Password:"
输入格式："%s"
输出提示信息：
"Correct password! Welcome to the system...\n"
"Invalid password!user input<password\n"
"Invalid password!user input>password\n"

我的答案：
#include <stdio.h>
#include <string.h>
#define STR_LEN 100

int main(int argc,char const*argv[])
{
	char *pass = "secret";
	char str[STR_LEN+1];
	printf("Input Password:");
	scanf("%s",str);
	if (strcmp(pass,str) == 0)
	{
		printf("Correct password! Welcome to the system...\n");
	}
	else if (strcmp(pass,str) > 0)
	{
		printf("Invalid password!user input<password\n");
	}
	else
	{
		printf("Invalid password!user input>password\n");
	}
	return 0;	
}

总结：向函数中传递指针只需传递地址。

2、从键盘输入一个字符串a，将字符串a复制到字符串b中，再输出字符串b，即编程实现字符串处理函数strcpy()的功能，但要求不能使用字符串处理函数strcpy()。
**输入提示信息："Input a string:"
**输入格式要求：用gets()输入字符串
**输出格式要求："The copy is:"
程序的运行示例如下：
Input a string:Hello China
The copy is:Hello China

我的答案：
#include <stdio.h>
#include <string.h>
#define STR_LEN 100

int main(int argc,char const*argv[])
{
	char s1[STR_LEN+1];
	char s2[STR_LEN+1];
	printf("Input a string:");
	gets(s1);
	
	int i;
	for (i=0 ; s1[i]!='\0' ; i++)
	{
		s2[i] = s1[i];
	}
	printf("The copy is:");
	puts(s2);
	
	return 0;	
}

3、
采用冒泡法进行升序排序。
基本原理是：对数组中的n个数执行n-1遍检查操作，在每一遍执行时，对数组中剩余的尚未排好序的元素进行如下操作：对相邻的两个元素进行比较，若排在后面的数小于排在前面的数，则交换其位置，这样每一遍操作中都将参与比较的数中的最大的数沉到数组的底部，经过n-1遍操作后将全部n个数按从小到大的顺序排好序。
要求限制数组元素最大个数为10。

程序的某次运行结果如下：
Input n:5↙
Input 5 numbers:21 32 45 12 0↙
Sorting results:   0  12  21  32  45（换行）

输入格式:"%d"
输入数据个数提示："Input n:"
输入数据提示："Input %d numbers:"
输出提示："Sorting results:"
输出数据格式:"%4d"

我的答案：
#include<stdio.h>

void BubbleSort(int a[],int n);

int main(int argc,char const*argv[])
{
	int n,i;
	int a[10];
	
	printf("Input n:");
	scanf("%d",&n);
	
	printf("Input %d numbers:",n);
	for (i=0 ; i<n ; i++)
	{
		scanf("%d",&a[i]);
	}
	
	BubbleSort(a,n);
	
	printf("Sorting results:");
	for (i=0 ; i<n ; i++)
	{
		printf("%4d",a[i]);
	}
	putchar('\n');
	return 0;	
}

void BubbleSort(int a[],int n)
{
	int i,j,temp;
	for (i=0 ; i<n-1 ; i++)
	{
		for (j=n-1 ; j>i ; j--)
		{
			if (a[j] < a[j-1])
			{
				temp = a[j];
				a[j] = a[j-1];
				a[j-1] = temp;
			}
		}
	}	
}

总结：注意输入数据的方法，scanf在遇到空白字符时就会跳过，直到读取下一个字符。

4、下面的函数MyStrcmp()用于实现字符串比较并返回较大字符串的功能，将两个字符串s和t进行比较，
要求将两个字符串中第一个不相同字符的ASCII码值之差与较大的字符串作为MyStrcmp()函数的返回值。
其中差值用return返回，函数的第三个参数用来存储较大的字符串，也是一种返回方式。找出其中错误并改正之。
#include <stdio.h>
int MyStrcmp(char s[], char t[], char bigger[]);
int main()
{
    char  str1[20], str2[20], str3[20];
    int diff;
    printf("Input string:");
    gets(str1);
    printf("Input another string:");
    gets(str2);
    diff = MyStrcmp(str1[20], str2[20], str3[20]);  
    printf("The bigger string is:%d\n", str3);       
    printf("The differ of the strings is:%d\n", diff);
    return 0;
}
 
int MyStrcmp(char s[], char t[], char bigger[])
{
    int i, result = 0;
    int len1 = 0, len2 = 0;
    while (s[len1++] != '\0');
    while (t[len2++] != '\0');
    for (i = 0; s[i] = t[i]; i++); 
    if (i=0 || s[i] != '\0' ) 
        result = t[i] - s[i];  
    if (result >= 0)
        for (i = 0; i < len1; i++)
            bigger[i] = s[i];
    else
        for (i = 0; i < len2; i++)
            bigger[i] = t[i];
    return result;
}

我的答案：
#include <stdio.h>
int MyStrcmp(char s[], char t[], char bigger[]);
int main()
{
    char  str1[20], str2[20], str3[20];
    int diff;
    printf("Input string:");
    gets(str1);
    printf("Input another string:");
    gets(str2);
    diff = MyStrcmp(str1, str2, str3);  
    printf("The bigger string is:%s\n", str3);       
    printf("The differ of the strings is:%d\n", diff);
    return 0;
}
 
int MyStrcmp(char s[], char t[], char bigger[])
{
    int i, result = 0;
    int len1 = 0, len2 = 0;
    while (s[len1++] != '\0');
    while (t[len2++] != '\0');
    for (i = 0; s[i] == t[i]; i++); 
    if (i==0 || s[i] != '\0' ) 
    {    result = s[i] - t[i];  
    if (result >= 0)
        for (i = 0; i < len1; i++)
            bigger[i] = s[i];
    else
        for (i = 0; i < len2; i++)
            bigger[i] = t[i];
    }
	else
	{	result = 0 - t[i];
		for (i = 0; i < len2; i++)
            bigger[i] = t[i];
    }
	return result;
}

标准答案：
#include <stdio.h>
int MyStrcmp(char s[], char t[], char bigger[]);
int main()
{          
    char  str1[20], str2[20], str3[20];
    int diff;
    printf("Input string:");
    gets(str1);
    printf("Input another string:");
    gets(str2);
    diff = MyStrcmp(str1, str2, str3); //1
    printf("The bigger string is:%s\n", str3); //1
    printf("The differ of the strings is:%d\n", diff);
    return 0;
}          
 
int MyStrcmp(char s[], char t[], char bigger[])
{          
    int i, result = 0;
    int len1 = 0, len2 = 0;
    while (s[len1++] != '\0');
    while (t[len2++] != '\0');
    for (i = 0;  s[i] == t[i] && s[i] != '\0' && t[i]!='\0'; i++); //1
    if (i==0 || s[i - 1] != '\0' ) //1
        result = s[i] - t[i]; //1
    if (result >= 0)
        for (i = 0; i < len1; i++)
            bigger[i] = s[i];
    else
        for (i = 0; i < len2; i++)
            bigger[i] = t[i];
    return result;
}
总结：
·while (s[len1++] != '\0');
 while (t[len2++] != '\0');
这两句用来统计字符串长度，不包含结尾的'\0'
·分开返回的思想
