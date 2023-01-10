# 🎯 Reflow or Repaint

- `reflow`는 생성된 DOM 노드의 레이아웃 수치 변경시 영향을 받은 모든 노드 수치를 다시 계산하여 `Render Tree`를 재생성하는 과정이다.

```jsx
function reflow(){
	document.getElementById('container').style.width = "600px";
	return false;
}
```

- 변경된 스타일 수치 계산이 수행되고, `reflow` 과정이 수행되고 생성된 `Render Tree` 를 그리고 `repaint` 과정이 수행된다.
- `background-color` 같은 경우는 레이아웃 수치는 변경되지 않았으므로 `reflow` 과정이 생략된 `repaint` 과정만 일어나게 된다.
