# ๐ 1109 (์ด์ฃผํฌ)

## ์์์๊ฐ, ๋ฉ๋ชจ๋ฆฌ
![3](https://user-images.githubusercontent.com/83942393/205477083-629a7c85-7631-47b5-b179-78a162318944.PNG)


## ํ์ด ๋ฐฉ๋ฒ
- ํธ๋๋ฐ ๋ช์ผ ๊ฑธ๋ ธ๋ค..
- ๋ฒฝ ๊นจ๋ถ์๋ ๋ฌธ์ ๋ 3์ฐจ์ ๋ฐฐ์ด๋ก๋ง ํ ์ ์๋ ์ค ์์๋๋ฐ, ์ธ์ ํ ๋ฐฉ๊ณผ ํฉ์น๋ ๋ฐฉ๋ฒ์ ์ฒ์ ๋ด์ ์ข์ ๊ณต๋ถ๊ฐ ๋ ๊ฒ ๊ฐ๋ค.

## Code

```java
import java.io.*;
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.HashSet;
import java.util.Queue;
import java.util.Set;
import java.util.StringTokenizer;

public class Main_bj_2234_์ฑ๊ณฝ2 {
	
	static int[][] wall, map;	// ๋ฒฝ์ ์ ๋ณด๋ฅผ ๋ด์ 2์ฐจ์ ๋ฐฐ์ด, ๊ฐ์ ๋ฐฉ ๋ฒํธ๋ฅผ ๋ด์ 2์ฐจ์ ๋ฐฐ์ด
	static int maxSize=0;
	static ArrayList<Integer> space = new ArrayList<>();	// ๋ฐฉ ๋ฒํธ์ ํด๋นํ๋ ๋์ด ๋ฆฌ์คํธ
	static HashMap<Integer, Set<Integer>> side = new HashMap<>();	// ๋ฐฉ๊ณผ ์ธ์ ํ ๋ฐฉ์ ๋ฆฌ์คํธ
	static Queue<int[]> que;
	static int[] di = {0, -1, 0, 1};
	static int[] dj = {-1, 0, 1, 0};
	static int[] dr = {1, 2, 4, 8};
	
	public static void main(String[] args) throws Exception {
		System.setIn(new FileInputStream("res/input_bj_2234.txt"));
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		StringTokenizer st = new StringTokenizer(br.readLine(), " ");
		int M = Integer.parseInt(st.nextToken());
		int N = Integer.parseInt(st.nextToken());
		
		wall = new int[N][M];	// ๋ฒฝ์ ์ ๋ณด๋ฅผ ๋ด์ ๋ฐฐ์ด
		map = new int[N][M];	// ๋ฐฉ์ ๋ฒํธ๋ฅผ ๋ด์ ๋ฐฐ์ด
		
		for(int i=0; i<N; i++) {
			st = new StringTokenizer(br.readLine(), " ");
			for(int j=0; j<M; j++) {
				wall[i][j] = Integer.parseInt(st.nextToken());
			}
		}
		que = new ArrayDeque<>();
		int num = 1; 	// 1๋ฒ ๋ฐฉ๋ถํฐ ๋ฒํธ ๋งค๊ธฐ๊ธฐ
		for(int i=0; i<N; i++) {
			for(int j=0; j<M; j++) {
				if (map[i][j] == 0) {			// ์์ง ๋ฐฉ๋ฌธ ์ํ๋ค๋ฉด
					bfs(i, j, num++, N, M); 	// ๊ฐ๋ค ์ค๋ฉด ๋ฒํธ๊ฐ 1์ฉ ์ฆ๊ฐ
				}
			}
		}
		
		int roomNum = num-1;
		System.out.println(roomNum);
		System.out.println(maxSize);
		
		
		int sum = 0; // ๋ฒฝ ํ๋ ํ๋ฌผ๊ณ  ํฉ์น ์ต๋ ๋์ด 
		for(int room=1; room<=roomNum; room++) {	// ๋ฐฉ ํ๊ฐ์ฉ ๋์๋ณด๋ฉฐ
			if(side.get(room) != null) {	// ์ธ์ ํ ๋ฐฉ์ด ์๋ค๋ฉด
				for(int j : side.get(room)) {	// ์ธ์ ํ ๋ฐฉ ํ๊ฐ์ฉ ๋ฐ์์ค๊ธฐ
					sum = Math.max(sum, space.get(room-1) + space.get(j-1));
				}
			}
		}
		
		System.out.println(sum);
	}
	
	static void bfs(int i, int j, int num, int N, int M) {
		map[i][j] = num;
		que.add(new int[] {i, j});
		
		Set<Integer> set = new HashSet<>();		// ํ์ฌ ๋ฐฉ๊ณผ ์ธ์ ํ ๋ฐฉ์ ๋ฒํธ, ๊ฒน์น์ง ์๊ธฐ ์ํด set ์ฌ์ฉ
		
		int cnt = 0;
		while(!que.isEmpty()) {
			int[] now = que.poll();
			cnt++;
			
			for(int d=0; d<4; d++) {
				int ni = now[0] + di[d];
				int nj = now[1] + dj[d];
				
				if(ni<0 || ni>=N || nj<0 || nj>=M) continue;
				if(map[ni][nj] != 0 && map[ni][nj] != num) {	// ๋ฐฉ๋ฌธ์ ํ๋๋ฐ ์ง๊ธ ๋ฐฉ ๋ฒํธ์ ๋ค๋ฅด๋ค๋ฉด ์ธ์ ํ ๋ฐฉ
					set.add(map[ni][nj]);
					continue;
				}
				if((wall[now[0]][now[1]] & dr[d]) == 0 && map[ni][nj] == 0) {	// ๊ฐ ์ ์๋ ๋ฐฉ์ด๊ณ , ๋ฐฉ๋ฌธํ์ง ์์๋ค๋ฉด
					que.add(new int[] {ni, nj});
					map[ni][nj] = num; 	// num ๋ฒ ๋ฐฉ ํ ๋น
				}
			}
		}
		
		maxSize = Math.max(maxSize, cnt);
		space.add(cnt);
		side.put(num, set);
	}

}
```
