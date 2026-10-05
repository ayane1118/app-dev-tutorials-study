# Managing data flow between views

---

## 参考教材
https://developer.apple.com/tutorials/app-dev-training/managing-data-flow-between-views

---

## Source of Truth

アプリ内で唯一の正しいデータを管理する場所
同じアプリ内で同じデータを複数箇所に保持すると、データの不整合が発生し、バグの原因になる。
そのため、SwiftUIでは各データに対して1つの「信頼できる単一の情報源(Source of Truth)」を持つことが推奨されている。

```
データ
↓
Source of Truth
↓
複数のViewが共有
```
1か所のデータを更新すると、そのデータを利用しているすべてのViewに変更が反映される。

**学んだこと**
- データは1か所で管理する
- 複数コピーを持たない
- バグや不整合を減らせる
- 複数のViewで同じデータを共有できる

---

##　 Property Wrapper

Swiftの機能の1つ。
プロパティへ特別な振る舞いを追加できる。
SwiftUIではデータ管理のために頻繁に利用する。

@State, @Bindingなど

**学んだこと**
- プロパティに特別な機能を追加できる
- SwiftUIの状態管理を支えている
- データとUIを同期できる

---

## @State

View内部で状態を保持するためのProperty Wrapper
```swift
@State private var count = 0
```

@Stateを使う場面：一時的な状態の管理。

**管理しやすいもの**
- ボタンの選択状態
- 検索条件
- フィルター設定
- シート表示状態
- 一時的な入力値

**学んだこと**
- View内で状態を保持できる
- 値が変わるとUIが自動更新される
- SwiftUIが再描画を担当する
- Viewのローカルな情報源になる
- 一時的な状態管理に向いている
- 永続化データには向いていない
- privateで利用することが推奨される

---

## @Binding

既存のSource of Truthを共有するProperty Wrapper
```swift
@Binding var scrum: DailyScrum
```

自分ではデータを保持しない。代わりに、
```swift
@State
```
で管理されている値への参照を持つ。

**イメージ**
```text
Parent View
↓
@State
↓
@Binding
↓
Child View
```

**学んだこと**
- データを保持しない
- 元のデータへの参照を持つ
- 読み取りも書き込みもできる
- 親子View間でデータ共有できる

---

## 振り返り
 
このセクションでは、SwiftUIの状態管理の基本となる「Source of Truth」の考え方と、`@State`・`@Binding` を学んだ。
 
- Source of Truthによるデータ一元管理
- データの重複管理を避ける重要性
- Property Wrapperの基本
- @Stateによる状態管理
- 状態変更時の自動再描画
- SwiftUIの宣言的UI
- @Bindingによるデータ共有
- 親Viewと子Viewの双方向通信
- 読み取り専用データの受け渡し
- Scrumdingerの編集機能で利用される設計
 
SwiftUIでは、`@State` がデータの所有者（Source of Truth）となり、`@Binding` がそのデータを他のViewへ共有する役割を持つ。
これにより、複数の画面間で常に同じデータを表示・編集できる仕組みが実現されている。