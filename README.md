#include <stdio.h>
#include <limits.h>
#define INF INT_MAX 
void floydWarshall(int graph[5][5]) {
    int dist[5][5];
    for (int i = 0; i < 5; i++) {
        for (int j = 0; j < 5; j++) {
            if (graph[i][j] == 0 && i != j)
                dist[i][j] = INF;
            else
                dist[i][j] = graph[i][j];
        }
    }
    for (int k = 0; k < 5; k++) {
        for (int i = 0; i < 5; i++) {
            for (int j = 0; j < 5; j++) {
                if (dist[i][k] != INF && dist[k][j] != INF) {
                    dist[i][j] = (dist[i][j] < dist[i][k] + dist[k][j]) ? dist[i][j] : dist[i][k] + dist[k][j];
                }
            }
        }
    }
    printf("\nThe shortest distances between every pair of vertices:\n");
    for (int i = 0; i < 5; i++) {
        for (int j = 0; j < 5; j++) {
            if (dist[i][j] == INF)
                printf("INF ");
            else
                printf("%d ", dist[i][j]);
        }
        printf("\n");
    }
}
int main() {
    int graph[5][5] = {
        {0, 3, 6, INF, INF},
        {3, 0, 2, INF, INF},
        {INF, 2, 8, 1, INF},
        {INF, INF, 1, 0, 4},
        {INF, INF, INF, 4, 0}
    };
    printf("The original graph's adjacency matrix (0 represents no edge):\n");
    for (int i = 0; i < 5; i++) {
        for (int j = 0; j < 5; j++) {
            if (graph[i][j] == INF)
                printf("INF ");
            else
                printf("%d ", graph[i][j]);
        }
        printf("\n");
    }
    floydWarshall(graph);
    return 0;
}
