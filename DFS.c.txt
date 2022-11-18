#include <stdio.h>
#include <stdlib.h>
#define size 20
int vis[size], top = -1, stack[size], a[size][size];
 
void dfs( int s, int n );
void push( int item );
int pop();

void main()
{
    int n, i, s, j;

	printf("Enter number of vertices : ");
	scanf( "%d", &n );

    for ( i = 1;i <= n;i++ )
	{
	    for ( j = 1;j <= n;j++ )
		{
		    printf( "Enter 1 if %d has a edge with %d else 0 : ", i, j );
		    scanf( "%d", &a[i][j] );
		}
	}

    printf( "The adjacency matrix is : \n" );
    for ( i = 1; i <= n; i++ )
	{
	    for ( j = 1; j <= n; j++ )
		{
		    printf( " %d", a[i][j] );
		}
	    printf("\n");
	}

	for ( i = 1; i <= n; i++ ){
		vis[i] = 0;
	}
	printf( "Enter the source vertex :" );
	scanf( "%d", &s );
		
	dfs(s, n);

}

void dfs( int s, int n )
{
    int i, k;
    push(s);
    vis[s] = 1;
    k = pop();

    if ( k != 0 )
	printf( " %d ", k );

    while ( k != 0 )
	{
	    for ( i = 1;i <= n;i++ )
		if ( ( a[k][i] != 0 ) && ( vis[i] == 0 ) )
		    {
			push(i);
			vis[i] = 1;
		    }

	    k = pop();

	    if ( k != 0 )
		printf( "%d", k );
	}

    for ( i = 1;i <= n;i++ )
	if ( vis[i] == 0 )
	    dfs(i, n);
}

void push( int item )
{
    if ( top == size-1 )
	printf( "Stack overflow!" );
    else
	stack[++top] = item;
}

int pop()
{
    int k;

    if ( top == -1 )
	return (0);
    else
	{
	    k = stack[top--];
	    return (k);
	}
} 