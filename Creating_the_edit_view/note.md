# Creating the edit view

---

## 参考教材
https://developer.apple.com/tutorials/app-dev-training/creating-the-edit-view

---

## emptyScrum

空のスクラムデータを返す静的プロパティ
```swift
static var emptyScrum: DailyScrum {
    DailyScrum(
        title: "",
        attendees: [],
        lengthInMinutes: 5,
        theme: .sky
    )
}
```
編集画面の初期値として利用する。

**学んだこと**
- 初期表示用のデータを定義できる
- 編集画面のプレビューやテストで利用できる
- モデルに共通の初期値を持たせられる

---

## Form

入力フォーム用のコンテナ
```swift
Form {
}
```
iOS標準の設定画面のような見た目になる。

**学んだこと**
- 入力画面を簡単に構築できる
- プラットフォームに最適な表示になる
- TextFieldやSliderとの相性が良い

---

## Section

入力項目をグループ化する
```swift
Section(header: Text("Meeting Info")) {
}
```

---

## TextField

テキスト入力用のコントロール

```swift
TextField(
"Title",
text: $scrum.title
)
```

---

## $

SwiftUIでBindingを生成する記法
```swift
$scrum.title
```

意味
```swift
scrum.title
```
→ String
 
```swift
$scrum.title
```
→ Binding<String>

**学んだこと**
- StateとViewを接続できる
- 双方向データバインディングを実現できる
- TextFieldやSliderで利用する

---

## lengthInMinutesAsDouble

Slider用の計算プロパティ
```swift
var lengthInMinutesAsDouble: Double
```

Slider：Doubleしか扱えない
しかし、モデルではlengthInMinutesがIntになっている

**学んだこと**
- UIとモデルの型の違いを吸収できる
- 計算プロパティを利用して変換できる

---

## get

値を取得するときに呼ばれる
```swift
get {
    Double(lengthInMinutes)
}
```
整数をDoubleへ変換する

**学んだこと**
- 表示用データを加工できる
- 読み取り時の処理を書ける

---

## set

値を書き込むときに呼ばれる
```swift
set {
    lengthInMinutes = Int(newValue)
}
```
Doubleを整数へ変換して保存する

---

## Slider

数値を調整するためのコントロール
```swift
Slider(
    value: $scrum.lengthInMinutesAsDouble,
    in: 5...30,
    step: 1
)
```

範囲：5~30
間隔：1刻み

**学んだこと**
- 数値を直感的に変更できる
- BindingでStateと接続できる
- 範囲や刻み幅を指定できる

