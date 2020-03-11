---
layout: post
title:  "java tip"
subtitle:   "java tip"
categories: Study
tags: Algo
---

### sc.next() 
```
공백 이전까지 읽어들인다 -> 공백이 남는다.
```

### sc.nextLine() 
```
공백까지 읽어들이고 난 후 공백을 버리고 읽은 것을 출력해준다.
```

### int형을 String형으로 형변환(Wrapper클래스 안쓰고)
~~~ java
String str = 9 + ""; // 공백없이
~~~

### char형을 int형으로 형변환
~~~ java
for(int i=0 ;i<6; i++) {
  cardNum[i] = card.charAt(i) - '0';
}
~~~

### 오름차순 정렬(퀵정렬) 
~~~ java
Arrays.sort(arr);
~~~

### Java에서 random 수 뽑기 
~~~ java
(int)(Math.random()*30)+1; //0~30

Math.random(); //0.0000000~9.9999999
Math.random()*100; //0.00000~9.99999
~~~

### stack 요소별로 확인
~~~ java
stack.elementAt(idx);
~~~

###
