# π 10775

## μμμκ°, λ©λͺ¨λ¦¬
244ms, 23028KB

## νμ΄ λ°©λ²

κ·Έλ¦¬λ, μμ νμμΌλ‘ νλ©΄ 10^10 κ³μ°μ΄λΌ 100μ΄κ° κ±Έλ¦΄ μ μμ΄ union-findλ₯Ό μ΄μ©ν΄μ νμ μκ°μ μ€μ¬μΌ ν¨.

## Code

```java
/**
 * Union-findλ₯Ό μ΄μ©ν νμ΄
 */

package backjoon;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Q_10775_2 {
    public static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    public static int G, P, ans;
    public static int[] arr;

    public static void main(String[] args) throws NumberFormatException, IOException {
        G = Integer.parseInt(br.readLine());
        P = Integer.parseInt(br.readLine());
        arr = new int[G + 1];
        for (int i = 0; i < G + 1; i++) {
            arr[i] = i;
        }

        // λΉνκΈ° νλμ© λ€μ΄μ
        for (int i = 0; i < P; i++) {
            int g = Integer.parseInt(br.readLine());
            // λ§μ½ λ μ΄μ λ μ μλ κ³³μ΄ μλ€.
            int emptyGate = find(g);
            if (emptyGate == 0) {
                break;
            }

            // λ μ μλ€.
            ans++;
            // κ° μ΅μ ν
            union(emptyGate, emptyGate - 1);
        }

        System.out.println(ans);
    }

    private static int find(int x) {
        if (arr[x] == x) {
            return x;
        }

        return arr[x] = find(arr[x]);
    }

    private static void union(int x, int y) {
        int a = find(x);
        int b = find(y);

        if (a != b) {
            arr[x] = y;
        }
    }
}

```