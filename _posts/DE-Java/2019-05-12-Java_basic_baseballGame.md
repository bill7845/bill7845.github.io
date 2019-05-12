---
layout: post
title: Basic_BaseBallGame
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

<br>

# <center> BaseBall 게임 </center>
---

<br>

* __배열 활용__
* __랜덤수__

<br>

```java
public static void main(String[] args) {

		// 숫자 야구게임

		int baseball[] = new int[3];

		// 1.컴퓨터 랜덤 수 3개 만들기
		for (int i = 0; i < baseball.length; i++) {
			baseball[i] = (int) (Math.random() * 10);  // 랜덤메서드
			System.out.print(baseball[i]);
		}
		System.out.println();

		// ============================================================================================

		// 2. 사용자가 입력한 답을 answer 에 각각 담기;
		for (int n = 0; n < 10; n++) {
			Scanner input_user = new Scanner(System.in);
			System.out.println("숫자 3개 입력:( / / )");
			String user = input_user.next();
			StringTokenizer st = new StringTokenizer(user, "/");

			int answer[] = new int[3];
			for (int i = 0; st.hasMoreTokens(); i++) {

				answer[i] = Integer.parseInt(st.nextToken());
				System.out.print(answer[i]);

			}

			// ==============================================================================================
			// 3. baseball 배열과 answer 배열을 각각 비교



			int strike = 0, ball = 0;
			END: for (int j = 0; j < answer.length; j++) {
				if (answer[j] == baseball[j])  {
					strike++;
          // 이곳에 break if문 넣으면 왜 안되는가
				} else {
					ball++;
				}
				if (strike == 3) {  // if문을 위에 if문을 안넣은 이유??
					break END;
				}
			}
			System.out.println();
			System.out.printf("%d스트라이크 %d볼", strike, ball);
			System.out.println();
		}
	}

```
