# ๐ 10775 (์ด์ฃผํฌ)

## ์์์๊ฐ, ๋ฉ๋ชจ๋ฆฌ
<img width="80%" alt="image" src="https://user-images.githubusercontent.com/83942393/209319767-5f982f83-f667-4573-8ed5-3e77b581598a.png">

## ํ์ด ๋ฐฉ๋ฒ
๋ฌธ์  ์ ํ : ๊ทธ๋ฆฌ๋, ๋ถ๋ฆฌ ์งํฉ
- ์ต๋ํ ๋ง์ ๋นํ๊ธฐ๊ฐ ๊ฒ์ดํธ์ ๋ํนํ๊ธฐ ์ํด์  ๋ํนํ  ์ ์๋ ๊ฒ์ดํธ๋ค ์ค ํฐ ๋ฒํธ์ ๋ํนํด์ผ ํจ -> ๊ทธ๋ฆฌ๋
- ๋ํนํ  ์ ์๋ ๊ฒ์ดํธ๋ฅผ ์ฐพ๊ธฐ ์ํด์ ๋ฐ๋ณต์ ์ผ๋ก ๋ค์์๋ถํฐ ํ์ํ๋ฉด ์๊ฐ ๋ณต์ก๋ ์ฆ๊ฐ -> ๋น์ด์ ธ ์๋ ๊ฒ์ดํธ ๋ฒํธ๋ฅผ parent ๋ฐฐ์ด์ ์๋ฐ์ดํธ -> union-Find ์ด์ฉ

## Code

```Java
import java.io.*;
import java.util.*;

public class Main_bj_10775_๊ณตํญ {
	
	static int[] parent;

	public static void main(String[] args) throws Exception {
//		System.setIn(new FileInputStream("res/input_bj_10775.txt"));
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		int G = Integer.parseInt(br.readLine());
		int P = Integer.parseInt(br.readLine());
		
		parent = new int[G+1];
		for(int i=1; i<=G; i++)
			parent[i] = i;			// ์๊ธฐ ์์ ์ผ๋ก ์ด๊ธฐํ
		
		int ans = 0;
		for(int i=0; i<P; i++) {
//			for(int j=1; j<=G; j++) {
//				System.out.print(parent[j] + " ");
//			}
//			System.out.println();
			
			int g = Integer.parseInt(br.readLine());
			int p = findParent(g);
			
			if(p == 0) break;
			else {
				union(p-1, p);
				ans++;
			}
		}
		
		System.out.println(ans);
		br.close();
	}
	
	static int findParent(int a) {
		if(parent[a] == a) return a;
		return parent[a] = findParent(parent[a]);
	}
	
	static void union(int a, int b) {
		int pa = findParent(a);
		int pb = findParent(b);
		
		parent[pb] = pa;
	}

}

```
