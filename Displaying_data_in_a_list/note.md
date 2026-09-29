# Displaying Data in a List

---

## 参考教材
https://developer.apple.com/tutorials/app-dev-training/displaying-data-in-a-list

---

## List

SwiftUIで一覧表示を行うためのView

設定アプリやメールアプリのような、複数のデータを縦方向に表示するUIを簡単に作成できる
```
List {
    Text("Item 1")
    Text("Item 2")
}
```

**学んだこと**
- 複数のデータを一覧表示できる
- 動的にViewを生成できる
- SwiftUIでのリスト表示の基本となるView

---

## ScrumsView

複数のスクラムを一覧表示するためのView

```
struct ScrumsView: View {
let scrums: [DailyScrum]
}
```

**学んだこと**
- 配列データを受け取れる
- 一覧画面を表現できる
- CardViewを組み合わせて大きな画面を構築できる

---

## KeyPath

オブジェクトのプロパティを参照するためのSwiftの記法
```
\.title
```
は
```
scrum.title
```
を意味する

**学んだこと**
- Listは各要素を識別するためのIDが必要
- KeyPathを利用して識別子を指定できる
- 今回は title を一時的な識別子として利用している

---

## Identifiable

SwiftUIでデータを一意に識別するためのプロトコル
```
struct DailyScrum: Identifiable {
}
```

Listは各要素を区別する必要があるため、データモデルに一意な識別子を持たせる

**学んだこと**
- Listはデータを識別するためのIDが必要
- タイトルでは重複する可能性がある
- Identifiableを利用すると安全に識別できる

---
 
## UUID

重複しない一意な識別子を生成するための型
```swift
let id: UUID
```

**学んだこと**
- 一意なIDを生成できる
- 同じタイトルのデータでも区別できる
- 実際のアプリ開発でもよく利用される

---

## Initializer

インスタンス生成時にプロパティへ値を設定するための仕組み
```
init(id: UUID = UUID(), title: String, attendees: [String], lengthInMinutes: Int, theme: Theme) {
    self.id = id
    self.title = title
    self.attendees = attendees
    self.lengthInMinutes = lengthInMinutes
    self.theme = theme
}
```

**学んだこと**
- self はインスタンス自身を表す
- 引数とプロパティを区別できる
- 受け取った値をプロパティへ代入するために使用する

---

## 振り返り
 
このチュートリアルでは、SwiftUIでデータを一覧表示する方法と、データを一意に識別する仕組みについて学んだ。
 
- `List` を利用した一覧画面の作成
- 配列データから動的にViewを生成する方法
- `CardView` を再利用したコンポーネント設計
- KeyPath（`\.title`）を利用した識別子の指定
- `Identifiable` プロトコルによるデータ管理
- `UUID` を利用した一意なIDの生成
- イニシャライザとデフォルト値の仕組み
- `WindowGroup` を利用したルート画面の設定
- `ScrumsView` をアプリの開始画面として表示する方法