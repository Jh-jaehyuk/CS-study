
## Vue.js 라이프사이클 알아야 하는 이유
1. **성능 최적화**: 불필요한 작업을 피하고, 필요한 시점에만 데이터를 가져오거나 이벤트 리스너를 설정함으로써 성능을 최적화할 수 있습니다.
2. **비동기 작업 처리**: 데이터 요청이나 타이머와 같은 비동기 작업을 라이프 사이클 훅에서 처리하면, 컴포넌트가 마운트 되거나 업데이트될 때 적절한 시점에 작업을 수행할 수 있습니다.
3. **코드 구조화**: 코드의 구조를 더 명확하게 하고, 각 훅에 맞는 로직을 분리하여 가독성을 높일 수 있습니다.
---

## 가이드 라인
**굵은 글씨**로 표현한 것들은 추가 설명이 있습니다.

---
## Vue.js 라이프사이클

Vue.js의 라이프사이클은 **인스턴스**나 **컴포넌트**가 생성되고 소멸되는 과정

라이프사이클이란 예를 들면 차량을 운행하기 위한 과정

---
### 인스턴스란 무엇인가?
**인스턴스**는 **데이터**, **메서드**, **라이프사이클 훅** 등등을 포함하며, Vue의 반응성을 제공하여 데이터가 변경될 때 **DOM**을 자동으로 업데이트합니다.

#### 인스턴스 자세히 보기
- **데이터 (data)**: Vue 인스턴스의 상태를 정의하는 객체입니다. 이 데이터는 컴포넌트의 템플릿에서 바인딩되어 사용됩니다.
```
  data () {
    return {
      //
    }
  },
```
- **메서드 (methods)**: 인스턴스에서 사용할 수 있는 함수들을 정의합니다. 이 메서드는 이벤트 핸들러나 데이터 조작에 사용됩니다.
```
  methods: {
    openLink() {
      console.log('openLink 함수 호출됨!');
    },
  },
```
- **계산된 속성 (computed)**: 데이터에 기반하여 계산된 값을 반환하는 속성입니다. 데이터가 변경될 때 자동으로 업데이트됩니다.
- **감시자 (watch)**: 특정 데이터 속성을 감시하고, 해당 속성이 변경될 때 특정 작업을 수행할 수 있도록 설정합니다.
- **라이프사이클 훅 (lifecycle hooks)**: 인스턴스의 생명주기 동안 특정 시점에 호출되는 메서드입니다. 예를 들어, created, mounted, updated, destroyed 등이 있습니다.
```
  mounted() {
    this.clientId = process.env.VUE_APP_GOOGLE_CLIENT_ID;
    console.log('Client ID:', this.clientId);
  },
```
- **템플릿 (template)**: Vue 인스턴스의 HTML 구조를 정의하는 부분으로, 데이터 바인딩과 디렉티브를 사용하여 동적으로 내용을 렌더링합니다.
- **이벤트 (event)**: DOM 이벤트를 처리하기 위한 메서드와 바인딩을 설정할 수 있습니다.
- **프로퍼티 (props)**: 부모 컴포넌트로부터 자식 컴포넌트로 전달되는 데이터입니다.
- **상태 관리 (store)**: Vuex와 같은 상태 관리 라이브러리와 함께 사용할 수 있으며, 애플리케이션의 전역 상태를 관리합니다.

**DOM이란 무엇인가?**
Document Object Model의 약자로, **웹 페이지의 구조를 표현하는 객체 모델**입니다.

**웹 페이지의 구조를 표현하는 객체 모델이란?**
```
객체 모델 (DOM 트리):
                - div (id="app")
                  |- h1
                  |   |- TextNode("안녕하세요!")
                  |- p
                      |- TextNode("이것은 Vue.js 애플리케이션입니다.")
```
위 구조는 실제로 브라우저 메모리에 있는 DOM(Document Object Model) 트리를 표현합니다. 이것이 바로 "웹 페이지의 구조를 표현하는 객체 모델"입니다. 각 줄은 DOM 노드를 나타내며, 이 노드들은 JavaScript를 통해 접근하고 조작할 수 있는 객체입니다.

DOM 트리가 만들어지는게 렌더링 과정
```
렌더링된 HTML:
<div id="app">
  <h1>안녕하세요!</h1>
  <p>이것은 Vue.js 애플리케이션입니다.</p>
</div>
```
이 HTML은 DOM 트리가 브라우저에 의해 렌더링된 결과입니다. 이는 실제로 사용자가 웹 페이지에서 보게 되는 내용입니다.

```
렌더링 과정을 단계별로 설명하면:

1. Vue.js 컴포넌트의 템플릿이 처리됩니다.
2. 템플릿은 가상 DOM(Virtual DOM)으로 변환됩니다.
3. 가상 DOM은 실제 DOM 트리로 변환됩니다 (위에서 본 객체 모델).
4. 브라우저는 이 DOM 트리를 해석하여 HTML로 렌더링합니다.
5. 렌더링된 HTML이 화면에 표시됩니다.
```
**DOM 객체 모델을 통해 우리가 할 수 있는 것들:**
- **요소 접근**: HTML 요소에 접근하고 수정할 수 있습니다.
- **이벤트 처리**: 사용자 인터페이스에서 발생하는 이벤트(클릭, 키 입력 등)를 처리할 수 있습니다.
- **동적 변경**: 페이지 내용을 동적으로 변경하거나 업데이트할 수 있습니다.
  - 사용자가 "좋아요" 버튼을 클릭하면 해당 버튼의 텍스트가 "좋아요 취소"로 바뀌거나, 좋아요 수가 증가하는 경우
---
### 컴포넌트란 무엇인가?
Vue에서 컴포넌트는 재사용 가능한 UI의 독립적인 조각을 의미합니다. 컴포넌트는 HTML, CSS, JavaScript를 하나의 단위로 묶어서 구성할 수 있으며, 다음과 같은 특징이 있습니다.

- **재사용성**: 한 번 정의된 컴포넌트는 여러 곳에서 재사용할 수 있습니다.
- **독립성**: 각 컴포넌트는 자신의 데이터와 로직을 가지고 있어, 다른 컴포넌트와 독립적으로 동작합니다.
- **조합 가능성**: 여러 개의 컴포넌트를 조합하여 복잡한 UI를 만들 수 있습니다.
---

![Vue.js 라이프사이클](https://storage.googleapis.com/blogcreator-6109.appspot.com/posts/25/56b2513c-116d-4c22-a780-25ea23c437cf.webp)

### beforeCreate
- 외부에서 들어오는 데이터인 **$props**(예시 코드0)에 접근할 수 있습니다.
- **컴포넌트 데이터**(예시 코드1)나 **컴포넌트 함수**(예시 코드1) 등이 아직 만들어지지 않았습니다. 따라서 **this**로 접근해서 컴포넌트 데이터와 관련된 작업을 할 수 없습니다.
```
예시 코드0
<!-- 부모 컴포넌트 -->
<template>
  <div>
    <MessageDisplay message="안녕하세요, Vue!" />
  </div>
</template>

<script>
import MessageDisplay from './MessageDisplay.vue'

export default {
  components: {
    MessageDisplay
  }
}
</script>
```
```
예시 코드0
<!-- 자식 컴포넌트: MessageDisplay.vue -->
<template>
  <div>
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  props: {
    message: String
  }
}
</script>
```
```
예시 코드1
export default {
  beforeCreate() {
    console.log(this.message);  // undefined 언디파인드가 뜸.
    this.greet();  // TypeError: this.greet is not a function
                  // greet 함수가 없다고 뜸
  },
  data() {
    return {
      message: 'Hello, World!'
    };
  },
  methods: {
    greet() {
      console.log(this.message);
    }
  }
}
```
### created
**인스턴스가 생성된 후 호출**됩니다.
- created 훅에서는 데이터 초기화, API 호출, 이벤트 리스너 등록, 타이머 설정을 합니다.
- data, methods, computed, watch와 같이 데이터와 관련된 것들을 **this**로 접근할 수 있게 됩니다.
- 컴포넌트의 template의 내용을 렌더링하기 전에 처리해야할 것들을 주로 여기서 합니다. (예시 코드3)
- 하지만 아직 마운트 전이라 **\$el**(예시 코드4), **\$ref**(예시 코드6)와 같은 것들을 이용해서 DOM에 접근할 수 없습니다.
```
예시 코드3
<template>
  <div>
    <h1>{{ message }}</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: ''
    };
  },
  created() {
    // 컴포넌트가 생성된 후 message를 설정
    this.message = 'Hello, Vue!';
    // API 호출 예시
    // this.fetchData();
  }
};
</script>
```
위 예시에서 created 훅은 컴포넌트가 생성된 후 message 데이터를 'Hello, Vue!'로 설정합니다. 
이로 인해 컴포넌트가 렌더링될 때 message가 템플릿에 표시됩니다.

**\$el란 무엇인가?**
```
예시 코드4
mounted() {
  console.log(this.$el); 
  // 이 컴포넌트의 루트 DOM 엘리먼트(예시 코드5)
}
```
**루트 DOM 엘리먼트란 무엇인가?**
```
예시 코드5
<template>
  <div class="root-element">
    <h1>제목</h1>
    <p>내용</p>
    <ChildComponent />
  </div>
</template>
```
위 코드에서 \<div class="root-element">가 루트 DOM 엘리먼트입니다. 이 \<div> 안에 있는 모든 요소들(h1, p, ChildComponent)은 이 루트 엘리먼트의 자식 요소가 됩니다.

**\$ref란 무엇인가?**
\$refs는 Vue.js에서 제공하는 특별한 속성으로, DOM 요소나 자식 컴포넌트에 직접 접근할 수 있게 해주는 기능입니다. ref는 이 $refs 시스템을 사용하기 위한 템플릿 속성입니다.
```
예시 코드6
<template>
  <div>
    <input ref="myInput">
  </div>
</template>

<script>
export default {
  mounted() {
    this.$refs.myInput.focus(); // 입력 필드에 포커스
  }
}
</script>
```


### beforeMount
인스턴스가 생성된 뒤 **template 옵션이** 있으면 이를 컴파일하는데 컴파일된 이후 호출됩니다.
- 컴파일 된 이후에 할만한 특별한 일이 별로 없습니다.
- 이후 **자식 컴포넌트**(예시 코드8)가 생성되고 마운트가 됩니다.

**template 옵션이란?**
```
template 옵션 = <template>
```
**자식 컴포넌트란?** (예시 코드8)
```
예시 코드8
<!-- ParentComponent.vue -->
<template>
  <div>
    <h1>부모 컴포넌트</h1>
    <ChildComponent />
  </div>
</template>

<script>
import ChildComponent from './ChildComponent.vue'

export default {
  components: {
    ChildComponent
  }
}
</script>

<!-- ChildComponent.vue -->
<template>
  <div>
    <p>자식 컴포넌트</p>
  </div>
</template>
```
자식 컴포넌트를 사용하는 이유
- 코드의 재사용성 향상
- 관심사의 분리로 인한 유지보수 용이성
- 복잡한 UI를 작은 단위로 나누어 관리 가능
- 자식 컴포넌트는 부모로부터 props를 받을 수 있고, 이벤트를 통해 부모와 통신할 수 있습니다.

**추가 설명이 필요한 beforeMount**
```
1. 부모 컴포넌트의 beforeMount 훅 실행:
   - 부모 컴포넌트의 템플릿이 컴파일된 후, 실제 DOM에 마운트되기 직전에 이 훅이 호출됩니다.
   - 이 시점에서 부모 컴포넌트의 데이터는 반응형이지만, DOM은 아직 업데이트되지 않은 상태입니다.

2. 자식 컴포넌트들의 생성 및 생명주기 훅 실행:
   - 부모 컴포넌트 템플릿 내의 자식 컴포넌트들이 생성됩니다.
   - 각 자식 컴포넌트는 자신의 생명주기 훅(created, beforeMount 등)을 차례로 실행합니다.
   - 이 과정은 재귀적으로 일어나며, 자식의 자식 컴포넌트도 같은 과정을 거칩니다.

3. 자식 컴포넌트들의 DOM 마운트:
   - 모든 자식 컴포넌트의 beforeMount 훅이 실행된 후, 자식 컴포넌트들이 실제 DOM에 삽입됩니다.
   - 이 시점에서 각 자식 컴포넌트의 mounted 훅이 호출됩니다.

4. 부모 컴포넌트의 DOM 마운트:
   - 모든 자식 컴포넌트가 DOM에 마운트된 후, 마지막으로 부모 컴포넌트가 DOM에 마운트됩니다.
   - 이후 부모 컴포넌트의 mounted 훅이 호출됩니다.

이 과정을 통해 컴포넌트 트리가 아래에서 위로(자식에서 부모로) 구축됩니다. 이는 각 컴포넌트가 자신의 자식 컴포넌트들이 완전히 준비된 후에 마운트되도록 보장합니다.

예를 들어, 컴포넌트 트리가 A(부모) > B(자식) > C(B의 자식) 구조라면:
1. A의 beforeMount
2. B의 생성 및 beforeMount
3. C의 생성 및 beforeMount
4. C의 DOM 마운트 및 mounted
5. B의 DOM 마운트 및 mounted
6. A의 DOM 마운트 및 mounted

이런 순서로 진행됩니다. 이 구조는 데이터 흐름과 컴포넌트 간 상호작용을 예측 가능하게 만들어 줍니다.
```

### mounted
**컴포넌트가 마운트된 이후 호출**됩니다.
- **\$el**, **\$ref**를 이용해 DOM에 접근할 수 있게 됩니다.
- **비동기 컴포넌트(async component)** 또는 **Suspense**가 들어간 컴포넌트를 제외하고는 모든 자식 컴포넌트들이 마운트되었을 때 호출됩니다.
- 대부분의 작업을 mounted에서 합니다.

**비동기 컴포넌트란?**
```
 AsyncHeavyComponent: defineAsyncComponent(() => import('./HeavyComponent.vue')
```

**\<Suspense>란?**
\<Suspense> 컴포넌트는 비동기 컴포넌트가 로딩되는 동안 "로딩 중..." 메시지를 표시합니다.

```
<Suspense>
  <template #default>
    <AsyncComponent />
  </template>
  <template #fallback>
    <div>Loading...</div>
  </template>
</Suspense>
```
### beforeUpdate
**컴포넌트 데이터가 변함으로 인해 DOM이 변화되기 전에 호출됩니다.**
- document.querySelector를 사용하면 브라우저의 실제 DOM을 직접 조회하므로 이미 새 값이 반영되어 있을 수 있습니다.
- \$el이나 \$ref를 사용하면 Vue가 관리하는 **가상 DOM**의 현재 상태(아직 업데이트되지 않은 상태)를 볼 수 있습니다.
- 여기서 데이터 값을 변경시키면 그 값이 렌더링에 반영되고, 다시 이 훅이 실행되진 않습니다. (무한 루프 방지)

**document.querySelector**란 무엇인가?
```
const element = document.querySelector('#myId');
```
- document.querySelector는 JavaScript에서 DOM(Document Object Model) 요소를 선택하는 데 사용되는 메서드입니다. 이 메서드는 CSS 선택자를 인자로 받아 해당 선택자와 일치하는 첫 번째 요소를 반환합니다.

**가상 DOM**이란 무엇인가?
- Vue는 데이터 변경 시 가상 DOM을 업데이트하고, 실제 DOM과 비교하여 변경된 부분만을 실제 DOM에 반영합니다. 이 과정은 성능을 향상시키고, 불필요한 DOM 조작을 줄여 CPU와 메모리 사용량을 감소시킵니다

### updated
**DOM이 변한 이후 호출**됩니다.
- 만일 여기서 값을 변경한다면 다시 beforeUpdate부터 호출되서 무한 루프를 돌 수 있습니다.

```
사용 예시
updated() {
  // 새로운 내용이 추가되어 스크롤이 필요한 경우
  if (this.$refs.container.scrollHeight > this.$refs.container.clientHeight) {
    this.$refs.container.scrollTop = this.$refs.container.scrollHeight;
  }
}
```
### beforeUnmount
**인스턴스가 마운트 해제되기 전에 호출**됩니다.
- 해제되기 직전이기 때문에 인스턴스의 모든 기능을 아직 사용할 수 있습니다.
- 이 후 자식 컴포넌트들도 해제됩니다.
```
export default {
  beforeUnmount() {
    // 전역 이벤트 리스너 제거
    window.removeEventListener('resize', this.handleResize);
    
    // 타이머 취소
    clearInterval(this.dataPollingInterval);
    
    // 웹소켓 연결 종료 준비
    this.websocket.prepareToClose();
  }
}
```

### unmounted
**컴포넌트가 마운트 해제된 후** 호출됩니다.
- 모든 자식 컴포넌트가 마운트 해제된 상태입니다.
- 컴포넌트에 관련된 것들이 모두 멈춥니다.
- 주료 별개로 남아있을 수있는 이벤트 리스너를 제거한다거나 서버와의 연결을 해지하는 용도로 사용합니다.
```
export default {
  unmounted() {
    // 웹소켓 연결 완전히 종료
    this.websocket.close();
    
    // 컴포넌트 관련 로컬 스토리지 정리
    localStorage.removeItem('componentData');
    
    // 사용 통계 전송
    this.analyticsService.sendComponentUsageStats(this.componentId);
    
    // 대용량 데이터 참조 제거
    this.largeDataSet = null;
    
    console.log('Component fully unmounted and cleaned up');
  }
}
```