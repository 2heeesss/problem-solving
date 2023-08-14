# 대충 만든 자판

#맵#배열

## 풀이 복기

문제를 풀면서 배운점이나 놓친점을 작성합니다.

### 풀이 1

```js
/**
 * AC
 * n: keymap.length, m: keymap[k].length, i: targets.length, j: target[k].length
 * 시간복잡도: O(n*m + i*j)
 * 공간복잡도: O(i)
 */
function solution(keymap, targets) {
  const keypadMap = getKeypadMap(keymap);

  return targets.map(target => {
    let sum = 0;
    for (const targetNum of target) {
      if (!keypadMap.has(targetNum)) {
        return -1;
      }
      sum += keypadMap.get(targetNum);
    }

    return sum;
  });
}
function getKeypadMap(keymap) {
  const map = new Map();

  for (const keys of keymap) {
    for (let i = 0; i < keys.length; i++) {
      const char = keys[i];
      if (map.has(char)) {
        const prevI = map.get(char);
        map.set(char, Math.min(prevI, i + 1));
      } else {
        map.set(char, i + 1);
      }
    }
  }

  return map;
}
```
