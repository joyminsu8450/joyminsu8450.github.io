---
layout: post
title: "JavaScript async/await 패턴 정리"
date: 2026-01-05
categories: [개발]
---

비동기 프로그래밍은 JavaScript의 핵심입니다. 콜백 지옥에서 Promise, 그리고 async/await까지의 발전 과정을 살펴보겠습니다.

## 콜백의 문제점

중첩된 콜백은 코드의 가독성을 크게 떨어뜨립니다.

```javascript
getUser(userId, function(user) {
  getOrders(user.id, function(orders) {
    getOrderDetail(orders[0].id, function(detail) {
      console.log(detail);
    });
  });
});
```

## Promise로 개선

```javascript
getUser(userId)
  .then(user => getOrders(user.id))
  .then(orders => getOrderDetail(orders[0].id))
  .then(detail => console.log(detail))
  .catch(error => console.error(error));
```

## async/await으로 더 깔끔하게

```javascript
async function getOrderInfo(userId) {
  try {
    const user = await getUser(userId);
    const orders = await getOrders(user.id);
    const detail = await getOrderDetail(orders[0].id);
    console.log(detail);
  } catch (error) {
    console.error('에러 발생:', error);
  }
}
```

## 병렬 실행 패턴

독립적인 비동기 작업은 `Promise.all`을 사용하면 성능을 크게 개선할 수 있습니다.

```javascript
// 순차 실행 - 느림
const users = await getUsers();
const posts = await getPosts();
const comments = await getComments();

// 병렬 실행 - 빠름
const [users, posts, comments] = await Promise.all([
  getUsers(),
  getPosts(),
  getComments()
]);
```

## 에러 핸들링 팁

`Promise.allSettled`를 사용하면 하나가 실패해도 나머지 결과를 받을 수 있습니다.

```javascript
const results = await Promise.allSettled([
  fetchUserData(),
  fetchAnalytics(),
  fetchNotifications()
]);

results.forEach(result => {
  if (result.status === 'fulfilled') {
    console.log('성공:', result.value);
  } else {
    console.log('실패:', result.reason);
  }
});
```

async/await은 비동기 코드를 동기 코드처럼 읽을 수 있게 해주는 강력한 도구입니다. 하지만 병렬 실행이 가능한 경우에는 반드시 `Promise.all`을 활용하세요!
