# π 1031 (λ°νμ΄)

## μμμκ°, λ©λͺ¨λ¦¬
- 62960 KB
- 808 ms

## νμ΄ λ°©λ²
- λ€μ΅μ€νΈλΌμ νλ‘μ΄λ μμμ λν΄ λ€μ κ³΅λΆνμ΅λλ€.
- ν΄λΉ λ¬Έμ μ κ°μ κ²½μ°μλ ν μμμ μμ λ€λ₯Έ νΉμ  μ§μ κΉμ μ΅λ¨ κ²½λ‘/κΈΈμ΄λ₯Ό κ³μ°νλ κ²μ΄ μλ λͺ¨λ  μ§μ μμ λͺ¨λ  μ§μ κΉμ§μ μ΅λ¨ κΈΈμ΄λ₯Ό μμμΌ νλ λ¬Έμ μκΈ°μ νλ‘μ΄λ μμλ‘ νμ΄μΌ νλ€λ κ²μ μμμ΅λλ€.
- μ¬κΈ°μ ν΅μ¬ λΌλ¦¬λ iμμ jλ‘ κ°λ kλ₯Ό κ±°μ³ κ°λ κ²κ³Ό λ°λ‘ κ°λ κ² μ€ μ΅μκ°μΌλ‘ κ°±μ νλ κ²μ΄λΌκ³  μκ°ν©λλ€. (μ΄ κ³Όμ μμ 3μ€ ν¬λ¬Έμ΄ λμμ μκ° λ³΅μ‘λκ° N^3)
- νμ΄ λ°©λ²μ κ°λ΅ν μ½λμ ν¨κ» μ£ΌμμΌλ‘ μμ±νμμ΅λλ€.

## Code
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class DAY221031_BOJ1956_G4_μ΄λ {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        // 1. μλ ₯
        int V = Integer.parseInt(st.nextToken()); // λ§μ
        int E = Integer.parseInt(st.nextToken()); // λλ‘

        int[][] map = new int[V + 1][V + 1];

        int INF = 987654321;

        // μΌλ¨ μκΈ°μμ μΌλ‘ κ°λ κ±° λΉΌκ³  λ¬΄νμΌλ‘ μ€μ 
        for (int i = 1; i <= V; i++) {
            for (int j = 1; j <= V; j++) {
                if (i == j) continue;
                map[i][j] = INF;
            }
        }

        // μ΄μ  μλ ₯ λ°κΈ°
        for (int i = 0; i < E; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());

            map[a][b] = c;
        }

        // 2. μ΄μ  λͺ¨λ  μ§μ μμ λ€λ₯Έ λͺ¨λ  μ§μ κΉμ§μ μ΅λ¨ κ²½λ‘λ₯Ό κ΅¬ν΄μΌ νλ€
        // λΌλ¦¬ : [i][j] = min ([i][j], [i][k] + [k][j] λ‘ μ΅λ¨ κ²½λ‘ κ°±μ 
        for (int k = 1; k <= V; k++) {
            for (int i = 1; i <= V; i++) {
                for (int j = 1; j <= V; j++) {
                    map[i][j] = Math.min(map[i][j], map[i][k] + map[k][j]);
                }
            }
        }

        // 3. μ΄μ  λ¬Έμ μμ μκ΅¬νλ λ΅μ κ΅¬νκΈ°
        // μ¬μ΄ν΄μ μ΄λ£¨λ λλ‘ μ€ κΈΈμ΄μ ν©μ΄ μ΅μμΈ κ²
        int ans = INF;

        // μ¬μ΄ν΄μ΄ μλ€λ κ² : [i][j]κ° λ¬΄νμ΄ μλκ³  [j][i]κ° λ¬΄νμ΄ μλλ©΄ λ¨
        for (int i = 1; i <= V; i++) {
            for (int j = 1; j <= V; j++) {
                if (i == j) continue; // μλ λ¬΄μ‘°κ±΄ 0μ΄λκΉ

                if (map[i][j] != INF && map[j][i] != INF) {
                    ans = Math.min(ans, map[i][j] + map[j][i]);
                }
            }
        }

        // 4. μΆλ ₯
        // μ€μ : μ¬μ΄ν΄μ΄ μμ λλ -1μ μΆλ ₯νλΌκ³  ν κ²μ λμ³€λ€.
        ans = (ans == INF) ? -1 : ans;
        System.out.println(ans);
    }
}

```
