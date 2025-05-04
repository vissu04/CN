#include <stdio.h>
#include <limits.h>

#define MAX_VERTICES 100
#define INF 99999 // Define a large number as infinity

// Function to find the vertex with the minimum distance value
int minDistance(int dist[], int sptSet[], int vertices) {
    int min = INT_MAX, minIndex = -1;
    int v;
    for (v = 0; v < vertices; v++) {
        if (!sptSet[v] && dist[v] < min) {
            min = dist[v];
            minIndex = v;
        }
    }
    return minIndex;
}

// Function to print the constructed distance array
void printSolution(int dist[], int vertices) {
    int i;
    printf("Vertex \tDistance from Source\n");
    for (i = 0; i < vertices; i++) {
        if (dist[i] == INF)
            printf("%d \tINF\n", i);
        else
            printf("%d \t%d\n", i, dist[i]);
    }
}

// Function to implement Dijkstra's algorithm
void dijkstra(int graph[MAX_VERTICES][MAX_VERTICES], int src, int vertices) {
    int dist[MAX_VERTICES];  // Distance array
    int sptSet[MAX_VERTICES]; // Shortest Path Tree Set
    int i, count, u, v;

    // Initialize all distances as INF and sptSet[] as false
    for (i = 0; i < vertices; i++) {
        dist[i] = INF;
        sptSet[i] = 0;
    }

    // Distance from source to itself is always 0
    dist[src] = 0;

    // Find shortest path for all vertices
    for (count = 0; count < vertices - 1; count++) {
        u = minDistance(dist, sptSet, vertices);

        // If no vertex is found, break early
        if (u == -1)
            break;

        // Mark the picked vertex as processed
        sptSet[u] = 1;

        // Update distance of adjacent vertices
        for (v = 0; v < vertices; v++) {
            if (!sptSet[v] && graph[u][v] && graph[u][v] != INF &&
                dist[u] != INF && dist[u] + graph[u][v] < dist[v]) {
                dist[v] = dist[u] + graph[u][v];
            }
        }
    }

    // Print the final distances
    printSolution(dist, vertices);
}

int main() {
    int vertices, i, j;

    // Input the number of vertices
    printf("Input the number of vertices: ");
    scanf("%d", &vertices);

    if (vertices <= 0 || vertices > MAX_VERTICES) {
        printf("Invalid number of vertices. Exiting...\n");
        return 1;
    }

    int graph[MAX_VERTICES][MAX_VERTICES];

    // Input the adjacency matrix
    printf("Input the adjacency matrix for the graph (use 99999 for infinity):\n");
    for (i = 0; i < vertices; i++) {
        for (j = 0; j < vertices; j++) {
            scanf("%d", &graph[i][j]);

            // Replace large values with INF for internal processing
            if (graph[i][j] == 99999) {
                graph[i][j] = INF;
            }
        }
    }

    int source;

    // Input the source vertex
    printf("Input the source vertex: ");
    scanf("%d", &source);

    if (source < 0 || source >= vertices) {
        printf("Invalid source vertex. Exiting...\n");
        return 1;
    }

    // Perform Dijkstra's algorithm
    dijkstra(graph, source, vertices);

    return 0;
}
