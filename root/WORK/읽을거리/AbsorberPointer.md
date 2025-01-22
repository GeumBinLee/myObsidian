`absorbing`은 `AbsorbPointer` 위젯의 속성으로, 자식 위젯이 터치 이벤트를 받을 수 있는지 여부를 제어합니다.

### `absorbing`의 역할

- `absorbing`이 **`true`**로 설정되면, 해당 위젯과 그 하위 위젯들은 모든 터치 이벤트를 "흡수"하여 터치 이벤트가 전달되지 않습니다.
- **`false`**로 설정되면, 터치 이벤트가 하위 위젯으로 전달되어 일반적으로 상호작용이 가능합니다.

즉, `AbsorbPointer`는 특정 조건에서 사용자 입력(터치 이벤트)을 차단하고 싶을 때 사용하는 위젯입니다.

### 사용된 코드

dart

복사편집

`AbsorbPointer(   absorbing: widget.readOnly,   child: TextFormField(     ...   ), )`

### 동작 설명

1. `widget.readOnly`가 **`true`**일 경우:
    
    - `AbsorbPointer`가 터치 이벤트를 차단합니다.
    - 따라서 `TextFormField`가 터치 이벤트를 받지 못하고 비활성화됩니다.
2. `widget.readOnly`가 **`false`**일 경우:
    
    - `AbsorbPointer`가 터치 이벤트를 차단하지 않습니다.
    - `TextFormField`가 터치 이벤트를 받아 정상적으로 상호작용할 수 있습니다.

### 사용 이유

`readOnly` 상태에서 `TextFormField`의 터치 동작을 비활성화하려면 `AbsorbPointer`를 사용하는 것이 적합합니다. 이렇게 하면 텍스트 입력은 차단되지만, 외부에서 터치 이벤트를 직접 처리(`onTap`)할 수 있는 유연성을 제공합니다.

### 참고

`AbsorbPointer`와 비슷한 위젯으로 `IgnorePointer`가 있습니다. 두 위젯의 차이점은 다음과 같습니다:

- **`AbsorbPointer`**: 터치 이벤트를 차단하지만, 해당 위젯은 여전히 화면에서 렌더링됩니다.
- **`IgnorePointer`**: 터치 이벤트를 차단하며, 터치 이벤트가 차단된 위젯은 완전히 무시됩니다.