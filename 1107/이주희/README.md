# ๐ 1107 (์ด์ฃผํฌ)

## ์์์๊ฐ, ๋ฉ๋ชจ๋ฆฌ
<img width="90%" alt="image" src="https://user-images.githubusercontent.com/83942393/207598590-865b4cc4-5137-4cee-956e-2cd79f9e7448.png">

## ํ์ด ๋ฐฉ๋ฒ
* BFS, ์๋ฎฌ๋ ์ด์

## Code
```Java
import java.io.*;
import java.util.ArrayDeque;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main_bj_13460_๊ตฌ์ฌํ์ถ2 {
	
	static int N, M;
	static char[][] map;
	static boolean[][][][] visited;
	static int[] dx = {-1, 0, 1, 0};	// ์, ์ฐ, ํ, ์ข
	static int[] dy = {0, 1, 0, -1};

	public static void main(String[] args) throws Exception {
//		System.setIn(new FileInputStream("res/input_bj_13460.txt"));
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine(), " ");
		
		int N = Integer.parseInt(st.nextToken());
		int M = Integer.parseInt(st.nextToken());
		
		map = new char[N][M];
		visited = new boolean[N][M][N][M]; 		// ๋ฐฉ๋ฌธ ์ฌ๋ถ ์ฒดํฌ
		
		int redX=0, redY=0, blueX=0, blueY=0;	// ๋นจ๊ฐ ๊ณต, ํ๋ ๊ณต ์์น ์ ์ฅ
		
		for(int i=0; i<N; i++) {
			map[i] = br.readLine().toCharArray();
			for(int j=0; j<M; j++) {
				if(map[i][j] == 'B') {
					blueX = i;
					blueY = j;
				}
				if(map[i][j] == 'R') {
					redX = i;
					redY = j;
				}
			}
		}
		
		System.out.println(bfs(redX, redY, blueX, blueY));
		br.close(); 
	}
	
	static class Position {
		private int redX;
		private int redY;
		private int blueX;
		private int blueY;
		private int cnt;
		
		Position(int redX, int redY, int blueX, int blueY, int cnt) {
			this.redX = redX;
			this.redY = redY;
			this.blueX = blueX;
			this.blueY = blueY;
			this.cnt = cnt;
		}
	}
	
	static int bfs(int redX, int redY, int blueX, int blueY) {
		Queue<Position> que = new ArrayDeque<>();
		que.add(new Position(redX, redY, blueX, blueY, 1));
		visited[redX][redY][blueX][blueY] = true;
		
		while(!que.isEmpty()) {
			Position now = que.poll();
			
			if(now.cnt > 10) return -1;
			
			// 4๋ฐฉ ํ์
			outer: for(int i=0; i<4; i++) {
				// ๊ตฌ์ฌ ์ด๋
				int nrx = now.redX;
				int nry = now.redY;
				int nbx = now.blueX;
				int nby = now.blueY;
				
				// ํ๋ ๊ณต ์ด๋
				while(map[nbx + dx[i]][nby + dy[i]] != '#') {
					nbx += dx[i];
					nby += dy[i]; 
					
					if(map[nbx][nby] == 'O') {	// ํ๋ ๊ณต์ด ๊ตฌ๋ฉ์ ๋ค์ด๊ฐ๋ฉด ๋ฌด์กฐ๊ฑด ๋ค์ ๊ฒฝ๋ก
						continue outer;
					}
				}
				
				while(map[nrx + dx[i]][nry + dy[i]] != '#') {
					nrx += dx[i];
					nry += dy[i]; 
					
					if(map[nrx][nry] == 'O') {	// ํ๋ ๊ณต์ด ๊ตฌ๋ฉ์ ๋ค์ด๊ฐ์ง ์๊ณ , ๋นจ๊ฐ ๊ณต์ด ๋ค์ด๊ฐ๋ฉด ๋ต return
						return now.cnt;
					}
				}
				
				// ๋นจ๊ฐ ๊ณต๊ณผ ํ๋ ๊ณต ๋ ๋ค ๊ตฌ๋ฉ์ ๋ค์ด๊ฐ์ง ์๊ณ 
				// ๋นจ๊ฐ ๊ณต๊ณผ ํ๋ ๊ณต์ ์์น๊ฐ ๊ฒน์น๋ ๊ฒฝ์ฐ -> ์,์ฐ,ํ,์ข ๋ฐฉํฅ์ ๋ฐ๋ผ ๋ค์ ์์ ๊ณต ์์น ์ฌ์กฐ์ 
				if(nrx == nbx && nry == nby) {
					
					// ์
					if(i == 0) {
						if(now.redX > now.blueX) {
							nrx -= dx[i];
						}
						else {
							nbx -= dx[i];
						}
					}
					
					// ์ฐ
					if(i == 1) {
						if(now.redY > now.blueY) {
							nby -= dy[i];
						}
						else {
							nry -= dy[i];
						}
					}
					
					// ํ
					if(i == 2) {
						if(now.redX > now.blueX) {
							nbx -= dx[i];
						}
						else {
							nrx -= dx[i];
						}
					}
					
					// ์ข
					if(i == 3) {
						if(now.redY > now.blueY) {
							nry -= dy[i];
						}
						else {
							nby -= dy[i];
						}
					}
				}
				
				// ๊ตฌ์ฌ ์ด๋ ์ข๋ฃ
				if(!visited[nrx][nry][nbx][nby]) {
					visited[nrx][nry][nbx][nby] = true;
					que.offer(new Position(nrx, nry, nbx, nby, now.cnt+1));
				}
				
			}
		}
		return -1;
	}

}

```
