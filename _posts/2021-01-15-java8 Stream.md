---
title:  "java 8 Stream 이란?"


categories:
  - Blog
tags:
  - Blog
last_modified_at: 2019-04-13T08:06:00-05:00

---

## 스트림이란?

스트림은 자바8에 새롭게 추가된 기능으로, 선언형(sql같은 질의형)으로 데이터(컬렉션, 배열, 파일, iterate ...)를 처리할 수 있다.  
자바8의 함수형 패러다임의 시작으로 람다를 이용해 함수형으로 데이터 처리가 가능해졌다.


## 스트림과 컬렉션

스트림과 컬렉션 모두 연속된 요소 형식의 값을 저장하는 자료구조의 인터페이스를 제공한다. 둘다 연속된 자료를 처리하기 위해 만들어진 것이다.  
둘의 가장 큰 차이점은 이 데이터를 *언제* 계산하느냐 이다.  

**컬렉션**은 현재 자료구조가 포함하는 모든 값을 메모리에 저장하는 자료구조이기 때문에 어떤 계산을 한 값들을 저장하기 위해서는 **모든 요소들이 컬렉션에 추가되는 전에 미리 계산**이 되어야 한다. 또한 컬렉션 인터페이스를 사용하기 위해서는 **외부 반복**을 사용해서 사용자가 직접 요소를 반복해야 한다. (for-each 사용)

하지만 **스트림**은 이론적으로 요청할 때만 요소를 계산하는 고정된 자료구조이다. 그렇기 때문에 스트림에 요소를 추가하거나 제거하는 작업은 할 수 없다.(컬렉션은 가능) 그리고 내부반복을 사용하기 때문에 추출할 요소만 선언해주면 알아서 반복을 처리하게 된다.

```
List<String> names = Arrays.asList("jeong", "pro", "jdk", "java");
// 기존의 코딩 방식
long count = 0;
for (String name : names) {
    if (name.contains("o")) {
        count++;
    }
}
System.out.println("Count : " + count); // 2
 
// 스트림 이용한 방식
count = 0;
count = names.stream().filter(x -> x.contains("o")).count();
System.out.println("Count : " + count); // 2

```

어떠한 컬렉션(names)이 존재하고 그 컬렉션의 요소를 순회하면서 "o"가 포함된 요소의 개수를 구한다고 가정했을 때, 기존의 코드 방식은 
반복 순회를 위한 for문, 필터링을 위한 분기 if문이 사용되돼야 비로소 구할 수 있었던 반면,   
스트림을 이용하면 한줄의 코딩만으로 count값을 구할 수 있다. (count 선언, 출력을 제외하면)   
즉, 불필요한 코딩(for, if 문법)을 걷어낼 수 있고 직관적이기 때문에 가독성이 좋아진다.   
이게 Stream의 **장점**이자 **목적**이다.



