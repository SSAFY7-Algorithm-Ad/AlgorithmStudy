# ๐ 2448 (์ด์ฃผํฌ)

## ์์์๊ฐ, ๋ฉ๋ชจ๋ฆฌ
<img width="70%" alt="image" src="https://user-images.githubusercontent.com/83942393/208051673-96f2ea7d-b79d-4d20-8465-2b78b2040be5.png">

## ํ์ด ๋ฐฉ๋ฒ
- ๊ฐํธ๋๊บผ ๋ณด๊ณ  ํ์์ต๋๋ค^-^b
- k=0 (N=3) ์ผ ๋ ๊ธฐ๋ณธ ๋ธ๋ก
```
  *  
 * *
*****
```
- ๊ท์น์ ์ฐพ์๋ฉด ํฌ๊ฒ 2์ค๋ก ๊ตฌ๋ถ๋จ
- ์ฒซ ๋ฒ์งธ ์ค์ ์ค์์ ํ ๊ฐ์ ๋ธ๋ก, ๋ ๋ฒ์งธ ์ค์ ๋น์นธ์ ์ฌ์ด์ ๋ ๋ ๊ฐ์ ๋ธ๋ก

```
     *        
    * *        
   *****     
  *     *    
 * *   * *  
***** *****
```
- ๋ ๋ฒ์งธ ์ค์ ๋ธ๋ก์ ํ ๊ฐ ์ฝ์ํ๊ณ , ๋น์นธ ์ฝ์ํ๊ณ , ๋ธ๋ก ํ ๊ฐ ์ฝ์
- ์ฒซ ๋ฒ์จฐ ์ค์ ๋ธ๋ก์ ์ค์์ ๋๊ธฐ ์ํด ๋ธ๋ก ์๊ณผ ๋ค์ ๋น์นธ์ ์ฝ์ (๋น์นธ์ ์ = N/2๊ฐ)
- ํ์ฌ ๋ง๋ค์ด์ง ์ ์ฒด ๊ทธ๋ฆผ์ด ๋ค์ ์ฌ๊ท์์ ํ ๊ฐ์ ๋ถ๋ถ ๋ถ๋ก์ด ๋๋ค.

## Code

```Java
import java.io.*;
import java.util.*;

public class Main_bj_2448_๋ณ์ฐ๊ธฐ11 {
	static int N;
	
	public static void main(String[] args) throws Exception {
		Scanner sc = new Scanner(System.in);
		N = Integer.parseInt(sc.next());
		StringBuilder[] sb = new StringBuilder[N];
		for(int i=0; i<N; i++)
			sb[i] = new StringBuilder();
		sb[0].append("  *  ");
		sb[1].append(" * * ");
		sb[2].append("*****");
		
		if(N>3) sb = star(1, sb);
		
		for(int i=0; i<N; i++)
			System.out.println(sb[i]);
		sc.close();
	}
	
	static StringBuilder[] star(int k, StringBuilder[] sb) {
		int n = (int) (3 * Math.pow(2, k));
		if(n<=N) {
			int idx = 0;
			for(int i=n/2; i<n; i++) {
				sb[i].append(sb[idx]).append(" ").append(sb[idx++]);
			}
			
			StringBuilder sbb = new StringBuilder();
			for(int i=0; i<n/2; i++)
				sbb.append(" ");
			
			for(int i=0; i<n/2; i++) {
				sb[i].insert(0, sbb);
				sb[i].append(sbb);
			}
			
			return star(k+1, sb);
		}
		
		return sb;
	}

}
```
