# ๐ 1956 (์ด์ฃผํฌ)

## ์์์๊ฐ, ๋ฉ๋ชจ๋ฆฌ
![3](https://user-images.githubusercontent.com/83942393/199091884-568caf7a-2a06-4110-9744-182324e43d24.PNG)

## ํ์ด ๋ฐฉ๋ฒ
* ์ต๋จ ๊ฒฝ๋ก ์๊ณ ๋ฆฌ์ฆ -> Floyd / Dijkstra
* ์ถ๋ฐ์ง๊ฐ ์ ํด์ง์ง ์์์ผ๋ฏ๋ก Floyd ์ฌ์ฉ

## Code
```Java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main_bj_1956_์ด๋ {

	public static void main(String[] args) throws Exception {
		System.setIn(new FileInputStream("res/input_bj_1956.txt"));
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		StringTokenizer st = new StringTokenizer(br.readLine(), " ");
		int V = Integer.parseInt(st.nextToken());
		int E = Integer.parseInt(st.nextToken());
		
		int[][] adjMatrix = new int[V+1][V+1];
		int INF = 987654321;
		for(int i=1; i<=V; i++)
			Arrays.fill(adjMatrix[i], INF);
		
		for(int i=0; i<E; i++) {
			st = new StringTokenizer(br.readLine(), " ");
			int a = Integer.parseInt(st.nextToken());
			int b = Integer.parseInt(st.nextToken());
			int w = Integer.parseInt(st.nextToken());
			
			adjMatrix[a][b] = w;
		}
		
		// ๊ฒฝ์ ์ง -> ์ถ๋ฐ์ง -> ๋์ฐฉ์ง
		for(int k=1; k<=V; k++) {
			for(int i=1; i<=V; i++) {
				if(i==k) continue;
				for(int j=1; j<=V; j++) {
					if(i==j || k==j) continue;
					if(adjMatrix[i][j] > adjMatrix[i][k] + adjMatrix[k][j]) {
						adjMatrix[i][j] = adjMatrix[i][k] + adjMatrix[k][j];
					}
				}
			}
		}
		
		int ans = INF;
		for(int i=1; i<=V; i++) {
			for(int j=1; j<=V; j++) {
				if(i==j) continue;			
				
				if(adjMatrix[i][j] != INF && adjMatrix[j][i] != INF)	// i-> j ๋ก ๊ฐ๋ ๊ฒฝ๋ก๊ฐ ์๊ณ , j->i ๋ก ๊ฐ๋ ๊ฒฝ๋ก๊ฐ ์๋ค๋ฉด ์ฌ์ดํด์ด ์กด์ฌํ๋ค๋ ๋ป
					ans = Math.min(ans, adjMatrix[i][j] + adjMatrix[j][i]);
			}
		}
		
		if(ans==INF)
			System.out.println(-1);
		else System.out.println(ans);
	}
}

```
