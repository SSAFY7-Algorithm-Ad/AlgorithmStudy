# ๐ 10775 (๊น๊ฐํธ)

## ์์์๊ฐ, ๋ฉ๋ชจ๋ฆฌ

204 ms, 22104 KB

## ํ์ด ๋ฐฉ๋ฒ

- ๊ทธ๋ฆฌ๋ํ ๋ฐฉ๋ฒ์ผ๋ก ๊ฐ๋ฅํ ํฐ๋ฒํธ์ ๊ณตํญ๋ถํฐ ์ ๊ทผํจ.
- ์ฒ์์ ๋ฒํธ๋ฅผ ํ๋์ฉ ์ค์ฌ๊ฐ๋ฉฐ ๋ชจ๋  ๊ฒฝ์ฐ์ ์๋ฅผ ์ ๊ทผํด์ ์๊ฐ์ด๊ณผ ๋ฐ์.
- Union & Find ํ์ฉํ์ฌ ์ ๊ทผํ  ์ ์๋ ๊ณตํญ์ ํฉ์ณ์ ๊ฒฝ์ฐ์ ์๋ฅผ ์ค์
- ์ฒซ๋ฒ์งธ ๊ณตํญ์ฒ๋ฆฌ ๋ฐ ๋ง์ง๋ง์ผ๋ก ์ ๊ทผ๊ฐ๋ฅํ ๊ณตํญ์ ์ฒ๋ฆฌํ๋ ๋ถ๋ถ์์ ํ๋ฆผ.
  - ๋จ์ํ root๋ฐฐ์ด์ด ๋ฐ๋ผ๋ณด๋ ๊ฐ์ด ์๋ find๋ฉ์๋๋ฅผ ์ฌ์ฉํ์ฌ ์ต์๋จ ๊ฐ์ ์ฐพ์์ ๋น๊ตํด์ผํจ

## Code

```Java
import java.io.*;
public class Main {
    static int[] root;
    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int G = Integer.parseInt(br.readLine());
        int P = Integer.parseInt(br.readLine());
        root = new int[G+1];
        for(int i=0; i<=G; i++) root[i] = i;
        int cnt = 0;
        for(int i=0; i<P; i++) {
            int g = Integer.parseInt(br.readLine());
            if(find(g) == 0) break;
            union(find(g),root[g]-1);
            cnt++;
        }
        System.out.println(cnt);
        br.close();
    }
    static void union(int a, int b) {
        int root_a = find(a);
        int root_b = find(b);
        if(root_a == root_b) return;
        root[a] = root_b;
    }
    static int find(int a) {
        if(root[a]==a) return a;
        return root[a] = find(root[a]);
    }
}
```
