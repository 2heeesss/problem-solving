# 햄버거 만들기

#스택

## 풀이 복기

입력의 범위를 보고 시간복잡도 제한을 생각하자

### 풀이 1

```js
/**
 * 시간초과
 * n: ingredient.length
 * 시간복잡도: O(n*n)
 * 공간복잡도: O(n)
 */
function solution(ingredient) {
  let originStr = ingredient.join('');
  let str = originStr;
  let replaceStr = str.replace('1231', '');

  while (str.length !== replaceStr.length) {
    str = replaceStr;
    replaceStr = replaceStr.replace('1231', '');
  }

  return Math.floor((originStr.length - str.length) / 4);
}
```

### 풀이 2

```js
/**
 * 시간초과
 * n: ingredient.length
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
function solution(hamburgerIngredient) {
  const stack = [];
  let hamburgerCnt = 0;

  for (const ingredient of hamburgerIngredient) {
    stack.push(ingredient);
    if (stack.length >= 4 && hasHamburger()) {
      stack.pop();
      stack.pop();
      stack.pop();
      stack.pop();
      hamburgerCnt += 1;
    }
  }

  return hamburgerCnt;

  function hasHamburger() {
    return `${stack.at(-4)}${stack.at(-3)}${stack.at(-2)}${stack.at(-1)}` === '1231';
  }
}
```
