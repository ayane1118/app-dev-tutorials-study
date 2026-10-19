# Making classes observable

---

## 参考教材
https://developer.apple.com/tutorials/app-dev-training/making-classes-observable
---

## Reference Type

`class` を利用して作成されるデータ型。

```swift
class ScrumTimer {
}
```

複数の変数から同じインスタンスを共有できる。

---

## Value Type と Reference Type

### Value Type

```swift
struct DailyScrum {
}
```

値がコピーされる。

```swift
var scrum1 = scrum
var scrum2 = scrum
```

---

### Reference Type

```swift
class ScrumTimer {
}
```

同じインスタンスを参照する。

```swift
let timer1 = ScrumTimer()
let timer2 = timer1
```

**学んだこと**

- `struct` はコピーされる
- `class` は共有される
- SwiftUIでは用途によって使い分ける

---
## Observable

クラスの変更を監視できるようにする機能。

```swift
@Observable
final class ScrumTimer {
}
```

プロパティが変更されると、SwiftUIへ通知される。

**学んだこと**

- クラスを監視対象にできる
- プロパティ変更をUIへ通知できる
- SwiftUIの状態管理と連携できる

---

## Observable Objectの受け渡し

親View

```swift
struct ParentView: View {
    @State var scrumTimer = ScrumTimer()
}
```

子View

```swift
struct ChildView: View {
    @Bindable var timer: ScrumTimer
}
```

利用例

```swift
ChildView(timer: scrumTimer)
```

**学んだこと**
- オブジェクトをView間で共有できる
- Source of Truthを親で保持できる
- 子Viewからも変更できる

---

## @Environment

View階層全体でデータを共有するProperty Wrapper。


### 環境へ登録

```swift
.environment(scrumTimer)
```

### 環境から取得

```swift
@Environment(ScrumTimer.self)
private var timer
```


**学んだこと**
- View階層全体でデータ共有できる
- 引数として渡し続ける必要がない
- 深い階層のViewからも取得できる

---

## Environmentの利用例

親View

```swift
struct ParentView: View {
    @State var scrumTimer = ScrumTimer()

    var body: some View {
        ChildView()
            .environment(scrumTimer)
    }
}
```

孫View

```swift
struct GrandchildView: View {
    @Environment(ScrumTimer.self)
    private var timer
}
```

**学んだこと**
- 中間Viewがデータを知らなくてもよい
- 不要な依存関係を減らせる
- アプリ構造をシンプルに保てる

---

## Property Wrapperの使い分け

### @State

```swift
@State var timer = ScrumTimer()
```
オブジェクトを作成・保持する。

### @Bindable

```swift
@Bindable var timer: ScrumTimer
```
親から受け取ったオブジェクトを利用する。

### @Environment

```swift
@Environment(ScrumTimer.self)
private var timer
```
環境からオブジェクトを取得する。

**学んだこと**

- @State → 作る
- @Bindable → 受け取る
- @Environment → 環境から取得する

---

## 振り返り

このチュートリアルでは、参照型（class）をSwiftUIで扱うための仕組みを学んだ。
- Reference Type（参照型）の特徴
- Value Typeとの違い
- `@Environment` を利用した環境共有
- View階層での状態管理の考え方
- ObservableオブジェクトとUI自動更新の仕組み

SwiftUIでは、値型には `@State` や `@Binding` を利用し、参照型には `@Observable`・`@State`・`@Bindable`・`@Environment` を組み合わせることで、複雑な状態管理をシンプルに実装できることを学んだ。