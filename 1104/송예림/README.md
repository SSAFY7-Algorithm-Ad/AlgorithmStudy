# π 1916

## μμμκ°, λ©λͺ¨λ¦¬
552ms, 51844KB

## νμ΄ λ°©λ²
- νλμ μμμ μμ λͺ¨λ  λΈλλ‘μ μ΅μ λΉμ© κ²½λ‘ -> λ€μ΅μ€νΈλΌ
- λͺ¨λ  λΈλλ‘ λμ°©νλ κ²½λ‘ κ΅¬ν ν κ²°κ³Ό μΆλ ₯

β μκ°μ΄κ³Ό
- νμ¬ νμν  λΈλμ λ°©λ¬Έ λ°°μ΄μ΄ trueμΈ κ²λ νμνκ² νμμ
- λ°©λ¬Ένλ λΈλλ νμνμ§ λͺ»νλλ‘ μμ 


## Code

```java
package BAEKJOON;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.PriorityQueue;
import java.util.StringTokenizer;

public class gold5_1916_μ΅μλΉμ©κ΅¬νκΈ° {

    static int N, M, start, end, result=Integer.MAX_VALUE;
    static ArrayList<Node>[] graph;
    static int[] dist;
    static boolean[] visit;

    public static void main(String[] args) throws NumberFormatException, IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        N = Integer.parseInt(br.readLine());
        M = Integer.parseInt(br.readLine());
        graph = new ArrayList[N+1];
        dist = new int[N+1];
        visit = new boolean[N+1];

        for (int i = 0; i <= N; i++) {
            graph[i] = new ArrayList<>();
            dist[i] = Integer.MAX_VALUE;
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int iu = Integer.parseInt(st.nextToken());
            int iv = Integer.parseInt(st.nextToken());
            int iw = Integer.parseInt(st.nextToken());
            graph[iu].add(new Node(iv, iw));
        }

        st = new StringTokenizer(br.readLine());
        start = Integer.parseInt(st.nextToken());
        end = Integer.parseInt(st.nextToken());

        dijkstra();

        System.out.println(dist[end]);
    }

    private static void dijkstra() {
        PriorityQueue<Node> queue = new PriorityQueue<>();
        dist[start] = 0;
        queue.add(new Node(start, dist[start]));

        while(!queue.isEmpty()) {
            Node current = queue.poll();
            if(!visit[current.v]) {
                visit[current.v] = true;

                for (Node next : graph[current.v]) {
                    if(!visit[next.v] && dist[next.v] > current.w + next.w) {
                        dist[next.v] = current.w + next.w;
                        queue.add(new Node(next.v, dist[next.v]));
                    }
                }
            }
        }
    }

    static class Node implements Comparable<Node>{
        int v, w;

        public Node(int v, int w) {
            this.v = v;
            this.w = w;
        }

        @Override
        public int compareTo(Node o) {
            return Integer.compare(this.w, o.w);
        }
    }
}

```