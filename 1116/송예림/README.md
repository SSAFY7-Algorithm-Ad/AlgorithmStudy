# ๐ 16236

## ์์์๊ฐ, ๋ฉ๋ชจ๋ฆฌ
136ms, 14676KB

## ํ์ด ๋ฐฉ๋ฒ
- bfs๋ก ๊ตฌํ, pq ์ฌ์ฉ
- compare ํจ์์์ ์ด์ด์๋ ์ค์... (this.r, o.r)

## Code

```java
package BAEKJOON;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.StringTokenizer;

public class gold3_16236_์๊ธฐ์์ด {
	static int[] dr = {-1, 0, 1, 0};
	static int[] dc = {0, 1, 0, -1};
	static int N, result = 0;
	static Node baby;
	static int[][] map;
	static boolean[][] visit;

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st;
		N = Integer.parseInt(br.readLine());
		map = new int[N][N];

		for (int r = 0; r < map.length; r++) {
			st = new StringTokenizer(br.readLine());
			for (int c = 0; c < map[r].length; c++) {
				map[r][c] = Integer.parseInt(st.nextToken());
				if(map[r][c] == 9) {
					baby = new Node(r, c, 0);
					map[r][c] = 0;
				}
			}
		}

		bfs();
		System.out.println(result);
	}

	private static void bfs() {
		int size = 2; // ์๊ธฐ์์ด ํฌ๊ธฐ
		int eat = 0; // ๋จน์ ๊ฐฏ์

		while(true) {
			PriorityQueue<Node> pq = new PriorityQueue<Node>();
			visit = new boolean[N][N];

			pq.add(new Node(baby.r, baby.c, 0));
			visit[baby.r][baby.c] = true;

			boolean check = false;

			// ์ฎ๊ฒจ๋ค๋๋ฉด์ ๋ฌผ๊ณ ๊ธฐ ๋จน๊ธฐ
			while(!pq.isEmpty()) {
				baby = pq.poll();

				// ๋จน์ด๊ฐ ์๊ณ , ์์ด ์ฌ์ด์ฆ๋ณด๋ค ์์ผ๋ฉด
				if(map[baby.r][baby.c] != 0 && map[baby.r][baby.c] < size) {
					// ๋ฌผ๊ณ ๊ธฐ ๋จน๊ธฐ
					map[baby.r][baby.c] = 0;
					eat++;
					// ์์ง์ธ ๊ฑฐ๋ฆฌ ์ถ๊ฐ
					result += baby.dist;
					// ๋จน์์ผ๋ฉด ๋๋ด๊ณ  ๋ค์ ์คํํด์ผํ๋๊น true
					check = true;
					break;
				}

				for (int d = 0; d < dc.length; d++) {
					int nr = baby.r + dr[d];
					int nc = baby.c + dc[d];

					if(nr>=0 && nr<N && nc>=0 && nc<N && !visit[nr][nc] && map[nr][nc] <= size) {
						pq.add(new Node(nr, nc, baby.dist+1));
						visit[nr][nc] = true;
					}
				}
			}

			// ๋จน์ ๋ฌผ๊ณ ๊ธฐ๊ฐ ์๋ค๋ ๋ป~
			if(!check) {
				break;
			}

			// ์์ด ์ฌ์ด์ฆ ๋ณ๊ฒฝ~
			if(size == eat) {
				size++;
				eat = 0;
			}
		}

	}

	static class Node implements Comparable<Node>{
		int r, c, dist;

		public Node(int x, int y, int dist) {
			super();
			this.r = x;
			this.c = y;
			this.dist = dist;
		}

		@Override
		public int compareTo(Node o) {
			if(o.dist == this.dist) {
				if(o.r == this.r) {
					return Integer.compare(this.c, o.c);
				}
				return Integer.compare(this.r, o.r);
			}
			return Integer.compare(this.dist, o.dist);
		}
	}

}

```
