# π 1976. μ¬ν κ°μ (μ΄μ£Όν¬)

## μμμκ°, λ©λͺ¨λ¦¬
**Floyd** </br>
<img width="80%" alt="image" src="https://user-images.githubusercontent.com/83942393/208032249-e1bcc4c2-4cbb-4fe8-87c1-b566a027150d.png">

**Union-Find** </br>
<img width="80%" alt="image" src="https://user-images.githubusercontent.com/83942393/208032051-72999950-4d53-4c35-9390-15dc771b85c5.png">
</br>

## νμ΄ λ°©λ²
* μ²μμ Floyd λ₯Ό μ¬μ©ν΄μ κ²½λ‘ μ¬λΆλ₯Ό νλ¨νλ€.
* Floyd μμ μΆλ°μ§μ λμ°©μ§κ° κ°λ€λ©΄ μ¬νμ΄ κ°λ₯ νλ€λ κ²μ νμνμ§ λͺ»ν΄μ νλ Έλ€.
* κ²μν΄λ³΄λ Union-Find λ₯Ό μ¬μ©ν΄μ λ§μ΄ νΌ κ² κ°μ Union-Find λ‘λ νμλ€.
* union ν  λ parent[x] = y; μμ x λ₯Ό xμ λΆλͺ¨λ‘ ν΄μΌ νλ κ²μμ μ‘°κΈ ν€λ§Έλ€.

## Code
**Floyd** </br>
```Java
import java.io.*;
import java.util.*;

public class Main_bj_1976_μ¬νκ°μ {

	public static void main(String[] args) throws Exception {
//		System.setIn(new FileInputStream("res/input_bj_1976.txt"));
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		int N = Integer.parseInt(br.readLine());
		int tripN = Integer.parseInt(br.readLine());
		
		int[][] graph = new int[N+1][N+1];
		
		final int INF = 987654321;
		
		StringTokenizer st;
		for(int i=1; i<=N; i++) {
			st = new StringTokenizer(br.readLine(), " ");
			for(int j=1; j<=N; j++) {
				graph[i][j] = Integer.parseInt(st.nextToken());
				if(i==j) graph[i][j] = 1; 		// μΆλ°μ κ³Ό λμ°©μ μ΄ κ°λ€λ©΄ ν­μ μ¬νμ΄ κ°λ₯ν¨
				if(graph[i][j] == 0) graph[i][j] = INF;
			}
		}
		
		// Floyd
		for(int k=1; k<=N; k++) {			// κ²½
			for(int i=1; i<=N; i++) {		// μΆ
				for(int j=1; j<=N; j++) {	// λ
					if(graph[i][j] > graph[i][k] + graph[k][j]) {
						graph[i][j] = graph[i][k] + graph[k][j];
					}
				}
			}
		}
		
		st = new StringTokenizer(br.readLine(), " ");
		int from = Integer.parseInt(st.nextToken());	// μ²« λ²μ§Έ μΆλ° λμ
		
		boolean isPossible = true;
		for(int i=1; i<tripN; i++) {
			int to = Integer.parseInt(st.nextToken());
			
			if(graph[from][to] >= INF) {
				isPossible = false;
				break;
			}
			from = to;
		}
		
		if(isPossible)
			System.out.println("YES");
		else
			System.out.println("NO");
		
		br.close();
	}

}

```
</br>

**Union-Find** </br>
```Java
import java.io.*;
import java.util.*;

public class Main_bj_1976_μ¬νκ°μ_sol2 {
	
	static int[] parent;

	public static void main(String[] args) throws Exception {
		System.setIn(new FileInputStream("res/input_bj_1976.txt"));
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		int N = Integer.parseInt(br.readLine());
		int tripN = Integer.parseInt(br.readLine());
		
		StringTokenizer st;
		parent = new int[N+1];		// λΆλͺ¨ λΈλλ₯Ό μ μ₯ν  λ°°μ΄
		for(int i=1; i<=N; i++)
			parent[i] = i;			// μκΈ° μμ μΌλ‘ μ΄κΈ°ν
		
		for(int i=1; i<=N; i++) {
			st = new StringTokenizer(br.readLine(), " ");
			for(int j=1; j<=N; j++) {
				int value = Integer.parseInt(st.nextToken());
				
				if(value == 1) {
					union(i, j);
				}
			}
		}
		
		st = new StringTokenizer(br.readLine(), " ");
		int from = Integer.parseInt(st.nextToken());
		
		boolean isPossible = true;
		for(int i=1; i<tripN; i++) {
			int to = Integer.parseInt(st.nextToken());
			
			if(findParent(from) != findParent(to)) {
				isPossible = false;
				break;
			}
			
			from = to;
		}
		
		if(isPossible) System.out.println("YES");
		else System.out.println("NO");
		
		br.close();
	}
	
	static int findParent(int n) {
		if(parent[n] == n) return n;
		return parent[n] = findParent(parent[n]);
	}
	
	static void union(int from, int to) {
		int fromParent = findParent(from);
		int toParent = findParent(to);
		
		if(fromParent == toParent) return;
		
		if(fromParent < toParent) parent[toParent] = fromParent;
		else parent[fromParent] = toParent;
	}
}

```
