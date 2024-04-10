# DOM ?

DOM은 HTML 문서의 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API, 즉 프로퍼티와 메서드를 제공하는 트리 자료구조다.

---

# 1. 노드

## 1) HTML 요소와 노드 객체

![스크린샷 2024-04-10 오전 10.43.24.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/61e26085-91c6-4da4-94a0-7980ec6e4935/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_10.43.24.png)

![스크린샷 2024-04-10 오전 10.45.16.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/29966ceb-87fb-4815-9cbc-1167f50fb556/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_10.45.16.png)

- HTML 요소(HTML 문서를 구성하는 개별적인 요소)는 렌더링 엔진에 의해 파싱되어 DOM을 구성하는 노드 객체로 변환된다.
- HTML 요소들은 중첩 관계를 갖는데 이 관계에 의해 계층적인 부자 관계가 형성된다. → 트리 자료구조로 구성

### 트리 자료구조

- 노드들의 계층 구조로 이뤄진다.(부모노드, 자식노드로 구성)
- 최상위 노드(루트 노드): 부모 노드가 없다. 루트 노드는 0개 이상의 자식 노드를 갖는다.
- 리프 노드: 자식 노드가 없는 노드

**노드 객체들로 구성된 트리 자료구조를 DOM(DOM 트리)이라 한다.**

## 2) 노드 객체의 타입

노드 객체는 총 12개의 종류(노드 타입)가 있다. 이 중에서 중요한 타입은 다음 4가지다.

### 문서 노드

- DOM 트리 최상위에 존재하는 루트 노드로서 document 객체(브라우저가 렌더링한 HTML 문서 전체를 가리키는 객체 / `window.document`로 참조)를 가리킨다.
- 모든 자바스크립트 코드는 전역 객체 window의 document 프로퍼티에 바인딩되어있는 하나의 document 객체를 바라본다. 즉, HTML 문서당 document 객체는 유일하다.
- 문서도느(document 객체)는 DOM 트리의 노드들에 접근하기 위한 진입점 역할을 한다.

### 요소 노드

- HTML 요소를 가리키는 객체
- HTML 요소 간의 중첩에 의해 부자 관계를 가지며, 이를 통해 정보를 구조화
- 문서 구조를 표현

### 어트리뷰트 노드

- HTML 요소의 어트리뷰트를 가리킨다.
- 어트리뷰트 노드는 요소 노드에만 연결되어 있다.(부모 노드 X, 요소 노드의 형제 노드 X)
- 참조하거나 변경하려면 먼저 요소 노드에 접근해야 한다.

### 텍스트 노드

- HTML 요소의 텍스트를 가리키는 객체
- 문서의 정보를 표현
- 요소 노드의 자식 노드이며, 리프 노드 → DOM 트리의 최종단

## 3) 노드 객체의 상속 구조

DOM을 구성하는 노드 객체는 DOM API를 통해 자신의 부모, 형제, 자식을 탐색할 수 있으며 자신의 어트리뷰트와 텍스트를 조작할 수도 있다.

DOM을 구성하는 노드 객체는 ECMAScript 사양에 정의된 표준 빌트인 객체가 아니라 브라우저 환경에서 추가적으로 제공하는 **호스트 객체**다. 하지만 자바스크립트 객체인건 마찬가지이므로 프로토타입에 의한 상속 구조를 갖는다.

![스크린샷 2024-04-10 오전 11.00.37.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/8edbc0f2-2b7a-46dc-ba59-a552bf670c7d/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_11.00.37.png)

프로토타입 체인 관점에서 예시)

input 요소 파싱 → input 요소 노드 객체

![스크린샷 2024-04-10 오전 11.03.32.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/69ea86a1-8f84-47d7-b299-60cb67542dee/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_11.03.32.png)

![스크린샷 2024-04-10 오전 11.04.31.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/310bc438-e0a9-4384-a458-21a8795651c0/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_11.04.31.png)

- 이 input 요소 노드 객체는 HTMLInputElement, HTMLElement, Element, Node, EventTarget, Object의 prototype에 바인딩되어 있는 프로토타입 객체를 상속받는다.
- input 요소 노드 객체는 프로토타입 체인에 있는 모든 프로토타입의 프로퍼티나 메서드를 상속받아 사용할 수 있다.

노드 객체가 갖는 기능

- 노드 객체 공통 기능(이벤트 ← EventTarget 인터페이스가 제공 / 트리 탐색 기능 ← Node 인터페이스가 제공)
- 노드 타입에 따른 고유 기능

공통된 기능일수록 프로토타입 체인 상위에, 개별적인 고유 기능일수록 체인 하위에 체인을 구축

- **DOM은 HTML 문서의 계층적 구조와 정보를 표현하는 것은 물론 노드 객체의 종류, 즉 노드 타입에 따라 필요한 기능을 프로퍼티와 메서드의 집합인 DOM API로 제공한다. 이 DOM API를 통해 HTML의 구조나 내용 또는 스타일 등을 동적으로 조작할 수 있다.**

---

# 2. 요소 노드 취득

HTML의 구조나 내용 또는 스타일 등을 동적으로 조작하려면 먼저 요소 노드를 취득해야 한다.

## 1) id

- `Document.prototype.getElementById` 메서드는 id 값을 갖는 하나의(첫 번째) 요소 노드를 탐색하여 반환
- id 값은 HTML 문서 내에서 유일한 값이어야 하며, class 와 달리 공백 문자로 구분하여 여러개의 값을 가질 수 없다. 단, HTML 문서 내에 중복된 id 값을 HTML 요소가 여러 개 존재하더라도 에러 발생 X
- id 값을 갖는 HTML 요소가 존재하지 않는 경우 `null` 반환
- HTML 요소에 id를 부여하면 id 값과 동일한 이름의 전역 변수가 암묵적으로 선언되고 해당 노드 객체가 할당되는 부수 효과가 있다.
- id 값과 동일한 이름의 전역 변수가 이미 선언되어 있으면 이 전역 변수에 노드 객체가 재할당되지 않는다.

## 2) 태그 이름

- `Document.prototype` / `Element.prototype.getElementsByTagName` 메서드는 인수로 전달한 태그 이름을 갖는 모든 요소 노드들을 탐색하여 반환
    - `getElementsByTagName` 메서드는 여러 개의 노드 객체를 갖는 DOM 컬렉션 객체인 HTMLCollection 객체를 반환
    - HTMLCollection 객체는 유사 배열 객체이면서 이터러블이다.
- `Document.prototype.getElementsByTagName` 메서드는 DOM의 루트 노드인 문서 노드를 통해 호출하며 DOM 전체에서 요소 노드를 탐색하여 반환한다. 하지만 `Element.prototype.getElementsByTagName` 메서드는 특정 요소 노드를 통해 호출하며, 특정 요소 노드의 자손 노드 중에서 요소 노드를 탐색하여 반환한다.
- 인수로 전달된 태그 이름을 갖는 요소가 없는 경우 빈 HTMLCollection 객체 반환

## 3) class

- `Document.prototype` / `Element.prototype.getElementsByClassName` 메서드는 인수로 전달한 class 어트리뷰트 값을 갖는 모든 요소 노드들을 탐색하여 반환
- 인수로 전달할 class 값은 공백으로 구분하여 여러 개의 class를 지정할 수 있다.
- 나머지는 태그와 동일

## 4) CSS 선택자

CSS 선택자는 스타일을 적용하고자 하는 HTML 요소를 특정할 때 사용하는 문법이다.

- `Document.prototype` / `Element.prototype.querySelector`
    - 인수로 전달한 CSS 선택자를 만족시키는 하나의 요소 노드를 탐색하여 반환
    - 여러개인 경우 첫 번쨰 요소 노드만 반환
    - 노드가 존재하지 않는 경우 null 반환
    - 문법에 맞지 않는 경우 DOMException 에러 발생
- `Document.prototype` / `Element.prototype.querySelectorAll`
    - CSS 선택자를 만족시키는 모든 요소 노드를 탐색하여 반환
    - 요소가 존재하지 않는 경우 NodeList 객체를 반환
    - 문법에 맞지 않는경우 DOMException 에러 발생
    

## 5) 특정 요소 노드를 취득할 수 있는지 확인

`Element.prototype.matches` 메서드는 인수로 전달한 CSS 선택자를 통해 특정 요소 노드를 취득할 수 있는지 확인한다.

- 이벤트 위임을 사용할 때 유용

## 6) HTMLCollection과 NodeList

- DOM API가 여러 개의 결과값을 반환하기 위한 DOM 컬렉션 객체다.
- 둘 다 유사 배열 객체이면서 이터러블
- 중요 특징
    - 노드 객체의 상태 변화를 실시간으로 반영하는 살아 있는 객체다.
        - HTMLCollection은 언제나 live 객체로 동작한다.
        - NodeList는 대부분의 경우 노드 객체의 상태변화를 실시간으로 반영하지 않고 정적 상태를 유지하는 non-live 객체로 동작하지만 경우에 따라 live 객체로 동작한다.

### HTMLCollection

- `getElementsByTagName`, `getElementsByClassName` 메서드가 반환한다.
- 노드 객체의 상태를 실시간으로 반영하고 살아 있는 DOM 컬렉션 객체다.
- for 문으로 순회하면서 노드 객체의 상태를 변경해야 할 때 주의해야 한다.
    - 첫 번째 요소에 무언가를 적용하면 그 다음 요소가 첫 번째로 인식되는 문제
    - for문을 역방향으로 순회, while 문을 사용하여 HTMLCollection 객체에 노드 객체가 남아 있지 않을 때까지 무한 반복하는 방법으로 회피가능
    - 더 간단한 해결책은 HTMLCollection을 사용하지 않는 것이다. 차라리 `forEach`, `map`, `filter`, `reduce` 등의 고차 함수를 사용할 수 있다.

### NodeList

- HTMLCollection의 부작용을 해결하기 위해 `querySelectorAll` 메서드를 사용하는 방법도 있다.
- `querySelectorAll` 메서드는 DOM 컬렉션 객체인 NodeList 객체를 반환한다.
- **childNodes 프로퍼티가 반환하는 NodeList 객체는 HTMLCollection 객체와 같이 실시간으로 노드 객체의 상태 변경을 반영하는 live 객체로 동작하므로 주의가 필요하다.**
- **노드 객체의 상태 변경과 상관없이 안전하게 DOM 컬렉션을 사용하려면 HTMLCollection이나 NodeList 객체를 배열로 변환하여 사용하는 것을 권장한다.**

---

# 3. 노드 탐색

요소 노드를 취득한 다음, 취득한 요소 노드를 기점으로 DOM 트리의 노드를 옮겨 다니며 부모, 형제, 자식 노드 등을 탐색해야 할 때가 있다.

DOM 트리 상의 노드를 탐색할 수 있도록 Node, Element 인터페이스는 트리 탐색 프로퍼티를 제공한다.

![스크린샷 2024-04-10 오후 1.12.25.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/f8d54377-5796-456b-af97-4d566048e37b/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_1.12.25.png)

- `parentNode`, `previousSibling`, `firstChild`, `childNodes` 프로퍼티는 `Node.prototype`이 제공
- 프로퍼티 키에 Element가 포함된 `previousElementSibling`, `nextElementSibling`과 같은 children 프로퍼티는 `Element.protoype`이 제공
- 노드 탐색 프로퍼티는 모두 접근자 프로퍼티이다. (setter 없이 getter만 존재하여 참조만 가능한 읽기 전용 프로퍼티)

## 1) 공백 텍스트 노드

- HTML 요소 사이의 스페이스, 탭, 줄바꿈 등의 공백 문자는 텍스트 노드를 생성한다. 이를 공백 텍스트 노드라 한다.
- 노드를 탐색할 때 공백 텍스트 노드에 주의해야 한다.

## 2) 자식 노드 탐색

자식 노드를 탐색하기 위해서는 다음과 같은 노드 탐색 프로퍼티를 사용한다.

![스크린샷 2024-04-10 오후 1.16.26.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/0c751489-fb6a-4223-9773-47ae59750ed3/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_1.16.26.png)

![스크린샷 2024-04-10 오후 1.16.35.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/87e2ec28-88af-4cf3-8dea-90ddaef18aa5/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_1.16.35.png)

## 3) 자식 노드 존재 확인

- `Node.prototype.hasChildNodes` 메서드 사용
- boolean 형태로 반환

**자식 노드 중에 텍스트 노드가 아닌 요소 노드가 존재하는지 확인할땐?**

`children.length` 또는 Element 인터페이스의 `childElementCount` 사용

## 4) 요소 노드의 텍스트 노드 탐색

- 요소 노드의 텍스트 노드는 `firstChild` 프로퍼티로 접근할 수 있다.
- `firstChild` 프로퍼티는 첫 번째 자식 노드를 반환

## 5) 부모 노드 탐색

- `Node.prototype.parantNode` 프로퍼티 사용
- 텍스트 노드는 DOM 트리의 최종단 노드인 리프 노드이므로 부모 노드가 텍스트 노드인 경우는 없다.

## 6) 형제 노드 검색

- 부모 노드가 같은 형제 노드를 탐색하려면 다음과 같은 노드 탐색 프로퍼티를 사용한다.
- 아래 프로퍼티는 텍스트 노드 또는 요소 노드만 반환

![스크린샷 2024-04-10 오후 1.21.40.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/cfcb07c5-7f85-45ef-845e-624a47ed35af/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_1.21.40.png)

![스크린샷 2024-04-10 오후 1.21.48.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/a10a9ffb-32d1-4202-afbe-5133f32d3fac/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_1.21.48.png)

---

# 4. 노드 정보 취득

노드 객체에 대한 정보를 취득하려면 다음과 같은 노드 정보 프로퍼티를 사용한다.

![스크린샷 2024-04-10 오후 1.23.06.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/d6036921-6da9-43c4-93ce-90108d5b4701/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_1.23.06.png)

---

# 5. 요소 노드의 텍스트 조작

## 1) nodeValue

- `Node.prototype.nodeValue` 프로퍼티는 setter getter 모두 존재하는 접근자 프로퍼티 → 참조, 할당 모두 가능
- 노드 객체의 nodeValue 프로퍼티를 참조하면 노드 객체의 값을 반환
    - 노드 객체의 값이란? 텍스트 노드의 텍스트
- 텍스트 노드가 아닌 노드를 참조하면 `null` 반환
- 텍스트 노드의 nodeValue 프로퍼티에 값을 할당하면 텍스트를 변경할 수 있다.
    - 텍스트를 변경할 요소 노드를 취득한 다음, 취득한 요소 노드의 텍스트 노드를 탐색한다. 텍스트 노드는 요소 노드의 자식 노드이므로 `firstChild` 프로퍼티를 사용하여 탐색한다.
    - 탐색한 텍스트 노드의 nodeValue 프로퍼티를 사용하여 텍스트 노드의 값을 변경한다.

## 2) textContent

- `Node.prototype.textConent` 프로퍼티는 setter getter 모두 존재하는 접근자 프로퍼티 → 요소 노드의 텍스트와 모든 자손 노드의 텍스를 모두 취득하거나 변경
- 요소 노드의 textContent 프로퍼티를 참조하면 요소 노드의 콘텐츠 영역 내의 텍스트를 모두 반환
- 요소 노드의 textContent 프로퍼티에 문자열을 할당하면 요소 노드의 모든 자식 노드가 제거되고 할당한 문자열이 텍스트로 추가된다. 이때 할당한 문자열에 HTML 마크업이 포함되어 있더라도 문자열 그대로 인식되어 텍스트로 취급된다. 즉, HTML 마크업이 파싱되지 않는다.

---

# 6. DOM 조작

DOM 조작은 새로운 노드를 생성하여 DOM에 추가하거나 기존 노드를 삭제 또는 교체하는 것을 말한다. DOM 조작에 의해 DOM에 새로운 노드가 추가되거나 삭제되면 리플로우와 리페인트가 발생하는 원인이 되므로 성능에 영향을 준다. 따라서 복잡한 콘텐츠를 다루는 DOM 조작은 성능 최적화를 위해 주의해야 한다.

## 1) innterHTML

- `Element.prototype.innterHTML` 프로퍼티는 setter와 getter 모두 존재하는 접근자 프로퍼티 → 요소 노드의 HTML 마크업을 취득하거나 변경
- 요소 노드의 innerHTML 프로퍼티를 참조하면 요소 노드의 콘텐츠 영역 내에 포함된 모든 HTML 마크업을 문자열로 반환
- 요소 노드의 innerHTML 프로퍼티에 문자열을 할당하면 요소 노드의 모든 자식 노드가 제거되고 할당한 문자열에 포함되어 있는 HTML 마크업이 파싱되어 요소 노드의 자식 노드로 DOM에 반영된다.
- 단점
    - innerHTML 프로퍼티에 할당한 HTML 마크업 문자열은 렌더링 엔진에 의해 파싱되어 요소 노드의 자식으로 DOM에 반영된다. 이때 사용자로부터 입력받은 데이터를 그대로 innerHTML 프로퍼티에 할당하는 것은 **크로스 사이트 스크립팅 공격**에 취약하므로 위험하다.
    - innerHTML에 HTML 마크업 문자열을 할당하는 경우 요소 노드의 모든 자식 노드를 제거하고 할당한 HTML 마크업 문자열을 파싱하여 DOM을 변경한다는 것. → 유지되어도 좋은 기존의 자식 노드까지 모두 제거하고 다시 처음부터 새롭게 자식 노드를 생성하여 DOM에 반영한다.
    - 새로운 요소를 삽입할 때 삽입될 위치를 지정할 수 없다.

## 2) insertAdjacentHTML 메서드

- `Element.prototype.insertAdjacentHTML(position, DOMString)` 메서드는 기존 요소를 제거하지 않으면서 위치를 지정해 새로운 요소를 삽입
- 두 번째 인수로 전달한 HTML 마크업 문자열을 파싱하고 그 결과로 생성된 노드를 첫 번째 인수로 전달한 위치에 삽입하여 DOM에 반영
- 첫 번째 인수로 전달할 수 있는 문자열은 ‘beforebegin’, ‘afterbegin’, ‘beforeend’, ‘afterend’의 4가지다.

![스크린샷 2024-04-10 오후 2.33.21.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/daf408a7-068a-41f7-9e8f-234a20ca2967/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_2.33.21.png)

![스크린샷 2024-04-10 오후 2.33.13.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/d23aca55-6063-4327-8fc2-13ab460169c6/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_2.33.13.png)

- innerHTML 프로퍼티보다 효율적이고 빠르다.
- 하지만 크로스 사이트 스크립팅 공격에는 여전히 취약하다.

## 3) 노드 생성과 추가

DOM은 노드를 직접 생성/삽입/삭제/치환/하는 메서드도 제공한다.

### 요소 노드 생성

- `Document.prototype.createElement(tagName)` 메서드는 요소 노드를 생성하여 반환
- `createElement` 메서드의 매개변수 tagName에는 태그 이름을 나타내는 문자열을 인수로 전달
    
    ![스크린샷 2024-04-10 오후 2.37.50.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/43cfc678-67ff-4db1-a8ce-be977c0afd2e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_2.37.50.png)
    

![스크린샷 2024-04-10 오후 2.38.09.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/444db87a-9e00-40f2-858a-5ee87458c076/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_2.38.09.png)

- createElement 메서드는 요소 노드를 생성할 뿐 DOM에 추가하지는 않는다.(위 그림처럼 createElement 메서드로 생성한 요소 노드는 기존 DOM에 추가되지 않고 홀로 존재하는 상태다.) 따라서 이후에 생성된 요소 노드를 DOM에 추가하는 처리가 별도로 필요
- 생성한 요소 노드는 아무런 자식 요소도 가지고 있지 않다.

### 텍스트 노드 생성

- `Document.prototype.createTextNode(text)` 메서드는 텍스트 노드를 생성하여 반환
- 매개변수 text에는 텍스트 노드의 값으로 사용할 문자열을 인수로 전달

![스크린샷 2024-04-10 오후 2.41.23.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/c002b9a0-389d-43f6-8a46-a44cc408722e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_2.41.23.png)

- 요소 노드의 자식 노드로 추가되지 않고 홀로 존재하는 상태다.
- 텍스트 노드를 요소 노드에 추가하는 처리가 별도로 필요

### 텍스트 노드를 요소 노드의 자식 노드로 추가

- `Node.prototype.appendChild(childNode)` 메서드는 매개변수 childeNode에게 인수로 전달한 노드를 appendChild 메서드를 호출한 노드의 마지막 자식 노드로 추가한다.

![스크린샷 2024-04-10 오후 2.43.03.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/1f08159f-e1cd-407a-9ab9-a10a7f25973a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_2.43.03.png)

- 하지만 아직 기존 DOM에 추가되지 않은 상태

### 요소 노드를 DOM에 추가

- `Node.prototype.appendChild` 메서드를 사용하여 텍스트 노드와 부자 관계로 연결한 요소 노드를 요소 노드의 마지막 자식 요소로 추가한다.
    
    ![스크린샷 2024-04-10 오후 2.48.55.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/8c8f51a4-bea2-4825-87c8-0f472bfef68c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_2.48.55.png)
    

## 4) 복수의 노드 생성과 추가

- DocumentFragment 노드 사용
    
    ![스크린샷 2024-04-10 오후 2.57.33.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/03d07dab-3de8-4af8-bd96-ff5e818ae8d1/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_2.57.33.png)
    
    - 문서, 요소, 어트리뷰트, 텍스트 노드와 같은 노드 객체의 일종으로, 부모 노드가 없어서 기존 DOM과는 별도로 존재한다는 특징이 있다. → 자식노드를 추가해도 기존 DOM에는 어떠한 변경도 없다.
    - 자식 노드들의 부모 노드로서 별도의 서브 DOM을 구성하여 기존 DOM에 추가하기 위한 용도로 사용된다.
    - DocumentFragment 노드를 DOM에 추가하면 자신은 제거되고 자신의 자식 노드만 DOM에 추가된다.
- `Document.prototype.createDocumentFroagment` 메서드는 비어 있는 DocumentFragment 노드를 생성하여 반환
- 먼저 DocumentFragment 노드를 생성하고 DOM에 추가할 요소 노드를 생성하여  DocumentFragment 노드에 자식 노드로 추가한 다음, DocumentFragment 노드르 기존 DOM에 추가한다.
    - 이때 실제로 DOM 변경이 발생하는 것은 한 번뿐이며 리플로우와 리페인트도 한 번만 실행된다.

## 5) 노드 삽입

### 마지막 노드로 추가

- `Node.prototype.appendChild`
    - 인수로 전달받은 노드를 자신을 호출한 노드의 마지막 자식 노드로 DOM에 추가한다.

### 지정한 위치에 노드 삽입

- `Node.prototype.insertBefore(newNode, childNode)`
    - 첫 번째 인수로 전달받은 노드를 두 번째 인수로 전달받은 노드 앞에 삽입한다.
    - 두 번째 인수로 전달받은 노드는 반드시 `insertBefore` 메서드를 호출한 노드의 자식 노드여야한다.(아니라면 DOMException 에러 발생)
    - 두 번째 인수로 전달받은 노드가 null이면 첫 번째 인수로 전달받은 노드를 `insertBefore` 메서드를 호출한 노드의 마지막 자식 노드로 추가된다. 즉, `appendChild` 메서드처럼 동작한다.

### 노드 이동

- DOM에 이미 존재하는 노드를 `appendChild` 또는 `insertBefore` 메서드를 사용하여 DOM에 다시 추가하면 현재 위치에서 노드를 제거하고 새로운 위치에 노드를 추가한다.

### 노드 복사

- `Node.prototype.cloneNode([deep: true | false])`
    - 노드의 사본을 생성하여 반환한다.
    - 매개변수 `deep`에 `true`를 인수로 전달하면 노드를 깊은 복사하여 모든 자손 노드가 포함된 사본을 생성
    - `false`를 인수로 전달하면 노드를 얕은 복사하여 노드 자신만의 사본을 생성(자손 노드를 복사하지 않으므로 텍스트 노드도 없다.)

### 노드 교체

- `Node.prototype.replaceChild(newChild, oldChild)`
    - 자신을 호출한 노드의 자식 노드를 다른 노드로 교체한다.
    - 첫 번째 매개변수 `newChild`에는 교체할 새로운 노드를 인수로 전달하고, 두 번째 매개변수 `oldChild`에는 이미 존재하는 교체될 노드를 인수로 전달한다.

### 노드 삭제

- `Node.prototype.removeChild(child)`
    - `child` 매개변수에 인수로 전달한 노드를 DOM에서 삭제
    

---

# 7. 어트리뷰트

## 1) 어트리뷰트 노드와 attributes 프로퍼티

- HTML 문서의 구성 요소인 HTML 요소는 여러 개의 어트리뷰트를 가질 수 있다.
- HTML 요소의 동작을 제어하기 위한 추가적인 정보를 제공하는 HTML 어트리뷰트는 HTML 요소의 시작 태그에 `어트리뷰트 이름=”어트리뷰트 값”` 형식으로 정의한다.
    
    ![스크린샷 2024-04-10 오후 3.11.14.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/32e2a663-d3f2-4994-84b2-9f4fcf47df7e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_3.11.14.png)
    
- 글로벌 어트리뷰트와 이벤트 핸들러 어트리뷰트는 모든 HTML 요소에서 공통적으로 사용할 수 있다.
- 특정 HTML 요소에만 한정적으로 사용 가능한 어트리뷰트도 있다.(`type`, `value`, `checked` 등)
- HTML 문서가 파싱될 때 HTML 요소의 어트리뷰트는 어트리뷰트 노드로 변환되어 요소 노드와 연결된다.
    - 이때 HTML 어트리뷰트당 하나의 어트리뷰트 노드가 생성된다.
- 어트리뷰트 노드의 참조는 `NamedNodeMap` 객체에 담겨서 요소 노드의 `attributes` 프로퍼티에 저장된다.
    - 따라서 요소 노드의 모든 어트리뷰트 노드는 `Element.prototype.attributes` 프로퍼티로 취득할 수 있다.
    - `attributes` 프로퍼티는 읽기 전용 접근자 프로퍼티로, 모든 어트리뷰트 노드의 참조가 담긴 `NamedNodeMap` 객체를 반환한다.

## 2) HTML 어트리뷰트 조작

- `Element.prototype.getAttributes/setAttribute`
    - `attribute` 프로퍼티를 통하지 않고 요소 노드에서 메서드를 통해 직접 HTML 어트리뷰트 값을 취득하거나 변경할 수 있어 편리하다.
- `Element.prototype.hasAttribute(attributeName)`
    - 특정 HTML 어트리뷰트가 존재하는지 확인
- `Element.prototype.removeAttribute(attributeName)`
    - 특정 HTML 어트리뷰트 삭제

## 3) HTML 어트리뷰트 vs DOM 프로퍼티

- 요소 노드 객체에는 HTML 어트리뷰트에 대응하는 프로퍼티가 존재한다. 이 DOM 프로퍼티들은 HTML 어트리뷰트 값을 초기값으로 가지고 있다.
- DOM 프로퍼티는 setter getter 모두 존재하는 접근자 프로퍼티다. → 참조와 변경 가능

- HTML 어트리뷰트는 다음과 같이 DOM에서 중복 관리되고 있는 것처럼 보인다.
    - 요소 노드의 attributes 프로퍼티에서 관리하는 어트리뷰트 노드
    - HTML 어트리뷰트에 대응하는 요소 노드의 프로퍼티(DOM 프로퍼티)
- 하지만 HTML 어트리뷰트는 DOM에서 중복 관리되고 있지 않다

```jsx
- HTML 어트리뷰트의 역할

HTML 요소의 초기 상태를 지정하는 것
HTML 어트리뷰트 값은 HTML 요소의 초기 상태를 의미하며 이는 변하지 않는다.
```

- 요소 노드는 상태를 가지고 있다.
    - 사용자가 input 요소의 입력 필드에 “foo”라는 값을 입력했다면 input 요소 노드는 사용자의 입력에 의해 변경된 최신 상태(”foo”)를 관리해야 하는 것은 물론, HTML 어트리뷰트로 지정한 초기상태도 관리해야 한다.
    - 요소 노드는 2개의 상태, 즉 초기 상태와 최신 상태를 관리해야 한다. 요소 노드의 초기 상태는 어트리뷰트 노드가 관리하며, 요소 노드의 최신 상태는 DOM 프로퍼티가 관리한다.
    

### 어트리뷰트 노드

- **HTML 어트리뷰트로 지정한 HTML 요소의 초기 상태는 어트리뷰트 노드에서 관리한다.**
- `getAttribute`로 참조하거나, `setAttribute`로 초기값을 변경할 수 있다.

### DOM 프로퍼티

- **사용자가 입력한 최신 상태는 HTML 어트리뷰트에 대응하는 요소 노드의 DOM 프로퍼티가 관리한다. DOM 프로퍼티는 사용자의 입력에 의한 상태 변화에 반응하여 언제나 최신 상태를 유지한다.**
- 단, 모든 DOM 프로퍼티가 사용자의 입력에 의해 변경된 최신 상태를 관리하는 것은 아니다.
    - 사용자 입력에 의한 상태 변화와 관계있는 DOM 프로퍼티만 최신 상태 값을 관리한다.

### HTML 어트리뷰트와 DOM 프로퍼티의 대응 관계

- 대부분의 HTML 어트리뷰트는 HTML 어트리뷰트 이름과 동일한 DOM 프로퍼티와 1:1로 대응한다.
- 단, 다음과 같이 HTML 어트리뷰트와 DOM 프로퍼티가 언제나 1:1로 대응하는 것은 아니다.
    
    ![스크린샷 2024-04-10 오후 3.33.11.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/c2b77c72-4c29-4d0d-a985-202c7bb175ea/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_3.33.11.png)
    

### DOM 프로퍼티 값의 타입

- `getAttribute` 메서드로 취득한 어트리뷰트 값은 언제나 문자열인다.
- 하지만 DOM 프로퍼티로 취득한 최신 상태 값은 문자열이 아닐 수도 있다.
    - 예를 들어, checkbox 요소의 checked 어트리뷰트 값은 문자열이지만 checked 프로퍼티 값은 불리언 타입이다.
        
        ![스크린샷 2024-04-10 오후 3.34.27.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/580fab05-04d4-483e-afa4-952c205044ce/1bd270dd-0d35-4ab6-a35d-1d263f086526/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-04-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_3.34.27.png)
        

## 4) data 어트리뷰트와 dataset 프로퍼티

- `data` 어트리뷰트와 `dataset` 프로퍼티를 사용하면 HTML 요소에 정의한 사용자 정의 어트리뷰트와 자바스크립트 간에 데이터를 교환할 수 있다.
- `data` 어트리뷰트는 `data-user-id`, `data-role`과 같이 `data-` 접두사 다음에 임의의 이름을 붙여 사용한다.
- `data` 어트리뷰트의 값은 `HTMLElement.dataset` 프로퍼티로 취득할 수 있다.
    - `dataset` 프로퍼티는 HTML 요소의 모든 `data` 어트리뷰트의 정보를 제공하는 DOMStringMap 객체를 반환한다.
    - DOMStringMap 객체는 `data` 어트리뷰트의 `data-` 접두사 다음에 붙인 임의의 이름을 카멜 케이스로 변환한 프로퍼티를 가지고 있다.
- `data` 어트리뷰트의 `data-` 접두사 다음에 존재하지 않는 이름을 키로 사용하여 `dataset` 프로퍼티에 값을 할당하면 HTML 요소에 `data` 어트리뷰트가 추가된다.

---

# 8. 스타입

## 1) 인라인 스타일 조작

- [`HTMLElement.prototype.style`](http://HTMLElement.prototype.style)
    - setter와 getter 모두 존재하는 접근자 프로퍼티 → 요소 노드의 **인라인 스타일**을 취득하거나 추가 또는 변경한다.
    - style 프로퍼티를 참조하면 CSSStyleDeclaration 타입의 객체를 반환
        - CSSStyleDeclaration 객체는 다양한 CSS 프로퍼티에 대응하는 프로퍼티를 가지고 있다.
        - 이 프로퍼티에 값을 할당하면 해당 CSS 프로퍼티가 인라인 스타일로 HTML 요소에 추가되거나 변경된다.

## 2) 클래스 조작

- .으로 시작하는 클래스 선택자를 사용하여 CSS class를 미리 정의한 다음, HTML 요소의 `class` 어트리뷰트 값을 변경하여 HTML 요소의 스타일을 변경할 수도 있다.
- `class` 어트리뷰트에 대응하는 DOM 프로퍼티는 `class`가 아니라 `className`과 `classList`다.

### className

- Element.prototype.className
    - getter, setter 모두 존재하는 접근자 프로퍼티 → HTML 요소의 class 어트리뷰트 값을 취득하거나 변경
    - 요소 노드의 className 프로퍼티를 참조하면 class 어트리뷰트 값을 문자열로 반환
    - 문자열을 할당하면 class 어트리뷰트 값을 할당한 문자열로 변경

### classList

- Element.prototype.classList
    - class 어트리뷰트의 정보를 담은 DOMTokenList 객체를 반환
    
    ```jsx
    DOMTokenList
    
    - class 어트리뷰트의 정보를 나타내는 컬렉션 객체로서 유사 배열 객체이면서 이터러블이다.
    - 다음과 같은 유용한 메서드들을 제공한다.
    	- add(...className): 인수로 전달한 1개 이상의 문자열을 class 어트리뷰트 값으로 추가한다.
    	- remove(...className): 인수로 전달한 1개 이상의 문자열과 일치하는 클래스를 class 어트리뷰트에서 삭제한다. 일치하는 게 없으면 무시됨
    	- item(index): 인수로 전달한 index에 해당하는 클래스를 class 어트리뷰트에서 반환한다.
    	- contains(className): 인수로 전달한 문자열과 일치하는 클래스가 class 어트리뷰트에 포함되어 있는지 확인한다.
    	- replace(oldClassName, newClassName): 첫 번쨰 인수로 전달한 문자열을 두 번쨰 인수로 전달한 문자열로 변경한다.
    	- toggle(className[. force]): 인수로 전달한 문자열과 일치하는 클래스가 존재하면 제거하고, 존재하지 않으면 추가한다. 두 번째 인수로 불리언 값으로 평가되는 조건식을 전달할 수 있다. 조건식을 평가 결과가 true이면 class 어트리뷰트에 강제로 첫 번째 인수로 전달받은 문자열을 추가하고, false이면 class 어트리뷰트에서 강제로 첫 번째 인수로 전달받은 문자열을 제거한다.
    
    - 이 밖에도 DOMTokenList 객체는 forEach, entries, keys, values, supports 메서드를 제공한다.
    ```
    
    ## 3) 요소에 적용되어 있는 CSS 스타일을 참조
