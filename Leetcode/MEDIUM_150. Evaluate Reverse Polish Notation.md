# 150. Evaluate Reverse Polish Notation

#stack

## 풀이 복기

첫번째 풀이는 틀렸다. 그 이유는 `/` 에서 Math.floor의 동작 때문인데, 양수일때는 잘 동작하지만 음수일때는 예상과 다르게 동작했기 때문이다.

Math.floor() 함수는 주어진 숫자와 같거나 작은 정수 중에서 가장 큰 수를 반환한다. 즉, -0.5 와 같은 음수일때는 -1을 반환하게 된다. 이 경우를 생각하지 못해서 두번째 풀이로 고쳐서 해결했다.

이와 비슷한 문제들에서 습관적으로 Math.floor, Math.ceil, Math.round 3개중에 하나를 고르게 된다. 이때 Math.trunc 라는 메서드를 사용했으면 첫번째 시도에서 해결했을것이다.

Math.trunc() 함수는 주어진 값의 소수부분을 제거하고 숫자의 정수부분을 반환한다. 즉, -0.5 와 같은 음수일때도 0을 반환하게 된다.

### 풀이 1

```js
/**
 * @param {string[]} tokens
 * @return {number}
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
const evalRPN = function (tokens) {
  const stack = [];
  tokens.forEach(token => {
    if (token === '+') {
      const secondNum = Number(stack.pop());
      const firstNum = Number(stack.pop());
      stack.push(firstNum + secondNum);
    } else if (token === '-') {
      const secondNum = Number(stack.pop());
      const firstNum = Number(stack.pop());
      stack.push(firstNum - secondNum);
    } else if (token === '*') {
      const secondNum = Number(stack.pop());
      const firstNum = Number(stack.pop());
      stack.push(firstNum * secondNum);
    } else if (token === '/') {
      const secondNum = Number(stack.pop());
      const firstNum = Number(stack.pop());
      stack.push(Math.floor(firstNum / secondNum));
    } else {
      stack.push(token);
    }
  });

  return stack;
};
```

### 풀이 2

```js
/**
 * @param {string[]} tokens
 * @return {number}
 */
const evalRPN = function(tokens) {
    const stack = [];
    tokens.forEach((token) => {
        if (token === '+') {
            const secondNum = Number(stack.pop());
            const firstNum = Number(stack.pop());
            stack.push(firstNum + secondNum);
        } else if (token === '-') {
            const secondNum = Number(stack.pop());
            const firstNum = Number(stack.pop());
            stack.push(firstNum - secondNum);
        } else if (token === '*') {
            const secondNum = Number(stack.pop());
            const firstNum = Number(stack.pop());
            stack.push(firstNum * secondNum);
        } else if (token === '/') {
            const secondNum = Number(stack.pop());
            const firstNum = Number(stack.pop());
            const resNum = Math.floor(Math.abs(firstNum) / Math.abs(secondNum));
            const secondNumSign = secondNum < 0 ? -1 : 1;
            const firstNumSign = firstNum < 0 ? -1 : 1;
            stack.push(resNum * secondNumSign * firstNumSign);
        } else {
            stack.push(token);
        }
    });

    return stack
};

    return stack
};

    return stack
};

    return stack
};

    return stack
};
```
