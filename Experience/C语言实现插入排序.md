插入排序类似于人们在桥牌中使用的排序方法，每次只考虑一张牌，将牌插入已经排好了的序的适当位置中。工作流程如下：从第一个元素开始，依次取出下一个元素，在已经排序的元素序列中从后向前扫描，如果该元素大于新元素，将该元素大于新元素，将该元素移到下一位置，直到找到已排序的元素小于或者等于新元素的位置，将新元素插入到该位置后。    
直接上源代码吧：
``` c
/*
* File     : insertion.c
* Author   : benbenbear                                                         
* Copyright: coolshare.pw
*/
#include <stdio.h>
#include <stdlib.h>

#define N 10

void exch(int *x, int *y);
void display(int a[], const int n);
void insertion_sort(int* a, const int l, const int r);

int main(int argc, char *argv[])
{
  int a[N] = {9,17,23,7,4,8,12,0,11,6};
	int i;
	printf("The array before sorting: \n");
	display(a, N);
	
	insertion_sort(a, 0, N-1);
	
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

/* insertion sort */
void insertion_sort(int* a, const int l, const int r)
{
	int i, j;
	for(i = l+1; i <= r; i++)
	{
		for(j = i; j > 0; j--)
		{
			if(a[j] < a[j-1])
			{
				exch(&a[j], &a[j-1]);
			}
		}
	}
}
```
下面是程序的运行结果：
```
The array before sorting: 
9 17 23 7 4 8 12 0 11 6 
The array after sorting: 
0 4 6 7 8 9 11 12 17 23 
```
上面的插入排序实现是很直接，但不高效，我们对它稍作改进:  
(1) 首先将数组中最小的元素放在第一位，当作观察哨;  
(2) 在内部循环中，它只做一个简单赋值，而不执行交换操作;  
(3) 当元素插入到正确位置后就终止内部循环。  
``` c
void insertion_sort(int* a, const int l, const int r)
{
	int i;
	for(i = r; i > 0; i--)
	{
		if(a[i] < a[i-1])
		{
			exch(&a[i],&a[i-1]);
		}
	}
	for(i = l+2; i <= r; i++)
	{
		int j = i;
		int v = a[i];
		while((v < a[j-1]))
		{
			a[j] = a[j-1];
			j--;
		}
		a[j] = v;
	}
}
```
改进后的插入排序比之前的效率要高，几乎是两倍的效率。和选择排序不同的是，插入排序的运行时间和输入文件数据的原始排列顺序密切相关。    
OK, Good Luck!!!
