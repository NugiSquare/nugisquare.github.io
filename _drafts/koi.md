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

#no.860

#include <stdio.h>
#include <string.h>

long long prime_number(int k, long long *array)
{
	if(array[k] != 0)
	{
		return array[k];
	}
	else
	{
		int flag = 0;
		int divide_flag = 0;
		int i;
		if(array[k-1] == 0)
		{
			array[k-1] = prime_number(k-1, array);
		}
		int ans = array[k-1];
		while(!flag)
		{
			ans++; divide_flag = 0;
			for(i=1; i<k; i++)
			{
				if(ans % array[i] == 0)
				{
					divide_flag = 1;
				}
				if(divide_flag)
					break;
			}
			if(!divide_flag)
				flag = 1;
		}
		return ans;
	}
}

int main(void)
{
	int k;
	long long ans;

	scanf("%d", &k);

	long long array[k+1];
	memset( array, 0, (k+1)*sizeof(long long) );
	array[1] = 2;

	ans = prime_number(k, array);
	printf("%d", ans);
}

#no.180

???

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

#no.169

    Background

    깊이우선탐색(DFS)는 그래프의 임의의 한 정점에서 출발하여, 연결된 정점들 중 하나에 대해서 깊이 순으로 먼저 탐색해 나가는 탐색법이다. 예를 들어 다음과 같은 그래프를 보자.

    <이미지>

    이 그리프에서 1번 정점에서 출발한 깊이우선탐색 결과는 다음과 같다.

    1-2-3-4-6-5-7

    (단, 한 점정에서 갈 수 있는 곳이 여러 곳일 먼저 입력된 정점 부터 먼저 방문한다. FIFO 즉, 2 4, 2 3 순으로 입력되었다면 2번 정점에서 4번을 먼저 방문하고 나중에 3번을 방문하도록 작성해야 한다.)
    문제에 주어지는 모든 그래프는 양방향 무가중치 그래프이다.
    Input

    첫 번째 줄에 정점의 수와 간선의 수가 공백으로 구분되어 입력된다. (단 정점은 100개 이하, 간선은 200개 이하임)
    둘 째 줄부터 간선의 수에 해당되는 줄 만큼 한 줄에 한 간선의 출발점과 도착점이 공백으로 구분되어 입력된다.
    Output

    DFS순회 결과를 공백으로 구분하여 출력한다. (출발점은 1)
    IO Example

    입력
    7 8
    1 2
    1 4
    1 5
    2 3
    3 4
    3 7
    4 6
    5 6

    출력
    1 2 3 4 6 5 7

    DATA제작 및 정답제작 : 이승현(27th)

FIFO라 인접행렬에 큐를 삽입한 형태를 처음엔 생각하였으나, 인접 리스트를 사용하는 것이 더 깔끔한 코드가 될 것이라 생각해 진행해보았다.

{% highlight c linenos %}

#include <stdio.h>
#include <stdlib.h>

#define TRUE 1
#define FALSE 0

typedef struct _vertex
{
    int index, visited;
    struct _vertex* next_vertex;
} vertex;

void insert_node(int vtx1, int vtx2, vertex *vertexs[])
{
    vertex *tmp_vertex = (vertex *) malloc(sizeof(vertex));
    vertex *new_vertex = (vertex *) malloc(sizeof(vertex));
    tmp_vertex = vertexs[vtx1];
    while(tmp_vertex->next_vertex != NULL) {
        tmp_vertex = tmp_vertex->next_vertex;
    }
    tmp_vertex->next_vertex = vertexs[vtx2];
}

void dfs(int start, vertex *vertexs[])
{
    printf("%d ", start);
    vertexs[start]->visited = TRUE;

    while (vertexs[start]->next_vertex != NULL) {
        if(vertexs[start]->next_vertex->visited == TRUE) {
            vertex *tmp_vertex = (vertex *) malloc(sizeof(vertex));
            tmp_vertex = vertexs[start]->next_vertex;
            vertexs[start]->next_vertex = vertexs[start]->next_vertex->next_vertex;
        }
        else {
            vertex *tmp_vertex = (vertex *) malloc(sizeof(vertex));
            tmp_vertex = vertexs[start]->next_vertex;
            vertexs[start]->next_vertex = vertexs[start]->next_vertex->next_vertex;
            dfs(tmp_vertex->index, vertexs);
        }
    }
}

int main(void)
{
    int num_vertex, num_edge, i, vtx1, vtx2, start;
    scanf("%d %d", &num_vertex, &num_edge);
    vertex *vertexs[num_vertex];
    for(i=0; i<num_vertex; i++)
    {
        vertexs[i] = (vertex *) malloc(sizeof(vertex));
        vertexs[i]->index = i;
        vertexs[i]->visited = FALSE;
        vertexs[i]->next_vertex = NULL;
    }
    for(i=0; i<num_edge; i++)
    {
        scanf("%d %d", &vtx1, &vtx2);
        if(i==0) { start = vtx1; }
        insert_node(vtx1, vtx2, vertexs);
        insert_node(vtx2, vtx1, vertexs);
    }

    dfs(start, vertexs);

    return 0;
}

{% endhighlight %}

이 경우에 전혀 예상하지 못한 오류가 생겼다. 링크드리스트를 생성하는 와중에 복수의 edge인지 다음 vertex의 edge인지 구분을 하지 못하는 것이다. 인접 리스트 라는 것을 참고하여 다시 작성하였다.

{% highlight c linenos %}

#include <stdio.h>
#include <stdlib.h>

#define TRUE 1
#define FALSE 0

typedef struct _vertex
{
    int index, visited;
    struct _vertex* next_vertex;
} vertex;

typedef struct _vertex_list
{
	struct _vertex* vertex;
    struct _vertex_list* next_vertex;
} vertex_list;

void insert_node(int vtx1, int vtx2, vertex_list *vl)
{
	int i;
	for(i=1; i<vtx1; i++)
	{
		vl = vl->next_vertex;
	}
	vl->vertex = (vertex *) malloc(sizeof(vertex));
	vl->vertex->index = i;
	vl->vertex->visited = FALSE;
	vl->vertex->next_vertex = NULL;
}

void dfs(int start, vertex *vertexs[])
{
    printf("%d ", start);
    vertexs[start]->visited = TRUE;

    while (vertexs[start]->next_vertex != NULL) {
        if(vertexs[start]->next_vertex->visited == TRUE) {
            vertex *tmp_vertex = (vertex *) malloc(sizeof(vertex));
            tmp_vertex = vertexs[start]->next_vertex;
            vertexs[start]->next_vertex = vertexs[start]->next_vertex->next_vertex;
        }
        else {
            vertex *tmp_vertex = (vertex *) malloc(sizeof(vertex));
            tmp_vertex = vertexs[start]->next_vertex;
            vertexs[start]->next_vertex = vertexs[start]->next_vertex->next_vertex;
            dfs(tmp_vertex->index, vertexs);
        }
    }
}

int main(void)
{
    int num_vertex, num_edge, i, vtx1, vtx2, start;

    scanf("%d %d", &num_vertex, &num_edge);

	vertex_list vl;
	vl = (vertex_list *) malloc(sizeof(vertex_list));
	vl->vertex = NULL;
	vl->next_vertex = NULL;

	tmp_vl = (vertex_list *) malloc(sizeof(vertex_list));
	tmp_vl = vl;

    for(i=0; i<num_vertex; i++)
    {
        tmp_vl->vertex = (vertex *) malloc(sizeof(vertex));
        tmp_vl->vertex->index = i;
        tmp_vl->vertex->visited = FALSE;
        tmp_vl->vertex->next_vertex = NULL;
		tmp_vl->next_vertex = (vertex_list *) malloc(sizeof(vertex_list));
		tmp_vl = tmp_vl->next_vertex;
    }

    for(i=0; i<num_edge; i++)
    {
        scanf("%d %d", &vtx1, &vtx2);
        if(i==0) { start = vtx1; }
        insert_node(vtx1, vtx2, vl);
        insert_node(vtx2, vtx1, vl);
    }

    dfs(start, vertexs);

    return 0;
}

{% endhighlight %}
