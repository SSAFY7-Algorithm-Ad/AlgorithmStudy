# ๐ 1744 (์ด์ฃผํฌ)

## ์์์๊ฐ, ๋ฉ๋ชจ๋ฆฌ
<img width="80%" alt="image" src="https://user-images.githubusercontent.com/83942393/209649509-34eb9f95-2c1c-4d23-a170-ea45983d0d76.png">

## ํ์ด ๋ฐฉ๋ฒ
๋ฌธ์  ์ ํ : ๊ทธ๋ฆฌ๋, ์ ๋ ฌ </br></br>
์ฒ์์ ์ ๋ ฌํด์ ํฐ ์๋ฅผ ๋๊ฐ์ฉ ๋ฌถ์ด์ ํธ๋ ๋ฐฉ๋ฒ์ ์๊ฐํ๋ค. ๊ทธ๋ฌ๋ค ๊ฑธ๋ฆฌ๋ ๊ฒ 0 ๊ณผ 1๊ณผ ์์๋ค์ด์๋ค. ์์์ธ ๊ฒฝ์ฐ์ ๋ฌด์กฐ๊ฑด ์์ ๋๋ 0 ๊ณผ ๊ณฑํด์ ์์์์ผ์ผ ํ๋ค. 1์ธ ๊ฒฝ์ฐ๋ ๊ณฑํ๋ ๊ฒ๋ณด๋ค
๋ํ๋ ๊ฒ ๋ ํฐ ์์ธ ๊ฒฐ๊ณผ๊ฐ์ด ๋์จ๋ค.
- ์์๋ฅผ ๋ด๋ ๋ฆฌ์คํธ์ ์์์ 0์ ํจ๊ป ๋ด๋ ๋ฆฌ์คํธ ๋ ๊ฐ๋ฅผ ๋ฐ๋ก ์ค๋นํด ๋ด๋๋ค.

## Code

```Java
import java.io.*;
import java.util.*;

public class Main_bj_1744_์๋ฌถ๊ธฐ {

	public static void main(String[] args) throws Exception {
//		System.setIn(new FileInputStream("res/input_bj_1744.txt"));
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		int N = Integer.parseInt(br.readLine());
		ArrayList<Integer> positive = new ArrayList<>();		// ์์๋ค๋ง ๋ชจ์๋์ ๋ฆฌ์คํธ
		ArrayList<Integer> negative = new ArrayList<>();		// ์์, 0 ์ ๋ชจ์๋์ ๋ฆฌ์คํธ
		
		for(int i=0; i<N; i++) {
			int a = Integer.parseInt(br.readLine());
			
			if(a>0) positive.add(a);
			else negative.add(a);
		}
		
		// ๋ด๋ฆผ์ฐจ์ ์ ๋ ฌ
//		Collections.sort(positive, Collections.reverseOrder());				1. Collections.reverseOrder ์ฌ์ฉ
		Collections.sort(positive, ((Integer o1, Integer o2) -> {return -(o1-o2);}));	// 2. ๋๋ค์ ์ฌ์ฉ
		
		Collections.sort(negative);		// ์ค๋ฆ์ฐจ์ ์ ๋ ฌ
		
		int ans = 0;
		
		for(int i=0; i<positive.size(); i++) {
			if((positive.get(i) == 1) || (i == positive.size()-1) || positive.get(i+1) == 1) {
				ans += positive.get(i);
			}
			else {
				ans += (positive.get(i) * positive.get(i+1));
				i++;
			}
		}
		
		for(int i=0; i<negative.size(); i++) {
			if(i == negative.size()-1) {
				ans += negative.get(i);
			}
			else {
				ans += (negative.get(i) * negative.get(i+1));
				i++;
			}
		}
		
		System.out.println(ans);
		br.close();
		
	}

}

```
