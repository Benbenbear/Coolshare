选择排序(Selection sort)是一种简单直观的排序算法，它的工作过程如下。首先选出数组中最小（大）的元素，将它与数组中第一个元素进行交换，然后找出次小（大）的元素，并将它与数组中第二个元素交换，以此类推，直到整个数组排完序。因为它是通过不断选出剩余元素中最小（大）元素来实现的，之所以叫选择排序。     
对`n`个元素的表进行排序总共进行至多`n-1`次交换。在所有依靠交换去移动元素的排序方法中，选择排序算是非常好的一种。选择排序也有一个缺点，它的运行时间对文件中已经有序的部分依赖较少--从文件中选出最小元素的每一遍操作过程，并没有给出下一遍要找的最小元素的位置的相关信息。     
直接上源代码吧：
{% codeblock lang:c selection.c %}
/*
* File     : selection.c
* Author   : benbenbear                                                         
* Copyright: coolshare.pw
*/
#include <stdio.h>
#include <stdlib.h>

#define N 10

void exch(int *x, int *y);
void display(int a[], const int n);
void selection_sort(int* a, const int l, const int r);

int main(int argc, char *argv[])
{
  int a[N] = {9,17,23,7,4,8,12,0,11,6};
	int i;
	printf("The array before sorting: \n");
	display(a, N);
	
	selection_sort(a, 0, N);
	
	printf("The array after sorting: \n");
	display(a,N);

    return 0;
}


/* exchange two integers */
void exch(int *x, int *y)
{
	int temp;
	temp = *x;
	*x = *y;
	*y = temp;
}

/* print the array elements*/
void display(int a[], const int n)
{
	int i;
	for(i = 0; i < n; i++)
	{
		printf("%d ", a[i]);
	}
	printf("\n");
}

/* selection sort */
void selection_sort(int* a, const int l, const int r)
{
	int i, j, min;
	
	for(i = l; i < r; i++)
	{
		min = i;
		for(j = i+1; j < r; j++)
		{
			if(a[j] < a[min])
			{
				min = j;
			}
		}
		exch(&a[i],&a[min]);
	}
}
{% endcodeblock %}
下面是程序运行结果：
{% codeblock %}
[benbenbear@benbenbear selection]$ gcc -g selection.c -o hello 
[benbenbear@benbenbear selection]$ ./hello 
The array before sorting: 
9 17 23 7 4 8 12 0 11 6 
The array after sorting: 
0 4 6 7 8 9 11 12 17 23 
{% endcodeblock %}
OK,就到这儿了吧。下次继续！Good night！
