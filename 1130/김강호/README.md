# π 1241 (κΉκ°νΈ)

## μμμκ°, λ©λͺ¨λ¦¬

400 ms, 28708 KB

## νμ΄ λ°©λ²

- μμλ₯Ό νλ³ν λ λͺ¨λ  μλ₯Ό νμνμ§ μκ³ , μ κ³±κ·Ό κ°κΉμ§λ§ νμνμ¬ ν΄κ²°

## Code

```Java
import java.io.*;
public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int N = Integer.parseInt(br.readLine());
        int[] arr = new int[N];
        int[] cnt = new int[1000001];
        int[] res = new int[N];
        for(int i=0; i<N; i++) {
            arr[i] = Integer.parseInt(br.readLine());
            cnt[arr[i]]++;
        }
        for(int i=0; i<N; i++) {
            for(int j=1; j*j<=arr[i]; j++) {
                    if(arr[i]%j==0) {
                        res[i] += cnt[j];
                        if(arr[i]/j!=j) res[i] += cnt[arr[i]/j];
                }
            }
        }
        for(int i=0; i<N; i++) sb.append(res[i]-1).append('\n');
        System.out.println(sb);
        br.close();
    }
}
```
