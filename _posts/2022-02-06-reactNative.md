---
title: React Native?
categories: [dev]
comments: true
---

리액트 네이티브를 다루는 기술(김민준 지음) 책을 보고나서 내용을 정리해보려고 한다.

## React Native?

리액트 네이티브는 리액트 네이티브는 페이스북에서 만든 오픈소스 모바일 애플리케이션 프레임워크이고
자바스크립트와 리액트 라이브러리를 사용해서 네이티브 앱을 구현할 수 있도록 해주는 기술이다
리액트 네이티브를 사용해 만든 프로젝트에는 JavaScriptCore라는 자바스크립트 엔진을 가지고 있으며 이 엔진을 통해서 우리가 작성하는 코드들이 앱 내에 실행할 수 있게 해준다.

## React Native 장점

- 리액트 네이티브를 개발하면 IOS, Android를 동시에 효과적인 앱 개발을 할 수 있다.
- 만약에 React를 알고 있다면 러닝 커브가 낮아 쉽게 배울 수 있다.

## React Native 단점

- 하이브리드 앱 방식으로 네이티브 방식에 비해 성능이 떨어진다.
- 상대적으로 라이브러리가 많지 않기 때문에 개별적으로 개발을 해야하는 문제가 생길 수 있다.

## React Native 프로젝트 만들기

```
npx react-native init StartReactNative

```

### React Native 엔트리 파일 및 App 컴포넌트

```
import {AppRegistry} from 'react-native';
import App from './App';
import {name as appName} from './app.json';

AppRegistry.registerComponent(appName, () => App);

```

index.js는 엔트리 파일로 프로젝트가 시작할때 첫 파일을 가르킵니다.
App이라는 컴포넌트를 불러와 AppRegistry.registerComponent 함수를 사용해서 네이티브 시스템에 해당 컴포넌트를 등록합니다.

```
const App = () => {
  return (
    <SafeAreaView>
      <StatusBar />
      <View>
        <Text>Hello React-Native!</Text>
      </View>
    </SafeAreaView>
  );
};
```

SafeAreaView => iPhone X 이상 기종에서 디스플레이가 보이지 않는 영역과 최하단 영역에 내용이 보여지는것을 방지해주는 컴포넌트
View => 가장 기본적인 컴포넌트(레이아웃 및 스타일)
Text => 텍스트를 보여주는 컴포넌트

### Props & defaultProps

Props는 리액트와 똑같이 부모 -> 자식으로 컴포넌트 속성을 내려줄 수 있는데, 이렇게 하면 임의의 값을 넣어줄 수 있습니다.

defaultProps는 props를 지정하지 않았을 때 기본값을 설정해주고 싶을 때 사용할 수 있습니다.

```
Greeting.defaultProps = {
  name: 'Props 초기값 입니다'
}
```

### JSX 문법

JSX 문법은 간단하게 정리를 하자면..

1. 태그를 열면 반드시 닫아주자!
2. 스스로 닫는 태그 사용하자!
3. 반환할 땐 꼭 하나의 태그로 감싸자!
4. JSX안에서는 자바스크립트 표현식을 사용할 땐 중괄호로 감싸자!

### StyleSheet

React Native에서는 StyleSheet라는 것을 사용해 스타일링을 할 수 있습니다.
StyleSheet.create 함수를 사용해 그 안에 스타일링을 작성해야 합니다.

```

const styles = StyleSheet.create({
  container: {
    backgroundColor: 'black'
  },
})

```

### props Style

컴포넌트 스타일을 지정할 때, 여러 스타일을 적용하고 싶다면 배열 형태로 설정하면 된다.
rounded props가 true이면 styles.rounded 스타일이 적용 된다.
size라는 객체를 만들고 각각의 사이즈에 맞게 스타일링을 하면 sizes를 props로 넘기는것에 따라
small, medium, large가 적용된다.

```
<View style={[styles.box, props.rounded && styles.rounded, sizes[props.size]]}>

const size = {
  small : styles.small,
  medium: styles.medium,
  large: styles.large,
}

```

### 구조분해할당

컴포넌트에서 props를 조회하는 코드를 더 짧게 하기 위해서 비구조화 할당이라는 것을 하는데, 객체 안에 있는 값을 더 짧게 밖으로 추출해줄 수 있다.

```
function Box({rounded, size}) {
  console.log(rounded, size)
}

```

### useState, 조건부 렌더링

```
const App = () => {
  const [visible, setVisible] = useState(false);

  const onPress = () => {
    setVisible(!visible);
  };

  return (
    <SafeAreaView>
      <Button title="클릭!!" onPress={onPress} />

      {visible && (
        <View>
          <Text>조건부 렌더링</Text>
        </View>
      )}
    </SafeAreaView>
  );
};

export default App;
```

useState는 리액트에서 상태를 관리하는 기본적인 방법이다. 보통 리액트에서 use 시작하는 함수들은 Hook이라고 표현하고 다양한 기능을 구현할 수 있습니다.
그 중에서 useState 상태관리를 할 수 있는데, 처음 visible은 상태 값을 가리키고 setVisible은 상태 값을 변경할 수 있는 함수라고 할 수 있습니다.
onPress 함수에서 setVisible을 이용해 visible 값을 변경에 따라서 visible이 true 또는 false로 바뀌는데 visible이라는 상태 값에 따라
Text 컴포넌트를 보여줄 수 있습니다.
