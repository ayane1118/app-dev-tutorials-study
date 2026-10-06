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

---

## onDelete

削除する
```swift
ForEach(scrum.attendees) { attendee in
Text(attendee.name)
}
.onDelete { indices in
scrum.attendees.remove(atOffsets: indices)
}
```

### indices

削除対象の行番号
```swift
indices
```

### remove(atOffsets:)
 
指定された位置の要素を削除する。
```swift
scrum.attendees.remove(atOffsets: indices)
```

**学んだこと**
- スワイプ操作で削除を実装できる
- 削除対象のインデックスを取得できる
- 配列とUIが自動で同期される

---

## attendeeName

新規参加者の入力内容を管理するState。
```swift
@State private var attendeeName = ""
```

**学んだこと**
- TextFieldの入力内容を保持できる
- View専用の状態を管理できる
- 入力中の値をリアルタイムで保持できる

---
 
## withAnimation

追加時にアニメーションを付与する
```swift
withAnimation {
}
```
**学んだこと**
- State変更時にアニメーションを適用できる
- List更新を滑らかに表現できる

---
 
## attendeeName = ""
 
参加者追加後に入力欄をクリアする。
```swift
attendeeName = ""
```
 
**学んだこと**
- Stateを変更するとUIも更新される
- TextFieldの内容をリセットできる
 
---

## disabled
 
入力値の検証を行う。
```swift
.disabled(attendeeName.isEmpty)
```
 
### attendeeName.isEmpty
 
文字列が空かどうか判定する。
```swift
attendeeName.isEmpty
```
 
**学んだこと**
- ボタンの有効・無効を切り替えられる
- 不正な入力を防止できる
- ユーザーに操作可能な状態を分かりやすく伝えられる

---

## isPresentingEditView

編集画面が表示されているかどうかを保持する。

```swift
true
``` 
→ 編集画面を表示
 
```swift
false
```
→ 編集画面を非表示
 
**学んだこと**
- モーダル画面の表示状態を管理できる
- Stateの変更に応じて画面を表示・非表示にできる
- UIの状態をBooleanで管理できる

---

## sheet
 
モーダル画面を表示するための修飾子。
```swift
.sheet(isPresented: $isPresentingEditView) {
DetailEditView()
}
```

---

## モーダル画面（Modal）
 
現在の画面の上に表示される一時的な画面。
```text
DetailView
↓
DetailEditView
```
 
**学んだこと**
- メイン画面から一時的な作業画面へ遷移できる
- 編集や設定など短時間の操作に適している
- 作業終了後は元の画面へ戻る

---

## ToolbarItem
 
ツールバーへボタンを配置する。
 
```swift
.toolbar {
ToolbarItem {
}
}
```
 
**学んだこと**
- 画面上部へアクションボタンを配置できる
- ナビゲーションバーと連携できる

---
 
## Edit Button
 
編集画面を開くためのボタン。
 
```swift
Button("Edit") {
isPresentingEditView = true
}
```
 
### 処理
 
```swift
isPresentingEditView = true
```
↓
```swift
sheet表示
```
↓
```swift
DetailEditView表示
```
 
**学んだこと**
- ボタン押下でStateを変更できる
- State変更によって画面遷移を実現できる

---

### dismiss()
 
現在表示中のモーダル画面を閉じる。
```swift
dismiss()
```
 
**学んだこと**
- 編集をキャンセルできる
- モーダル画面を閉じられる
- iOS標準のUIパターンを実装できる

---

## 振り返り
 
このチュートリアルでは、SwiftUIで編集画面を作成し、ユーザー入力を管理する方法を学んだ。
 
- emptyScrumによる初期データの作成
- Formを利用した入力フォームの構築
- Sectionによる入力項目の整理
- TextFieldを利用したテキスト入力
- Binding（$）によるStateとの連携
- Sliderを利用した数値入力
- 計算プロパティによる型変換
- get・setによる値の取得と更新
- ForEachによる出席者一覧の表示
- onDeleteによる出席者の削除
- @Stateを利用したフォーム状態の管理
- attendeeNameを利用した入力値の保持
- Buttonによる出席者の追加
- withAnimationによるアニメーション付き更新
- disabledによる入力値検証
- sheetによるモーダル画面の表示
- isPresentingEditViewによる画面表示状態の管理
- ToolbarItemによるツールバーへのボタン配置
- Editボタンから編集画面を開く仕組み
- dismiss()によるモーダル画面の終了
 
特に、@StateとBindingを利用したフォーム入力の仕組みについて理解を深めることができた。
 
また、TextFieldやSliderの値をStateと連携させることで、ユーザーの操作に応じて画面を自動的に更新できることを学んだ。
 
さらに、sheetを利用したモーダル表示やdismiss()による画面の終了方法を学び、一覧画面と編集画面を連携させる基本的な画面遷移の流れを理解することができた。
 
これにより、SwiftUIでユーザー入力を扱うフォーム画面の作成から、編集画面の表示・終了までの一連の実装方法を学ぶことができた。
