# Passing data with binding

---

## 参考教材
https://developer.apple.com/tutorials/app-dev-training/passing-data-with-bindings

---

## Modifierの順番
 
修飾子の順番によって結果が変わる。
 
### 推奨
 
```swift
.frame(maxWidth: .infinity)
.background(theme.mainColor)
```
 
### 順番を逆にした場合
 
```swift
.background(theme.mainColor)
.frame(maxWidth: .infinity)
```
 
背景色が期待した範囲まで広がらない。
 
**学んだこと**
- SwiftUIは上から順番に処理される
- Modifierの順序はUIに影響する
 
---

## accentColor
 
文字色として利用するカラー。
 
```swift
.foregroundStyle(theme.accentColor)
```
 
### theme.accentColor
 
メインカラーと十分なコントラストを持つ色。

```swift
theme.accentColor
```
↓
```text
黒 または 白
```
 
**学んだこと**
- 可読性を向上できる
- テーマごとに適切な文字色を設定できる

---

## ThemePicker
 
テーマを選択するためのカスタムView。
 
```swift
struct ThemePicker: View {
}
```
ThemeViewを利用して、利用可能なテーマを一覧表示する。
 
**学んだこと**
- カスタムPicker用のViewを作成できる
- Viewを分割して再利用できる
- テーマ選択専用のUIを独立して管理できる
 
---

## @Previewable
 
Preview内で変更可能な状態を作る。
 
```swift
@Previewable @State var theme = Theme.periwinkle
```
 
### Preview
 
```swift
#Preview {
@Previewable @State var theme = Theme.periwinkle
 
ThemePicker(selection: $theme)
}
```
 
**学んだこと**
- Preview上で状態変更を試せる
- 実際の操作に近いプレビューを作成できる
- Bindingを持つViewの確認に便利

---

## pickerStyle
 
Pickerの表示形式を変更する。
 
```swift
.pickerStyle(.navigationLink)
```
 
### navigationLink
 
ナビゲーション形式のPicker。
 
```swift
.pickerStyle(.navigationLink)
```
 
**学んだこと**
- Pickerの見た目を変更できる
- 選択画面を別画面として表示できる
- iOS標準の設定画面に近いUIを作れる

---
 
## データの流れ
 
```text
DetailEditView
↓
$scrum.theme
↓
ThemePicker
↓
ユーザーが選択
↓
scrum.theme更新
```

---

## editingScrum
 
編集用の一時データ。
 
```swift
@State private var editingScrum =
DailyScrum.emptyScrum
```
 
### 役割
 
```text
元のデータ
↓
編集用にコピー
↓
編集
↓
Doneなら反映
Cancelなら破棄
```
 
**学んだこと**
- 編集中の変更を一時保存できる
- Cancel時に元データを保持できる

---
 
## DetailView Preview
 
Binding対応後のPreview。
 
```swift
#Preview {
@Previewable @State var scrum =
DailyScrum.sampleData[0]
 
NavigationStack {
DetailView(scrum: $scrum)
}
}
```
 
**学んだこと**
- Bindingを利用するViewにはBindingを渡す必要がある
- Previewでも同じルールが適用される