---
layout: post
title:  "Maaaaaaaaaze"
subtitle:   "16985"
categories: Algorithm
tags: BOJ
---

## 백준 [16985] Maaaaaaaaaze
[문제보기](https://www.acmicpc.net/problem/16985) <br>
![Alt text](/assets/img/baekjoon/16985.JPG)

### 풀이
- 판돌리기 : DFS
- 판의순서 : 순열
- 미로찾기 : BFS

### 소스코드
~~~ java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
	static int ans;
	static int[][][] maze;
	static int[] dx = { 0, 0, -1, 1, 0, 0 };
	static int[] dy = { 0, 0, 0, 0, -1, 1 };
	static int[] dz = { -1, 1, 0, 0, 0, 0 };

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		ans = 987654321;
		maze = new int[5][5][5];

		for (int i = 0; i < 5; i++) {
			for (int j = 0; j < 5; j++) {
				StringTokenizer st = new StringTokenizer(br.readLine());
				for (int k = 0; k < 5; k++) {
					maze[i][j][k] = Integer.parseInt(st.nextToken());
				}
			}
		}

		turnMaze(0);
		if (ans == 987654321) {
			ans = -1;
		}
		System.out.println(ans);
	}

	public static void turnMaze(int idx) {
		if (idx >= 5) {
			orderMaze(new int[] { 0, 1, 2, 3, 4 }, 0);
			return;
		}

		// 4번 돌리면 원래대로 돌아오므로 백트래킹해주지않아도된다.
		for (int i = 0; i < 4; i++) {
			turn(idx);
			turnMaze(idx + 1);
		}
	}

	// 판돌리기
	public static void turn(int idx) {
		int[][] newMaze = new int[5][5];
		int r = 0;
		int c = 4;
		for (int i = 0; i < 5; i++) {
			for (int j = 0; j < 5; j++) {
				newMaze[r][c] = maze[idx][i][j];
				r++;
				if (r >= 5) {
					c--;
					r = 0;
				}
			}
		}
		maze[idx] = newMaze;
	}

	// 판 순서
	public static void orderMaze(int[] arr, int idx) {
		if (idx >= 5) {
			int[][][] realMaze = new int[5][5][5];
			for (int i = 0; i < 5; i++) {
				realMaze[i] = maze[arr[i]];
			}

			if (realMaze[0][0][0] != 0 && realMaze[4][4][4] != 0) {
				go(realMaze);
			}
			return;
		}

		for (int i = idx; i < 5; i++) {
			swap(arr, idx, i);
			orderMaze(arr, idx + 1);
			swap(arr, idx, i);
		}
	}

	public static void swap(int[] arr, int idx, int i) {
		int tmp = arr[idx];
		arr[idx] = arr[i];
		arr[i] = tmp;
	}

	// bfs
	public static void go(int[][][] realMaze) {
		boolean[][][] v = new boolean[5][5][5];
		Queue<int[]> queue = new LinkedList<>();
		queue.add(new int[] { 0, 0, 0, 0 });
		v[0][0][0] = true;

		while (!queue.isEmpty()) {
			int[] q = queue.poll();
			if (q[3] >= ans)
				continue;
			if (q[0] == 4 && q[1] == 4 && q[2] == 4) {
				ans = Math.min(ans, q[3]);
				if (ans == 12) {
					System.out.println(12);
					System.exit(0);
				}
			}

			for (int i = 0; i < 6; i++) {
				int z = q[0] + dz[i];
				int x = q[1] + dx[i];
				int y = q[2] + dy[i];

				if (isRange(z, x, y) && !v[z][x][y] && realMaze[z][x][y] == 1) {
					v[z][x][y] = true;
					queue.add(new int[] { z, x, y, q[3] + 1 });
				}
			}
		}
	}

	public static boolean isRange(int z, int x, int y) {
		return z >= 0 && x >= 0 && y >= 0 && z < 5 && x < 5 && y < 5;
	}
}
~~~
