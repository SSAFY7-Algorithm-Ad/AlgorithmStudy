# ๐ 1107 (๋ฐํ์ด)

## ์์์๊ฐ, ๋ฉ๋ชจ๋ฆฌ
- 14360 KB
- 128 ms

## ํ์ด ๋ฐฉ๋ฒ
- bfs๋ฅผ ์ฌ์ฉํ์ฌ ์ต์๋ก ์ด๋ํ๋ cnt๋ฅผ ๊ตฌํ๊ณ ์ ํ์ต๋๋ค.
- ๋นจ๊ฐ ๊ตฌ์ฌ๊ณผ ํ๋ ๊ตฌ์ฌ์ด ์์ง์ธ ์์น๋ฅผ ๊ฐ์ด ์ ์ฅํ๊ณ ์ ํด๋์ค๋ฅผ ํ๊บผ๋ฒ์ ๊ตฌํํ์ต๋๋ค.
- ์ ๋ ์  ํ์ผ๋ก ํ ์ ์๋ ๋ฌธ์ ๋ผ์ ๋ ๊ตฌ๊ธ๋ง์ ํด์ ํ์์ต๋๋ค. ๋ฉฐ์น  ๋ค์ ๋ค์ ํ๋ฒ ํ์ด๋ด์ผ๊ฒ ์ต๋๋ค.
- ๊ตฌํ ๋ฌธ์ ๋ฅผ ๋ง์ด ํ์ด์ผ๊ฒ ์ต๋๋ค..
- ๋๋์ฒด ์ด๊ฑฐ ๊ทธ๋ฅ ํธ์๋ ๋ถ์ .. ์ด๋ค ๋ถ์ด์ ์ง.. ๋๋จ..

## Code
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class DAY221107_BOJ13460_G1_๊ตฌ์ฌํ์ถ2 {
    static int N, M;
    static char[][] map;
    static Marble blue, red;
    static int hole_x, hole_y;
    static boolean[][][][] visited;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken()); // ์ธ๋ก
        M = Integer.parseInt(st.nextToken()); // ๊ฐ๋ก

        map = new char[N][M];
        visited = new boolean[N][M][N][M]; // ๋ฐฉ๋ฌธ ์ฒ๋ฆฌํ  ๋ฐฐ์ด์... 4์ฐจ์์ผ๋ก...

        // ๋ณด๋ ์ธํ
        for (int i = 0; i < N; i++) {
            String s = br.readLine();
            for (int j = 0; j < M; j++) {
                char c = s.charAt(j);
                map[i][j] = c;
                if (c == 'B') {
                    blue = new Marble(0, 0, i, j, 0);
                } else if (c == 'R') {
                    red = new Marble(i, j, 0, 0, 0);
                } else if (c == 'O') {
                    hole_x = i;
                    hole_y = j;
                }
            }
        }

        System.out.println(bfs());

        br.close();
    }

    // ์ ์ค ์ ์ผ
    static int[] dr = {-1, 0, 1, 0};
    static int[] dc = {0, 1, 0, -1};

    private static int bfs() {
        Queue<Marble> queue = new LinkedList<>();
        queue.add(new Marble(red.red_x, red.red_y, blue.blue_x, blue.blue_y, 1)); // cnt๋ฅผ 1์ ๋ฃ์ด์ฃผ๋ ์ด์ ๋?
        visited[red.red_x][red.red_y][blue.blue_x][blue.blue_y] = true;

        while (!queue.isEmpty()) {
            Marble marble = queue.poll();

            int curr_red_x = marble.red_x;
            int curr_red_y = marble.red_y;
            int curr_blue_x = marble.blue_x;
            int curr_blue_y = marble.blue_y;
            int curr_cnt = marble.cnt;

            if (curr_cnt > 10) return -1;

            for (int d = 0; d < 4; d++) {
                int new_red_x = curr_red_x;
                int new_red_y = curr_red_y;
                int new_blue_x = curr_blue_x;
                int new_blue_y = curr_blue_y;

                boolean isRedHole = false;
                boolean isBlueHole = false;

                // ๋นจ๊ฐ ๊ตฌ์ฌ ์ด๋
                // ์ด๋ํ ๊ณณ์ด #์ด ์๋๋ผ๋ฉด
                while (map[new_red_x + dr[d]][new_red_y + dc[d]] != '#') {
                    // ์์น ๊ฐฑ์ 
                    new_red_x += dr[d];
                    new_red_y += dc[d];

                    // ๊ทผ๋ฐ ๊ทธ ์์น๋ฅผ ๊ฐฑ์ ํ ๊ณณ์ด ๊ตฌ๋ฉ์ด๋ผ๋ฉด?
//                    if (map[new_red_x][new_red_y] == 'O') {
                    if (new_red_x == hole_x && new_red_y == hole_y) {
                        isRedHole = true;
                        break;
                    }
                }

                // ํ๋ ๊ตฌ์ฌ๋ ๋์์ ์ด๋ํ ๊ฑฐ๋๊น
                while (map[new_blue_x + dr[d]][new_blue_y + dc[d]] != '#') {
                    new_blue_x += dr[d];
                    new_blue_y += dc[d];

//                    if (map[new_blue_x][new_blue_y] == 'O') {
                    if (new_blue_x == hole_x && new_blue_y == hole_y) {
                        isBlueHole = true;
                        break;
                    }
                }

                if (isBlueHole) continue;

                if (isRedHole) return curr_cnt;

                // ๋๋ค ๊ตฌ๋ฉ์ ๋น ์ง์ง ์๊ณ  ์ด๋ํ๋๋ฐ ๊ทธ ์๋ฆฌ๊ฐ ๊ฒน์น๋ ๊ฒฝ์ฐ
                // ์์น ์กฐ์ ์ด ํ์ํจ
                if(new_red_x == new_blue_x && new_red_y == new_blue_y) {
                    // ์
                    if (d == 0) {
                        // ์ด๋ํ๊ธฐ ์ ์ ๋ ์์ ์๋ ๊ฒ ๋ ์์ ์๋๋ก ํด์ผ์ง
                        if (curr_blue_x < curr_red_x) {
                            new_red_x -= dr[d];
                        } else {
                            new_blue_x -= dr[d];
                        }
                    } else if (d == 1) { // ์ค๋ฅธ์ชฝ
                        // y๊ฐ์ด ๋ ํฐ๊ฒ ๋ ์ค๋ฅธ์ชฝ์ ์์ด์ผ ํจ
                        if (curr_blue_y > curr_red_y) {
                            new_red_y -= dc[d];
                        } else {
                            new_blue_y -= dc[d];
                        }
                    } else if (d == 2) { // ์๋
                        // ๊ฐ์ด ๋ ์์ ๊ฒ ๋ ์์ ์์ด์ผ ํจ
                        if (curr_red_x < curr_blue_x) {
                            new_red_x -= dr[d];
                        } else {
                            new_blue_x -= dr[d];
                        }
                    } else { // ์ผ์ชฝ
                        // y์ด ๊ฐ์ด ๋ ์์ ๊ฒ ๋ ์ผ์ชฝ์ ์์ด์ผํจ
                        // ํฐ ๊ฑธ ๋นผ์ผํจ
                        if (curr_red_y > curr_blue_y) {
                            new_red_y -= dc[d];
                        } else {
                            new_blue_y -= dc[d];
                        }
                    }
                }

                // ์์น ์กฐ์  ํ ์ด๋ํ ๊ณณ์ด ์ฒ์ ๋ฐฉ๋ฌธํ ๊ณณ์ด๋ผ๋ฉด ํ์ ๋ฃ๊ธฐ
                if (!visited[new_red_x][new_red_y][new_blue_x][new_blue_y]) {
                    visited[new_red_x][new_red_y][new_blue_x][new_blue_y] = true;
                    queue.add(new Marble(new_red_x, new_red_y, new_blue_x, new_blue_y, curr_cnt + 1));
                }

            }

        }
        // ์ด๋ ๊ฒ ํด๋ ์๋ฌด ๊ฒ๋ ์๋์?
        return -1;
    }
}

// Marble ํด๋์ค ํ๋์ ๋นจ๊ฐ ๊ณต, ํ๋ ๊ณต์ ์ขํ๋ฅผ ๋ชจ๋ ๋ด๋ ์ด์ ๋ ๋ญ๊น?
// ํ๋ฐฉ์ ์์ง์ด๋ ค๊ณ 
class Marble {
    int red_x;
    int red_y;
    int blue_x;
    int blue_y;
    int cnt;

    public Marble(int red_x, int red_y, int blue_x, int blue_y, int cnt) {
        this.red_x = red_x;
        this.red_y = red_y;
        this.blue_x = blue_x;
        this.blue_y = blue_y;
        this.cnt = cnt;
    }
}
```
