# BFS
#include <bits/stdc++.h>
#include <omp.h>
using namespace std;
const int N = 1e5 + 5;
vector<int> g[N];
bool vis[N];
void bfs(int s) {
 queue<int> q;
 q.push(s);
 vis[s] = true;
 while (!q.empty()) {
 int u = q.front();
 q.pop();
 #pragma omp parallel for
 for (int i = 0; i < g[u].size(); i++) {
 int v = g[u][i];
 if (!vis[v]) {
 vis[v] = true;
 q.push(v);
 }
 }
 }
}
void dfs(int u) {
 vis[u] = true;
 #pragma omp parallel for
 for (int i = 0; i < g[u].size(); i++) {
 int v = g[u][i];
 if (!vis[v])
 dfs(v);
 }
}
int main() {
 int n, m, s, choice;
 cout << "Enter number of vertices : ";
 cin >> n ;
 cout << "Enter number of edges : ";
 cin >> m ;
 cout << "Enter number of source vertex : ";
 cin >> s ;
 cout << "Enter 1 for BFS traversal and 2 for DFS traversal : ";
 cin >> choice;
 for (int i = 0; i < m; i++) {
 int x, y;
 cout << "Enter Edge "<<i+1<<": ";
 cout << "Enter Edge Vertex 1 : ";
 cin >> x ;
 cout << "Enter Edge Vertex 2 : ";
 cin >> y;
 g[x].push_back(y);
 g[y].push_back(x);
 }
 cout<<endl;
 if (choice == 1)
 bfs(s);
 else if (choice == 2)
 dfs(s);
 else
 cout << "Invalid choice\n";
 cout << "The result of traversal:\n";
 for (int i = 1; i <= n; i++) {
 if (vis[i])
 cout << i << " ";
 }
 cout << endl;
 return 0;
}
