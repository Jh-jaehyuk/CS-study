
---
#### Vuex Store를 공부해서 가져갈 수 있는 것
상태 관리 패턴 이해:
Vuex는 상태 관리 패턴의 좋은 예시입니다. 이를 통해 대규모 애플리케이션에서 데이터를 어떻게 효과적으로 관리할 수 있는지 배울 수 있습니다.

모듈화와 구조화:
Vuex Store를 모듈로 나누는 방법을 배우면서, 큰 규모의 애플리케이션을 어떻게 구조화하고 관리할 수 있는지 이해할 수 있습니다.

---

## 가이드 라인
**굵은 글씨**로 표현한 것들은 추가 설명이 있습니다.

---
### VUEX의 STORE란 무엇인가?
Vuex는 Vue.js 애플리케이션의 상태 관리를 위한 라이브러리입니다. Vuex의 Store는 애플리케이션의 **중앙 집중식 상태를 관리하는 객체**입니다.

**중앙 집중식 상태를 관리하는 객체란?**
애플리케이션의 모든 상태(데이터)를 한 곳에서 관리하는 방식을 말합니다. Vuex Store는 이러한 역할을 하는 객체로, 애플리케이션의 모든 컴포넌트가 접근할 수 있는 전역 상태를 저장하고 관리합니다.

Store의 핵심 구성 요소들은 State, Mutations, Actions, Getters가 있습니다.

#### State (데이터 객체)
- State는 쉽게 생각하면 공통으로 참조하기 위한 변수를 정의한 것입니다.
- 프로젝트의 모든 곳에서 이를 참조하고 사용할 수 있습니다.
- 모든 컴포넌트들에서 공통된 값을 사용할 수 있습니다.
```
export const state = () => ({
  user: null,
  isAuthenticated: false,
  posts: []
})
```

#### Mutations (동기형 State 변경 처리기)
- State의 데이터를 변경하는 방법을 Mutations에서 정의합니다.
- **동기 처리** 기준입니다.
- commit은 Mutation을 호출하여 State를 변경하는 메서드입니다.
- commit('함수명', '전달인자') 방식으로 호출합니다.
- mutations 내에 함수들을 작성합니다.

**동기 처리란?**
코드가 순차적으로 실행되며, 한 작업이 완료될 때까지 다음 작업이 기다리는 방식입니다. Mutations는 동기적으로 동작해야하는데, 이는 상태 변화를 예측 가능하고 추적하기 쉽게 만들기 위함입니다.

아래 코드에서 currentUser라는 Mutation을 정의하고 있습니다.
```
export const mutations = {
  setUser(state, user) {
    state.user = user;
    state.isAuthenticated = !!user;
  },
  setPosts(state, posts) {
    state.posts = posts;
  }
}
```
이 Mutation을 호출하려면 다음과 같이 commit을 사용합니다
```
store.commit('setUser', { id: 1, name: 'John' });
```
#### Actions(Mutation 트리거)
- Mutation을 실행시키는 역할을 담당합니다.
- **비동기 처리 기준**입니다.
- dispatch('함수명', '전달인자') 방식으로 호출합니다.
- 비동기 기준이므로 주로 **콜백 함수**로 작성합니다.
- Actions 내에 함수들을 작성합니다.

**비동기 처리 기준이란?**
작업이 완료되기를 기다리지 않고 다음 코드를 실행하는 방식입니다.
주로 API호출이나 타이머 같은 시간이 걸리는 작업에 사용됩니다.
Actions는 비동기 작업을 수행할 수 있어, 데이터를 가져오거나 복잡한 로직을 처리한 후 Mutation을 commit할 수 있습니다.

**콜백 함수**
콜백 함수는 다른 함수에 인자로 전달되어, 특정 이벤트가 발생하거나 작업이 완료되었을 때 호출되는 함수입니다. 비동기 작업에서 자주 사용되며, 작업이 완료된 후 실행될 로직을 정의하는 데 사용됩니다.

```
function doSomething(callback) {
  console.log("작업을 수행중...");
  
  // 작업이 끝난 후 콜백 함수를 호출
  callback();
}

function afterWork() {
  console.log("작업이 끝났어요!");
}

// doSomething 함수를 호출하면서 afterWork 함수를 콜백으로 전달
doSomething(afterWork);
```
위 코드를 실행하면 다음과 같은 결과가 나옵니다:
```
작업을 수행중...
작업이 끝났어요!
```

```
export const actions = {
  login({ commit }, user) {
    // 비동기 로직 (예: API 호출)을 여기서 수행할 수 있습니다.
    commit('setUser', user);
  },
  fetchPosts({ commit }) {
    // 비동기로 포스트를 가져오는 로직
    // 예: API 호출 후 결과를 받아 commit
    const posts = [/* API에서 받아온 포스트 데이터 */];
    commit('setPosts', posts);
  }
}
```
액션을 호출할 때는 다음과 같이 dispatch를 사용합니다:
```
store.dispatch('login', { id: 1, name: 'John' });
store.dispatch('fetchPosts');
```

#### Getters (State 기반 계산된 속성)
- State를 기반으로 계산된 값을 반환합니다.
- 컴포넌트에서 여러 번 사용되는 복잡한 로직을 중앙화할 수 있습니다.
- 성능 최적화를 위해 결과를 캐싱합니다.
- 여러 컴포넌트에서 동일한 연산을 반복하는 대신, Getter를 통해 한 번만 정의하고 여러 곳에서 재사용할 수 있습니다.

```
export const getters = {
  isAdmin: (state) => {
    return state.user && state.user.role === 'admin';
  },
  postCount: (state) => {
    return state.posts.length;
  },
  getPostById: (state) => (id) => {
    return state.posts.find(post => post.id === id);
  }
}
```
컴포넌트에서 Getter를 사용할 때는 다음과 같이 접근합니다:
```
computed: {
  isAdmin() {
    return this.$store.getters.isAdmin;
  },
  postCount() {
    return this.$store.getters.postCount;
  }
}
```
이렇게 State, Mutations, Actions, Getters를 통해 Vuex Store는 애플리케이션의 상태를 효과적으로 관리하고, 컴포넌트 간 데이터 공유와 상태 변경을 일관되게 처리할 수 있게 해줍니다.
