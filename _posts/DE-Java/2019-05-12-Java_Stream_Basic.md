---
layout: post
title: 입출력 Stream
comments: true
categories: [Development Environment/Java]
tags: [Java]
---
<br>

# <center> Stream </center>
---

<br>

* __Stream__


<br>

## 1. Stream?

<br>

_stream이란 자료의 입출력을 도와주는 중간 통로이다_
> 데이터를 읽어 들이는 __입력 스트림__(reader) 과 데이터를 보내는 __출력 스트림__(writer)으로 나눌 수 있다
> 또, 문자 단위로 처리하느냐 바이트 단위로 처리하느냐로 나눌 수 있다

<br>

![byteStream](./assets/img/byteStream.png)
![stringStream](./assets/img/byteStream.png)

<br>

1. 데이터를 생석 혹은 지정한다
2. 데이터에 맞는 스트림을 생성한다
3. 스트림 클래스의 메서드를 이용하여 데이터를 핸들링 한다

```java
import java.io.FileOutputStream;
import java.io.IOException;

public class OutputTestFirst
{
	public static void main( String args[] )
	{
		try // stream 예외처리 필수
		{
			FileOutputStream fos = new FileOutputStream("a.txt");	// 출력스트림, byte 스트림

			for( int ch = 'A'; ch <='Z'; ch++)
			{
				fos.write(ch);
			}

			fos.close();	// Stream Close

		}catch( IOException ex ){
			System.out.println("파일전송실패 :" + ex.toString() );
		}
	}
}
```
