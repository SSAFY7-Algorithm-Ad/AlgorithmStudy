# π 1102 (λ°νμ΄)

## μμμκ°, λ©λͺ¨λ¦¬
- 111720 KB
- 952 ms

## νμ΄ λ°©λ²
- μ°μ μμ νλ₯Ό νμ©νμ¬ κ±°λ¦¬κ° κ°μ₯ μ§§μ λΈλ μμΌλ‘ poll λ  μ μλλ‘ κ΅¬ννμμ΅λλ€.
- λ¬Όλ‘  κΈ°μ΅μ΄ νλλ λμ§ μμμ νμ΅ + κ΅¬κΈλ§μ λμμ λ°μ νμμ΅λλ€!

## Code
```java
import java.io.*;
import java.util.*;

class Node implements Comparable<Node> {
    int end;
    int weight;

    public Node(int end, int weight) {
        this.end = end;
        this.weight = weight;
    }

    @Override
    public int compareTo(Node o) {
        return weight - o.weight; // μμμ¬μΌ μμ λ°°μΉ
    }
}

public class DAY221102_BOJ1753_G4_μ΅λ¨κ²½λ‘ {
    static int V, E;
    static List<Node>[] list;

    static int[] dist;
    static boolean[] visited;
    static int INF = 987654321;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        // 1. μλ ₯
        V = Integer.parseInt(st.nextToken());
        E = Integer.parseInt(st.nextToken());

        int start = Integer.parseInt(br.readLine());

        // 2. λ¬΄νμΌλ‘ μ΄κΈ°ν
        dist = new int[V + 1];
        Arrays.fill(dist, INF);

        // 3. μ λ³΄ μΈν
        list = new ArrayList[V + 1];
        visited = new boolean[V + 1];
        for (int i = 1; i <= V; i++) {
            list[i] = new ArrayList<>();
        }

        for (int i = 0; i < E; i++) {
            st = new StringTokenizer(br.readLine());
            int s = Integer.parseInt(st.nextToken());
            int e = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());

            list[s].add(new Node(e, w));
        }

        dijkstra(start);

        // dist[] κ°±μ  λ

        for (int i = 1; i <= V; i++) {
            if (dist[i] == INF) {
                System.out.println("INF");
            } else {
                System.out.println(dist[i]);
            }
        }

    }

    private static void dijkstra(int start) {
        // 1. μμμ μ 0μΌλ‘ μΈν
        dist[start] = 0;

        // 2. μ°μ μμ ν
        PriorityQueue<Node> q = new PriorityQueue<>();
        // μμ λΈλμμ μμ λΈλλ‘ κ°λ μ΅λ¨ κ±°λ¦¬λ 0μ΄λ€ λ‘ μΈννκ³  μμ!
        q.add(new Node(start, 0));

        while (!q.isEmpty()) {
            Node node = q.poll(); // weight κ° μ μΌ μμ μΉκ΅¬λΆν° λμ΄
            int curr = node.end;

            // λ°©λ¬Ένλμ§ μ²΄ν¬
            if (visited[curr]) continue;
            visited[curr] = true;

            // currμ΄ μμμ , n.endκ° λμ°©μ 
            for (Node n: list[curr]) {
                // κ·Έλμ n.endμ κ±°λ¦¬κ° currμ κ±°λ¦¬ + n.weight λ³΄λ€ ν¬λ€λ©΄ κ°±μ 
                if (dist[n.end] > dist[curr] + n.weight) {
                    dist[n.end] = dist[curr] + n.weight;
                    q.add(new Node(n.end, dist[n.end]));
                }
            }
        }
    }
}

```
