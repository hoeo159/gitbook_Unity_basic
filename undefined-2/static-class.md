# static class

&#x20;gpt에게 코드를 추천받았을 때 static class를 보게 되었다. 대학 공부나 내가 공부를 했을 때 책에서는 보통 static을 잘 보지 못했다. 이론적으로 알고 있는 것은 static을 넣으면 변수나 함수 등이 원래 메모리 상의 위치와 다르게 스택이나 힙에 붙는 게 아니라 file data 영역에 나와서 프로그램 상에 시작이나 소멸 위치가 완전 다르다. 때문에 속도 향상에 도움이 되는 것으로 알고 있었다.

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption><p>사진 <a href="https://junghn.tistory.com/entry/%EC%BB%B4%ED%93%A8%ED%84%B0-%EA%B8%B0%EC%B4%88-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B5%AC%EC%A1%B0-%EC%8A%A4%ED%83%9DStack-%ED%9E%99Heap-%EB%8D%B0%EC%9D%B4%ED%84%B0Data%EC%98%81%EC%97%AD">출처</a></p></figcaption></figure>

&#x20;그렇다면 static class를 쓸 수 있는 기준이 어떻게 되는가??? 일단 C#을 기준으로 설명하자면 다음과 같은 기준점들이나 class의 방향성이 만족하면 고려할 수 있다.

* 인스턴스 마다 상태가 달라질 필요가 없다
  * 멤버 변수가 없거나 이전 호출 결과를 저장할 필요가 없다
* 외부 전역 변수 없이 입력이 명시적이다.
  * 예를 들어서 function(a, b)를 통해 a와 b를 매개 변수로 받는데
  * function()을 만들고 다른 인스턴스(Gamemanager.Instance.a)를 가져와서 읽으면 안된다
* 계산, 선택, 포맷, 변환 같은 간단하고 순진?한것들? 유틸리티 함수들??에 적합하다
  * 씬 오브젝트나 코루틴 등 같이 스마트 한 것들은 좀 생각을 하고 해야된다
* Enable 같은 [life cycle](event-functions.md)이 참여하지 않는다.
  * static은 수명 관리가 따로라서 캐시나 큐 등을 넣으면 이상해진다.
* multi thread나 동수 호출 문제를 만들지 않는다.
  * 속도를 빠르게 하려고 하는데 lock이 걸리거나 race condition이 걸리거나 등등,,,

&#x20;물론 static을 써거나 남발해도 요즘 컴파일러는 스마트해서 컴파일 단계에서 문제를 일으키진 않는데 속도가 저하되거나 static을 안쓰느니만 못하는 상황들이 나올 수 있기 때문에 주의를 해서 쓰면 좋은 문법인 것 같다. 또 static을 쓰면 사람들이 이 함수를 볼 때 아 이건 유틸 함수구나, instance가 없구나, 공유를 피하고 객체 생성을 줄여야 겠구나 하고 알려주는 역할도 한다고 한다. 참고로 instance가 없다, 의존하지 않는다는 것은 this에 의존하지 않는다고 또 생각하면 쉽게 이해할 수 있다.
