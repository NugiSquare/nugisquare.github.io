#no.180

#include <stdio.h>

typedef struct node
{
	int content;
	*node parent;
	*node left;
	*node right;
}

int init(*node nd, int input, *node pt, *node lf, *node rg)
{
	nd = (node *)malloc(sizeof(node));
	nd->content = input;
	nd->parent = pt;
	nd->left = lf;
	nd->right = rg;
}

int main(void)
{
	int count, i, tmp_input;
	*node root, tmp_node;
	scanf("%d", &count);
	for(i=0; i<count; i++)
	{
		scanf("%d", &tmp_input);
		if(i == 0)
		{
			init(root, tmp_input, NULL, NULL, NULL);
			tmp_node = root;
		}
		else
		{

		}
	}
}

#no.1348

    Background

    3차원 좌표평면 상에 n개의 점이 주어진다.

    각 점을 입력받아서 원하는 기준으로 정렬하여 출력하는 프로그램을 작성하시오.
    Input

    첫 번째 줄에 점의 수 n이 입력된다.
    두 번째 줄부터 n줄에 걸쳐서 각 좌표 x, y, z가 공백으로 구분되어 입력된다.
    마지막 줄에 정렬 기준이 입력된다.

    정렬기준
    1 : x기준 오름차순
    2 : x기준 내림차순
    3 : y기준 오름차순
    4 : y기준 내림차순
    5 : z기준 오름차순
    6 : z기준 내림차순

    [입력값의 정의역]
    1 <= n <= 30,000
    -2^15 <= x, y, z <= 2^15
    입력되는 x, y, z값은 모두 다르다.
    Output

    정렬된 결과 점의 정보를 한 줄에 하나씩 x, y, z순으로 출력한다.
    IO Example

    입력
    3
    1 5 -2
    2 6 4
    -10 -11 100
    3

    출력
    -10 -11 100
    1 5 -2
    2 6 4

    * y기준으로 오름차순으로 출력한 것이다.

{% highlight c linenos %}

#include <stdio.h>
#include <stdlib.h>

typedef struct _dot {
    int x, y, z;
} dot;

void swap(int j, dot *dot_array[])
{
    dot *tmp_dot = (dot *)malloc(sizeof(dot));
    tmp_dot = dot_array[j];
    dot_array[j] = dot_array[j+1];
    dot_array[j+1] = tmp_dot;
}

int main(void)
{
    int n, i, j, tmpX, tmpY, tmpZ, sort_mode;
    scanf("%d", &n);
    dot *dot_array[n];
    for(i=0; i<n; i++)
    {
        scanf("%d %d %d", &tmpX, &tmpY, &tmpZ);
        dot_array[i] = (dot *)malloc(sizeof(dot));
        dot_array[i]->x = tmpX;
        dot_array[i]->y = tmpY;
        dot_array[i]->z = tmpZ;
    }
    scanf("%d", &sort_mode);
    switch(sort_mode) {
        case 1:
            //1 : x기준 오름차순
            for(i=0; i<n-1; i++)
            {
                for(j=0; j<n-i-1; j++)
                {
                    if(dot_array[j]->x > dot_array[j+1]->x)
                    {
                        swap(j, dot_array);
                    }
                }
            }
            break;
        case 2:
            //2 : x기준 내림차순
            for(i=0; i<n-1; i++)
            {
                for(j=0; j<n-i-1; j++)
                {
                    if(dot_array[j]->x < dot_array[j+1]->x)
                    {
                        swap(j, dot_array);
                    }
                }
            }
            break;
        case 3:
            //3 : y기준 오름차순
            for(i=0; i<n-1; i++)
            {
                for(j=0; j<n-i-1; j++)
                {
                    if(dot_array[j]->y > dot_array[j+1]->y)
                    {
                        swap(j, dot_array);
                    }
                }
            }
            break;
        case 4:
            //4 : y기준 내림차순
            for(i=0; i<n-1; i++)
            {
                for(j=0; j<n-i-1; j++)
                {
                    if(dot_array[j]->y < dot_array[j+1]->y)
                    {
                        swap(j, dot_array);
                    }
                }
            }
            break;
        case 5:
            //5 : z기준 오름차순
            for(i=0; i<n-1; i++)
            {
                for(j=0; j<n-i-1; j++)
                {
                    if(dot_array[j]->z > dot_array[j+1]->z)
                    {
                        swap(j, dot_array);
                    }
                }
            }
            break;
        case 6:
            //6 : z기준 내림차순
            for(i=0; i<n-1; i++)
            {
                for(j=0; j<n-i-1; j++)
                {
                    if(dot_array[j]->z < dot_array[j+1]->z)
                    {
                        swap(j, dot_array);
                    }
                }
            }
            break;
    }
    for(i=0; i<n; i++)
    {
        printf("%d %d %d\n", dot_array[i]->x, dot_array[i]->y, dot_array[i]->z);
    }
    return 0;
}

{% endhighlight %}

여기까지 했더니 Time Limit Exceeded 이 떠버렸다.

{% highlight c linenos %}

for(i=0; i<n; i++)
{
	scanf("%d %d %d", &tmpX, &tmpY, &tmpZ);
	dot_array[i] = (dot *)malloc(sizeof(dot));
	dot_array[i]->x = tmpX;
	dot_array[i]->y = tmpY;
	dot_array[i]->z = tmpZ;
}

{% endhighlight %}

이 부분의 경우는 아래의 경우로 코드 단순화가 가능하다.

{% highlight c linenos %}

for(i=0; i<n; i++)
    {
    	dot_array[i] = (dot *)malloc(sizeof(dot));
        scanf("%d %d %d", &dot_array[i]->x, &dot_array[i]->y, &dot_array[i]->z);
    }

{% endhighlight %}

퀵정렬을 적용해봤다.

{% highlight c linenos %}

#include <stdio.h>
#include <stdlib.h>

//sturcture definition
typedef struct _dot {
    int x, y, z;
} dot;

//Swap Structure which indexs are i and j
void swap(int i, int j, dot *dot_array[])
{
    dot *tmp_dot = (dot *)malloc(sizeof(dot));
    tmp_dot = dot_array[j];
    dot_array[j] = dot_array[i];
    dot_array[i] = tmp_dot;
    free(tmp_dot);
}

//compare
int compare(dot *dot_array[], int index, int pivot, int sort_mode, int compflag)
{
	switch(sort_mode) {
        case 1:
            //1 : x기준 오름차순
            if(compflag)
            {
            	if(dot_array[index]->x < pivot) return 1;
            	else return 0;
            }
            else
            {
            	if(dot_array[index]->x > pivot) return 1;
            	else return 0;
            }
	    break;
        case 2:
            //2 : x기준 내림차순
            if(compflag)
            {
            	if(dot_array[index]->x > pivot) return 1;
            	else return 0;
            }
            else
            {
            	if(dot_array[index]->x < pivot) return 1;
            	else return 0;
            }
	    break;
        case 3:
            //3 : y기준 오름차순
            if(compflag)
            {
            	if(dot_array[index]->y < pivot) return 1;
            	else return 0;
            }
            else
            {
            	if(dot_array[index]->y > pivot) return 1;
            	else return 0;
            }
	    break;
        case 4:
            //4 : y기준 내림차순
            if(compflag)
            {
            	if(dot_array[index]->y > pivot) return 1;
            	else return 0;
            }
            else
            {
            	if(dot_array[index]->y < pivot) return 1;
            	else return 0;
            }
	    break;
        case 5:
            //5 : z기준 오름차순
            if(compflag)
            {
            	if(dot_array[index]->z < pivot) return 1;
            	else return 0;
            }
            else
            {
            	if(dot_array[index]->z > pivot) return 1;
            	else return 0;
            }
	    break;
        case 6:
            //6 : z기준 내림차순
            if(compflag)
            {
            	if(dot_array[index]->z > pivot) return 1;
            	else return 0;
            }
            else
            {
            	if(dot_array[index]->z < pivot) return 1;
            	else return 0;
            }
	    break;
    }
}

//assign pivot's value
int assign_pivot(dot *dot_array[], int left, int right, int sort_mode)
{
    switch(sort_mode) {
        case 1:
        case 2:
            return dot_array[(left + right)/2]->x;
        break;
        case 3:
        case 4:
            return dot_array[(left + right)/2]->y;
        break;
        case 5:
        case 6:
            return dot_array[(left + right)/2]->z;
        break;
    }
}

//quicksort
void quickSort(dot *dot_array[], int left, int right, int sort_mode)
{
	int i = left, j = right;
	int pivot = assign_pivot(dot_array, left, right, sort_mode);

	while(i <= j)
	{
		while(compare(dot_array, i, pivot, sort_mode, 1)) i++;
		while(compare(dot_array, j, pivot, sort_mode, 0)) j--;
		if(i <= j)
		{
			swap(i, j, dot_array);
			i++; j--;
		}
	}

	if (left < j)
            quickSort(dot_array, left, j, sort_mode);
	if (i < right)
            quickSort(dot_array, i, right, sort_mode);
}

int main(void)
{
    int n, i, tmpX, tmpY, tmpZ, sort_mode;
    scanf("%d", &n);
    dot *dot_array[n];
    for(i=0; i<n; i++)
    {
        scanf("%d %d %d", &tmpX, &tmpY, &tmpZ);
        dot_array[i] = (dot *)malloc(sizeof(dot));
        dot_array[i]->x = tmpX;
        dot_array[i]->y = tmpY;
        dot_array[i]->z = tmpZ;
    }
    scanf("%d", &sort_mode);
    quickSort(dot_array, 0, n-1, sort_mode);
    for(i=0; i<n; i++)
    {
        printf("%d %d %d\n", dot_array[i]->x, dot_array[i]->y, dot_array[i]->z);
    }
    free(dot_array);
    return 0;
}

{% endhighlight %}

**관련문서**

- [구조체 배열 초기화](http://shinluckyarchive.tistory.com/218)
- [switch case 예제](http://mwultong.blogspot.com/2007/03/c-switch-switch-case-default-statement.html)
- [C 주석 스타일(영어)](https://msdn.microsoft.com/en-us/library/wfwda74e.aspx)

#no.171

{% highlight c linenos %}

#include <stdio.h>
#include <stdlib.h>

typedef struct queue
{
	int node_index;
	struct queue* next;
} queue;

typedef struct node
{
	int visit_flag;
	queue* node_queue;
} node;

int addEdge(node *nodes[], int node1, int node2)
{
	queue *tmp_queue = NULL;
	if(nodes[node1]->node_queue == NULL)
	{
		nodes[node1]->node_queue = (queue *)malloc(sizeof(queue));
		nodes[node1]->node_queue->node_index = node2;
		nodes[node1]->node_queue->next = NULL;
	}
	else
	{
		tmp_queue = nodes[node1]->node_queue;
		while(tmp_queue->next != NULL)
		{
			tmp_queue = tmp_queue->next;
		}
		tmp_queue->next = (queue *)malloc(sizeof(queue));
		tmp_queue->next->node_index = node2;
		tmp_queue->next->next = NULL;
	}
	return 0;
}

int addQueue(queue *bfs_queue, int input)
{
	queue *tmp_queue = bfs_queue;
	while(tmp_queue->next != NULL)
	{
		tmp_queue = tmp_queue->next;
	}
	tmp_queue->next = (queue *)malloc(sizeof(queue));
	tmp_queue->next->node_index = input;
	tmp_queue->next->next = NULL;
}

int bfs(node *nodes[], queue *bfs_queue, int start)
{
	int destination;
	queue *tmp_queue = NULL;
	while(bfs_queue != NULL)
	{
		while(nodes[start]->node_queue != NULL)
		{
			addQueue(bfs_queue, nodes[start]->node_queue->node_index);
			nodes[start]->node_queue = nodes[start]->node_queue->next;
		}

		tmp_queue = bfs_queue;

		while(tmp_queue != NULL)
		{
			destination = tmp_queue->node_index;
			if(!nodes[destination]->visit_flag)
			{
				printf("%d ", destination);
				nodes[destination]->visit_flag = 1;
				bfs(nodes, bfs_queue, destination);
			}
			bfs_queue = bfs_queue->next;
			tmp_queue = tmp_queue->next;
		}
	}
	return 0;
}

int main(void)
{
	int i, node_count, edge_count, node1, node2;
	scanf("%d %d", &node_count, &edge_count);
	node *nodes[node_count+1];
	//init nodes
	for(i=1; i<=node_count; i++)
	{
		nodes[i] = (node *)malloc(sizeof(node));
		nodes[i]->visit_flag = 0;
		nodes[i]->node_queue = NULL;
	}
	//init edges
	for(i=0; i<edge_count; i++)
	{
		scanf("%d %d", &node1, &node2);
		addEdge(nodes, node1, node2);
		addEdge(nodes, node2, node1);
	}
	//init bfs_queue
	queue *bfs_queue = (queue *)malloc(sizeof(queue));
	bfs_queue->node_index = 1;
	bfs_queue->next = NULL;
	//bfs
	bfs(nodes, bfs_queue, 1);
	return 0;
}

{% endhighlight %}
