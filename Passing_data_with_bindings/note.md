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

---

## ScrumsViewのBinding化
 
変更前
```swift
let scrums: [DailyScrum]
```
 
変更後
```swift
@Binding var scrums: [DailyScrum]
```
 
### 違い
 
```swift
let
```
- 読み取り専用
 
```swift
@Binding
```
- 親Viewが管理している値を参照・更新できる
 
**学んだこと**
- 配列全体をBindingとして受け取れる
- 下位ViewへBindingを渡せる
- データの変更を一覧画面へ反映できる

---
 
## Previewの修正
 
Binding対応後はPreviewにもBindingを渡す必要がある。
 
```swift
#Preview {
    @Previewable @State var scrums =DailyScrum.sampleData
     
    ScrumsView(scrums: $scrums)
}
```
 
### $scrums
 
```swift
$ scrums
```
↓
```swift
Binding<[DailyScrum]>
```
 
**学んだこと**
- Bindingを利用するViewにはBindingを渡す必要がある
- Previewでも同じルールが適用される

## DetailViewへのBinding受け渡し
 
変更前
```swift
DetailView(scrum: scrum)
```
 
変更後
```swift
DetailView(scrum: $scrum)
```
 
### 型
 
```swift
scrum
```
↓
```swift
DailyScrum
```
 
```swift
$scrum
```
↓
```swift
Binding<DailyScrum>
```
 
### 理由
 
DetailViewは
```swift
@Binding var scrum: DailyScrum
```
を要求しているため。
 
**学んだこと**
- BindingはView階層を通して渡せる
- 子Viewが親Viewのデータを編集できる
 
---

## ScrumdingerApp
 
アプリのエントリポイント。
 
```swift
@main
struct ScrumdingerApp: App {
}
```
 
### 役割
- アプリ起動時に最初に実行される
- 画面構成を決定する
- 共有データを保持する
 
**学んだこと**
- SwiftUIアプリの開始地点
- アプリ全体で共有する状態を管理できる

---

## 振り返り
 
このチュートリアルでは、SwiftUIにおけるBindingを利用したデータ共有と状態管理について学んだ。
 
- ThemeViewの作成
- Modifierの適用順序による表示の違い
- accentColorを利用した可読性の向上
- ThemePickerによるカスタムPickerの実装
- @Previewableを利用したインタラクティブなPreview
- pickerStyle(.navigationLink)によるナビゲーション形式のPicker
- @Bindingによる親Viewと子Viewのデータ共有
- ThemePickerへのテーマ情報の受け渡し
- editingScrumを利用した編集用データの管理
- DoneとCancelを考慮した編集画面の実装
- DetailViewのBinding化
- ScrumsViewのBinding化
- 配列Binding構文 `List($scrums)` の利用
- Binding<DailyScrum>の取得と利用
- DetailViewへのBinding受け渡し
- ScrumdingerAppでのState管理
- Single Source of Truthの実現
- アプリ全体へのBindingの伝播