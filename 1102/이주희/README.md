# ð 1753 (ì´ì£¼í¬)

## ìììê°, ë©ëª¨ë¦¬
![3](https://user-images.githubusercontent.com/83942393/200112632-ff9c3a32-9337-4f31-94fa-e25f77b14e6e.PNG)

## íì´ ë°©ë²
* í ê°ì ì ì ìì ë¤ë¥¸ ì ì ë¤ê¹ì§ì ìµë¨ ê²½ë¡ë¥¼ êµ¬íë ë¬¸ì  -> Dijkstra
* ì ì ì ê°¯ì Vê° ìµë 200ì´ë¯ë¡ 2ì°¨ì ì¸ì íë ¬ì ì¬ì©í  ì ì í ë©ëª¨ë¦¬ 256MB ì´ê³¼ -> ì¸ì  ë¦¬ì¤í¸ ì¬ì©
* ê°ì¥ ì ì ë¹ì©ì ì ì ì êµ¬íê¸° ìí´ PQ ì¬ì©

## Code
```Java
import java.io.*;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.PriorityQueue;
import java.util.StringTokenizer;

public class Main_bj_1753_ìµë¨ê²½ë¡ {
	static class Node {
		int vertex, weight;
		Node link;
		
		public Node(int vertex, int weight, Node link) {
			this.vertex = vertex;
			this.weight = weight;
			this.link = link;
		}
	}
	
	public static void main(String[] args) throws Exception{
		System.setIn(new FileInputStream("res/input_bj_1753.txt"));
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		StringTokenizer st = new StringTokenizer(br.readLine(), " ");
		int V = Integer.parseInt(st.nextToken());
		int E = Integer.parseInt(st.nextToken());
		int start = Integer.parseInt(br.readLine());
		
		Node[] adjList = new Node[V+1];
		
		for(int i=0; i<E; i++) {
			st = new StringTokenizer(br.readLine(), " ");
			int from = Integer.parseInt(st.nextToken());
			int to = Integer.parseInt(st.nextToken());
			int w = Integer.parseInt(st.nextToken());
			
			adjList[from] = new Node(to, w, adjList[from]);
		}
		
		PriorityQueue<int[]> pq = new PriorityQueue<>((o1, o2) -> (o1[1] - o2[1]));		// ìµì ì°ì  ìì í
		int[] distance = new int[V+1];
		Arrays.fill(distance, Integer.MAX_VALUE);
		distance[start] = 0;
		pq.offer(new int[] {start, 0});
		
		while(!pq.isEmpty()) {
			int[] now = pq.poll();
			if(distance[now[0]] < now[1]) continue;
			
			for(Node temp = adjList[now[0]]; temp != null; temp = temp.link) {
				if(distance[temp.vertex] > distance[now[0]] + temp.weight) {	// íì¬ ìµì ë¹ì©ì´ ê°ì¥ ì ì ì ì ì ê±°ì³ê°ë ê²ì´ ë ë¹ì©ì´ ì ë¤ë©´
					distance[temp.vertex] = distance[now[0]] + temp.weight;
					pq.offer(new int[] {temp.vertex, distance[temp.vertex]});
				}
			}
		}
		
		StringBuilder sb = new StringBuilder();
		for(int i=1; i<=V; i++) {
			if(distance[i] >= Integer.MAX_VALUE)
				sb.append("INF").append("\n");
			else
				sb.append(distance[i]).append("\n");
		}
		
		System.out.print(sb.toString());
		br.close();
	}
}
```
