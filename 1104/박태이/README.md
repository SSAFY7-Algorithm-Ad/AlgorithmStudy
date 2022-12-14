# π 1104 (λ°νμ΄)

## μμμκ°, λ©λͺ¨λ¦¬
- 51172 KB
- 548 ms

## νμ΄ λ°©λ²
- 11μ 2μΌμ νμλ λ¬Έμ μ²λΌ μ°μ μμ νλ₯Ό νμ©νμ¬ κ±°λ¦¬κ° κ°μ₯ μ§§μ λΈλ μμΌλ‘ poll λ  μ μλλ‘ κ΅¬ννμμ΅λλ€.
- μ€μ€λ‘μ νμΌλ‘ νλ©΄μ κ΅¬νμ΄ λμ§ μλ λΆλΆμ μμ΄ μ‘°κΈ λ μ΄ν΄ν  μ μλ κ³κΈ°κ° λμμ΅λλ€. λ€μ΅μ€νΈλΌ λ¬Έμ λ₯Ό κ³μ νλ©΄μ κ°μ μ‘μμΌκ² μ΄μ!

## Code
```java
import java.io.*;
import java.util.*;

class Node implements Comparable<Node>{
    int end;
    int weight;

    public Node(int end, int weight) {
        this.end = end;
        this.weight = weight;
    }

    @Override
    public int compareTo(Node node) {
        return this.weight - node.weight;
    }
}

public class DAY221104_BOJ1916_G5_μ΅μλΉμ©κ΅¬νκΈ° {
    public static int V, E;
    public static List<Node>[] map;
    public static int[] dist;
    public static boolean[] visited;
    public static int INF = 987654321;
    public static int start, end;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        V = Integer.parseInt(st.nextToken());
        E = Integer.parseInt(br.readLine());

        map = new ArrayList[V + 1];
        for (int i = 1; i <= V; i++) {
            map[i] = new ArrayList<>();
        }

        for (int i = 0; i < E; i++) {
            st = new StringTokenizer(br.readLine());
            int s = Integer.parseInt(st.nextToken());
            int e = Integer.parseInt(st.nextToken());
            int d = Integer.parseInt(st.nextToken());

            // sμμ μΆλ°νλ λ²μ€λ eκΉμ§ dλ§νΌμ κ±°λ¦¬κ° κ±Έλ¦Ό
            map[s].add(new Node(e, d));
        }

        st = new StringTokenizer(br.readLine());
        start = Integer.parseInt(st.nextToken());
        end = Integer.parseInt(st.nextToken());

        // TODO λ°°μ΄μ μΈλ±μ€μ λμ λ²νΈλ₯Ό λμΌνκ² κ°μ Έκ° κ±°λΌμ +1λ‘ μμ±ν΄μΌνλ κ²μ λμΉ¨
        dist = new int[V + 1];
        visited = new boolean[V + 1];
        Arrays.fill(dist, INF);

        // μ΅μ κ±°λ¦¬λ‘ κ°±μ μν€κ³  μ€κΈ°
        dijkstra(start);

        System.out.println(dist[end]);
    }

    public static void dijkstra(int start) {
        // μμμ μ 0μΌλ‘ μ΄κΈ°ν
        dist[start] = 0;

        // κ±°λ¦¬κ° κ°μ₯ μ§§μ κ³³λΆν° μμν΄μ μ°μ μμ νμ λ΄κΈ°
        PriorityQueue<Node> q = new PriorityQueue<>();
        // μμμ μμ μμμ μΌλ‘ κ°λ κ² μ μΌ κ°κΉμ°λκΉ λ΄λ κ±°! κΉλ¨Ήμ§ λ§κΈ°
        q.add(new Node(start, 0));

        while (!q.isEmpty()) {
            Node node = q.poll();
            int curr = node.end;
            if (visited[curr]) continue;
            visited[curr] = true;

            // κ°±μ 
            for (Node n : map[curr]) {
                if (dist[n.end] > dist[curr] + n.weight) {
                    dist[n.end] = dist[curr] + n.weight;
                }
                q.add(new Node(n.end, dist[n.end]));
            }
        }
    }
}
```
