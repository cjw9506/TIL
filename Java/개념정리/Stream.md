# [Java8] Stream

-   **Stream이란?**
    
    Java8부터 추가된 Stream은 람다를 활용할 수 있는 기술이다. Java8 이전에는 배열 또는 컬렉션 인스턴스를 다루는 방법이 for문이나 foreach문을 활용하여 하나씩 꺼내서 다루었다. 간단한 경우엔 상관없지만 복잡해질수록 여러 로직이 섞이는 경우, 루프를 여러 번 도는 경우도 발생한다.
    
    Stream을 이용하면 배열 또는 컬렉션 인스턴스에 함수 여러개를 조합해서 원하는 결과를 필터링하고 가공된 결과를 얻을 수 있다. 또한, 코드의 양을 줄이고 간결하게 표현할 수 있다. 즉, 배열과 컬렉션을 함수형으로 처리할 수 있다.
    
---

-   **Stream의 특징**
    -   데이터를 담고 있는 저장소(컬렉션)이 아니다.
    -   스트림이 처리하는 데이터 소스를 변경하면 안된다.
    -   스트림으로 처리하는 데이터는 한번만 처리한다.
    -   **중개 오퍼레이션**은 근본적으로 **종료 오퍼레이션**이 오지 않으면 실행 X(종료 오퍼레이션이 없으면 무의미)
    -   손쉽게 병렬 처리할 수 있다.(parallelStream() -> 무조건 빠른건 아니다, 데이터가 너무 방대할 때 사용하는 것 추천!)
        
---

-   **중개 오퍼레이션과 종료 오퍼레이션**
    
```java
public class test {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>(); //리스트 추가
        names.add("jiwon");
        names.add("user1");
        names.add("user2");

        Stream<String> stream = names.stream().map(String::toUpperCase); 
        //리스트의 모든 값들을 대문자로 치환하는 로직
        //하지만, 위에 설명에서 봤듯이 리턴값이 Stream이고, 이는 종료 오퍼레이션이 있지 않으므로
        //실행되지 않고 무의미하다.
        //stream을 출력할 수 없다.
        
        List<String> list = names.stream().map(String::toUpperCase).collect(Collectors.toList());
        //뒤에 collect로 종료 오퍼레이션을 추가해줌. 리턴값이 List가 된 것을 볼 수 있다.
        //종료 오퍼레이션을 추가한 뒤 바뀐 값을 출력할 수 있다.
        for (String s : list) {
            System.out.println(s);
        }
    }
}
```

---

**<중개형 오퍼레이션 종류>**

1.  스트림 필터링 : filter(), distinct()
2.  스트림 변환 : map()
3.  스트림 제한 : limit()
4.  스트림 정렬 : sorted()
5.  스트림 연산 결과 확인 : peek()
6.  타입변환 : asLongStream(), boxed()
    
-   filter(), distinct()
    -   filter()는 스트림 요소마다 비교문을 만족하는 요소로 구성된 스트림을 반환(특정 조건에 맞는 값만 추리기 위한 용도)
    -   distinct()는 요소들의 중복을 제거하고 스트림을 반환
-   map()
    -   스트림의 각 요소마다 수행할 연산을 구현할 때 사용.
-   limit()
    -   스트림의 시작 요소로부터 인자로 전달된 인덱스 까지의 요소를 추출
-   skip()
    -   limit()과 반대로, 시작 요소로부터 전달된 인덱스 까지를 제외하고 스트림 생성
-   sorted()
    -   스트림 요소를 오름차순으로 정렬
-   peak()
    -   결과 스트림의 요소를 사용해 추가로 동작을 수행한다(스트림 연산 과정에서 중간 중간 결과를 확인할 때 사용할 수 있다.)
    -   이 자체로 종료 오퍼레이션이 아니기 때문에 종료 오퍼레이션이 호출되지 않으면 동작 X
        
---

**<종료형 오퍼레이션 종류>**

1.  요소의 출력 : forEach()
2.  요소의 소모 : reduce()
3.  요소의 검색 : findFirst(), findAny()
4.  요소의 검사 : anyMatch(), allMatch(), noneMatch()
5.  요소의 통계 : count(), min(), max()
6.  요소의 연산 : sum(), average()
7.  요소의 수집 : collect()
    
-   forEach()
    -   스트림의 요소들을 순환하면서 반복해서 처리해야 하는 경우 사용
-   reduce()
    -   map()과 비슷하게 동작하지만 누적연산이 이루어진다.
-   findFirst(), findAny()
    -   스트림에서 지정한 첫번째 요소를 찾는 메서드
    -   findFirst()는 stream(), findAny()는 parallelStream()에서 사용
-   anyMatch(), allMatch(), noneMatch()
    -   스트림의 요소중 특정 조건을 만족하는 요소를 검사하는 메서드
-   count(), min(), max()
    -   스트림의 원소들의 전체 개수, 최솟값, 최댓값을 구하기 위한 메서드
-   sum(), average()
    -   스트림 원소들의 합계나 평균을 구함
-   collect()
    -   스트림의 결과를 모으기 위한 메서드로 Collectors 객체에 구현된 방법에 따라 처리하는 메서드
