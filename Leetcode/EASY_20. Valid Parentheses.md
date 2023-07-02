# 20. Valid Parentheses

#stack

### 풀이 1

```js
/**
 * @param {string} s
 * @return {boolean}
 */
const isValid = function (s) {
  const closeBraketsMap = new Map();
  closeBraketsMap.set(')', '(');
  closeBraketsMap.set('}', '{');
  closeBraketsMap.set(']', '[');

  const st = [...s].reduce((stack, bracket) => {
    if (stack.length === 0) {
      stack.push(bracket);
      return stack;
    }

    if (closeBraketsMap.get(bracket) === stack[stack.length - 1]) {
      stack.pop();
    } else {
      stack.push(bracket);
    }
    return stack;
  }, []);

  return st.length === 0;
};
```

### 풀이 2

```js

```
