# π 1976 (κΉκ°νΈ)

## μμμκ°, λ©λͺ¨λ¦¬

288ms, 21988KB

## νμ΄ λ°©λ²

- dfsνμ©νμ¬ ν.
- μ²μμ νμ¬ μμΉμ λμλ₯Ό μ¬λ¬λ² λ°©λ¬Έν  κ³νμΌλλ₯Ό κ³ λ €νμ§ μμ νλ¦Ό

## Code

```Java
import java.io.*;
import java.util.*;
public class Main {
    static int N, M, trip_idx=0;
    static int[][] map;
    static boolean[] visit;
    static int[] trip;
    static boolean end;
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        N = Integer.parseInt(br.readLine());
        M = Integer.parseInt(br.readLine());
        map = new int[N][N];
        trip = new int[M];
        for(int i=0; i<N; i++) {
            st = new StringTokenizer(br.readLine()," ");
            for(int j=0; j<N; j++) map[i][j] = Integer.parseInt(st.nextToken());
        }
        st = new StringTokenizer(br.readLine()," ");
        for(int i=0; i<M; i++) trip[i] = Integer.parseInt(st.nextToken())-1;
        visit = new boolean[N];
        visit[trip[0]]=true;
        dfs(trip[0]);
        if(end) System.out.println("YES");
        else System.out.println("NO");
        br.close();
    }
    static void dfs(int n) {
        if(end) return;
        while(trip[trip_idx]==n) {
            if(++trip_idx==M) {
                end = true;
                return;
            }
            visit = new boolean[N];
        }
        for(int j=0; j<N; j++) {
            if(visit[j]) continue;
            if(map[n][j]==1) {
                visit[j] = true;
                dfs(j);
            }
        }
    }
}
```
