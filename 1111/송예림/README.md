# ๐ 14503

## ์์์๊ฐ, ๋ฉ๋ชจ๋ฆฌ
132ms, 14384KB

## ํ์ด ๋ฐฉ๋ฒ
dfs๋ก ๊ตฌํ

## Code

```java
package bj;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class gold5_14503_๋ก๋ด์ฒญ์๊ธฐ {
	// ๋ถ ๋ ๋จ ์
	static int[] dr = { -1, 0, 1, 0 };
	static int[] dc = { 0, 1, 0, -1 };
	static int N, M, R, C, D, result;
	static int[][] map;

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		map = new int[N][M];
		st = new StringTokenizer(br.readLine());
		R = Integer.parseInt(st.nextToken());
		C = Integer.parseInt(st.nextToken());
		D = Integer.parseInt(st.nextToken());

		for (int r = 0; r < map.length; r++) {
			st = new StringTokenizer(br.readLine());
			for (int c = 0; c < map[r].length; c++) {
				map[r][c] = Integer.parseInt(st.nextToken());
			}
		}

		map[R][C] = 2;
		result = 1;
		play(R, C, D);
		System.out.println(result);
	}

	private static void play(int r, int c, int dist) {
		for (int d = 0; d < dc.length; d++) {
			dist = (dist + 3) % 4;
			int nr = r + dr[dist];
			int nc = c + dc[dist];
			// ์ผ์ชฝ๋ฐฉํฅ์ด ์ฒญ์ํ์ง ์์๋ค๋ฉด
			if (map[nr][nc] == 0 && nr >= 0 && nr < N && nc >= 0 && nc < M) {
				// ํ์ฌ ์์น ์ฒญ์
				map[nr][nc] = 2;
				result++;

				// ํ์นธ ์ ์ง ํ ์งํ
				play(nr, nc, dist);
				return;
			}
		}

		int back = (dist + 2) % 4;
		int nr = r + dr[back];
		int nc = c + dc[back];
		if (nr >= 0 && nr < N && nc >= 0 && nc < M) {
			if (map[nr][nc] != 1) {
				// 3๋ฒ ์งํ
				play(nr, nc, dist);
			}
		}
	}
}

```
