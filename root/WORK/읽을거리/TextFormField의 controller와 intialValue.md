
### 문제의 원인

`TextFormField`에서 `controller`와 `initialValue`를 동시에 설정하면, **`controller`가 우선 순위를 가지며 `initialValue`는 무시**됩니다. 즉, `controller`가 설정된 경우 `initialValue` 값이 필드에 나타나지 않습니다.

이 코드에서:

dart

복사편집

`DefaultTextFormField(   onTap: () {     signUpProcess.updateCurrentStep(1);     navigate(context, route: AppRoute.signUpProfileChoice);   },   enabled: true,   readOnly: true,   initialValue: signUpState.age.toString(),   autofocus: false,   controller: _nicknameController,   keyboardType: TextInputType.text,   hintText: '나이를 선택해주세요.',   fillColor: Palette.colorGrey100,   errorText: signUpState.error, // 상태 기반 에러 메시지   onFieldSubmitted: (value) =>       signUpProcess.updateNickname(value), ),`

- `controller`가 설정되어 있으므로 `initialValue`는 적용되지 않습니다.

---

### 해결 방법

#### 1. **`controller`와 `initialValue` 중 하나만 사용**

`controller`가 필요 없다면 `initialValue`만 설정하세요:

dart

복사편집

`DefaultTextFormField(   onTap: () {     signUpProcess.updateCurrentStep(1);     navigate(context, route: AppRoute.signUpProfileChoice);   },   enabled: true,   readOnly: true,   initialValue: signUpState.age.toString(), // initialValue 사용   autofocus: false,   keyboardType: TextInputType.text,   hintText: '나이를 선택해주세요.',   fillColor: Palette.colorGrey100,   errorText: signUpState.error, // 상태 기반 에러 메시지   onFieldSubmitted: (value) =>       signUpProcess.updateNickname(value), ),`

---

#### 2. **`controller`의 초기값 설정**

`initialValue` 대신 `controller.text`를 사용하여 초기값을 설정합니다. 이 방법은 `controller`를 계속 사용해야 할 경우 유용합니다:

dart

복사편집

`final TextEditingController _nicknameController = TextEditingController();  @override void initState() {   super.initState();   _nicknameController.text = signUpState.age?.toString() ?? ''; }`

위처럼 초기화한 뒤, `initialValue`를 제거하고 `controller`만 사용합니다:

dart

복사편집

`DefaultTextFormField(   onTap: () {     signUpProcess.updateCurrentStep(1);     navigate(context, route: AppRoute.signUpProfileChoice);   },   enabled: true,   readOnly: true,   controller: _nicknameController, // controller 사용   autofocus: false,   keyboardType: TextInputType.text,   hintText: '나이를 선택해주세요.',   fillColor: Palette.colorGrey100,   errorText: signUpState.error, // 상태 기반 에러 메시지   onFieldSubmitted: (value) =>       signUpProcess.updateNickname(value), ),`

---

### 선택 가이드

- **`controller`가 필요하지 않다면**: `initialValue`만 사용하세요.
- **`controller`가 필요하다면**: `controller.text`를 초기화하고 `initialValue`는 제거하세요.

이로 인해 `selectedYear`가 정상적으로 `TextFormField`의 초기값으로 표시될 것입니다.