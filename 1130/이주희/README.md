# ๐ 1130 (์ด์ฃผํฌ)

## ์์์๊ฐ, ๋ฉ๋ชจ๋ฆฌ
<img width="90%" alt="image" src="https://user-images.githubusercontent.com/83942393/207781286-3a969902-0737-41cf-ad0f-d252ff31c5da.png">

## ํ์ด ๋ฐฉ๋ฒ
๋ฌธ์  ์ ํ : ์ํ, ์์ ํ์ 

์๋ชป๋ ๋ฐฉ๋ฒ)
์์  ํ์์ผ๋ก ํ ๊ฒฝ์ฐ N๊ฐ์ ์ซ์๊ฐ ์ฐจ๋ก๋ก N-1 (์์ ์ ๋บ ๋๋จธ์ง) ๊ฐ์ ์ซ์๋ฅผ ํ์ํ๋ฉด์ ์์ ์ด ๋ฐฐ์์ธ์ง ํ์ธํ๋ค๋ฉด ์๊ฐ ๋ณต์ก๋ O(N^2)
N์ ์ต๋๊ฐ์ 10๋ง์ด๋ฏ๋ก N^2 ๋ผ๋ฉด 100์ต, 1์ต๋น 1์ด๊ฐ ๊ฑธ๋ฆฐ๋ค๋ฉด ์์ ์๊ฐ 10์ด -> ์ ํ ์๊ฐ 2์ด๋ฅผ ์ด๊ณผ

ํด๊ฒฐ ๋ฐฉ๋ฒ)
* ์ฝ์์ ๊ฐฏ์๋งํผ ๋จธ๋ฆฌ ํกํก ํ๋ฏ๋ก ์ฝ์์ ๊ฐฏ์ ๊ตฌํ๊ธฐ
* ๊ณ์ฐ ํ์๋ฅผ ์ค์ด๊ธฐ ์ํด ์ ๊ณฑ๊ทผ๊น์ง๋ง ํ์

## Code
```Java
import java.io.*;
import java.util.Arrays; 

public class Main_bj_1241_๋จธ๋ฆฌํกํก {

	public static void main(String[] args) throws Exception {
//		System.setIn(new FileInputStream("res/input_bj_1241.txt"));
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		int N = Integer.parseInt(br.readLine());
		int[] numbers = new int[N];
		int[] count = new int[1000001];
		
		for(int i=0; i<N; i++) {
			numbers[i] = Integer.parseInt(br.readLine());
			count[numbers[i]]++;
		}
		
		StringBuilder sb = new StringBuilder();
		for(int i=0; i<N; i++) {
			int ans = 0;
			
			// ์ฝ์์ ๊ฐฏ์๋งํผ ๋จธ๋ฆฌ ํกํก -> ์ฝ์ ๊ตฌํ๊ธฐ
			for(int j=1; j<=Math.sqrt(numbers[i]); j++) {
				if(numbers[i] % j == 0) {
					ans += count[j];
					
					if((numbers[i] / j) != j) {			// ์ ๊ณฑ๊ทผ์ธ ๊ฒฝ์ฐ ์ ์ธ(ex)1*1=1)
						ans += count[numbers[i] / j];
					}
				}
			}
			
			ans--;		// ์๊ธฐ ์์  ๊ฐฏ์ ๋นผ๊ธฐ
			sb.append(ans).append("\n");
		}
		
		System.out.println(sb.toString());
		br.close();
	}
}
```
