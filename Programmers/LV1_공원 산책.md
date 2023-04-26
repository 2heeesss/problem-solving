# 공원 산책

#구현#배열#문자열

## 풀이 복기

첫번째 풀이에서 런타임 에러 발생. 발생한 이유는 배열의 요소를 찾을 때 배열 범위를 넘어가는 경우에도 찾아서 발생함. 해당 문제 때문에 배열의 범위를 넘어가는지 확인하는 조건문이 for문안으로 들어와서 해결함

startPosition을 찾는 더 간단한 방법이 있어서 대체함. 마지막 방법이 눈에 더 쉽게 들어 와서 좋은방법같다고 생각함.

### 풀이 1

```js
function solution(park, routes) {
  const startPosition = park
    .map(val => [...val])
    .reduce((acc, cur, yPosition) => {
      const xPosition = cur.findIndex(val => val === 'S');
      return xPosition !== -1 ? [yPosition, xPosition] : acc;
    }, []);
  const parkMatrix = park.map(val => [...val]);
  const parkWidth = park[0].length;
  const parkHeight = park.length;

  const directionMap = new Map();
  directionMap.set('E', [0, 1]);
  directionMap.set('W', [0, -1]);
  directionMap.set('N', [-1, 0]);
  directionMap.set('S', [1, 0]);

  return routes.reduce(
    (acc, route) => {
      const [direction, length] = route.split(' ');
      const vector = directionMap.get(direction);
      let newPosition = acc;
      for (let i = 0; i < length; i++) {
        newPosition = [newPosition[0] + vector[0], newPosition[1] + vector[1]];
        if (parkMatrix[newPosition[0]][newPosition[1]] === 'X') {
          return acc;
        }
      }
      if (0 > newPosition[0] || newPosition[0] >= parkHeight) {
        return acc;
      }
      if (0 > newPosition[1] || newPosition[1] >= parkWidth) {
        return acc;
      }

      return newPosition;
    },
    [startPosition[0], startPosition[1]]
  );
}
```

### 풀이 2

```js
function solution(park, routes) {
  const startPosition = park
    .map(val => [...val])
    .reduce((acc, cur, yPosition) => {
      const xPosition = cur.findIndex(val => val === 'S');
      return xPosition !== -1 ? [yPosition, xPosition] : acc;
    }, []);
  const parkMatrix = park.map(val => [...val]);
  const parkWidth = park[0].length;
  const parkHeight = park.length;

  const directionMap = new Map();
  directionMap.set('E', [0, 1]);
  directionMap.set('W', [0, -1]);
  directionMap.set('N', [-1, 0]);
  directionMap.set('S', [1, 0]);

  return routes.reduce(
    (acc, route) => {
      const [direction, length] = route.split(' ');
      const vector = directionMap.get(direction);
      let newPosition = acc;
      for (let i = 0; i < length; i++) {
        newPosition = [newPosition[0] + vector[0], newPosition[1] + vector[1]];

        if (0 > newPosition[0] || newPosition[0] >= parkHeight) {
          return acc;
        }
        if (0 > newPosition[1] || newPosition[1] >= parkWidth) {
          return acc;
        }
        if (parkMatrix[newPosition[0]][newPosition[1]] === 'X') {
          return acc;
        }
      }

      return newPosition;
    },
    [startPosition[0], startPosition[1]]
  );
}
```

### 풀이 2

```js
const startPositionY = park.findIndex(v => v.includes('S'));
const startPositionX = [...park[startPositionY]].findIndex(v => v === 'S');
```
