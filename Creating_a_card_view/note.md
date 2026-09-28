# Creating a card view

---

## 参考教材
https://developer.apple.com/tutorials/app-dev-training/creating-a-card-view

---

## DailyScrum Model

DailyScrum は 1 回分のスクラムミーティングを表すデータモデル

Scrumdinger アプリでは、会議名・参加者・時間・テーマカラーなど、スクラムに関する情報をこのモデルで管理する
```
struct DailyScrum {
    var title: String
    var attendees: [Attendee]
    var lengthInMinutes: Int
    var theme: Theme
}
```

**学んだこと**
- DailyScrum はスクラム会議を表すデータモデル
- 関連する情報を1つにまとめて管理できる
- モデルを利用することで View とデータを分離できる
- struct は値型であり、安全にデータを扱える
- SwiftUI ではデータモデルとして struct がよく利用される

---

## SampleData

実際のユーザーデータの代わりに開発中やプレビュー表示で使用するダミーデータのこと

```
extension DailyScrum {
    static let sampleData: [DailyScrum] = [...]
}
```

---

## Preview Content

SwiftUI の Preview や開発時の確認に使用するリソースを配置するフォルダ。

- サンプルデータ
- テスト用画像
- 開発用アセット

などを保存できる。

**学んだこと**
- 開発・デバッグ用のデータを管理できる
- SwiftUI Previewで使用される
- 本番ユーザー向けのデータではない
- アプリの最終リリースには含まれない

---

## CardView

1つのスクラムミーティングの情報をカード形式で表示するためのView
これまで作成した `DailyScrum` のデータを受け取り、画面上に表示する役割を持つ

**学んだこと**
View はデータを受け取って表示できる
DailyScrum の情報を画面に反映できる
Model と View を分離して管理できる

## DailyScrumの受け取り

CardViewは DailyScrum を受け取って表示する
```
let scrum: DailyScrum
```

利用例
```
CardView(scrum: scrum)
```

**学んだこと**
- View はパラメータとしてデータを受け取れる
- 表示する内容は渡されたデータによって決まる
- SwiftUI ではデータ駆動でUIを構築する

---

## Preview

アプリを実行しなくても UI を確認できる機能
```
#Preview {
    let scrum = DailyScrum.sampleData[0]
    CardView(scrum: scrum)
}
```

**学んだこと**
- 実機やシミュレータを起動せずに確認できる
- サンプルデータを利用できる
- UI開発の効率を向上できる

---

## fixedlayout

Preview のサイズを固定するための設定
```
#Preview(
    traits: .fixedLayout(
        width: 400,
        height: 60
    )
)
```

**学んだこと**
- Preview の幅と高さを指定できる
- View単体のレイアウトを確認しやすくなる
- UIの見た目を調整しやすくなる

---

## ThemeとBackground

背景色の設定
theme.mainColor を使用して背景色を設定する
```
.background(scrum.theme.mainColor)
```

---

## Color Scheme Variant

Xcode Previewでライトモードとダークモードを同時に確認できる機能

### ダークモードの問題
 
背景色が黄色の場合、
 
```swift
.background(scrum.theme.mainColor)
```

ダークモードではテキストが見づらくなる場合がある

---

## foregroundStyle

テキストやアイコンの色を設定するModifier
```
.foregroundStyle(scrum.theme.accentColor)
```

**学んだこと**
- テキスト色を変更できる
- アイコン色も変更できる
- テーマに応じた見やすい表示ができる

---
 
## accentColor

Themeに応じて適切な文字色を返すプロパティ
```
scrum.theme.accentColor
```

---

## LabelStyle

`LabelStyle` は、SwiftUI の `Label` の見た目やレイアウトをカスタマイズするためのプロトコル

---

## TrailingIconLabelStyle

アイコンをテキストの後ろに表示するためのカスタムLabelStyle
```
struct TrailingIconLabelStyle: LabelStyle {
}
```

**学んだこと**
- 独自のLabelStyleを作成できる
- 共通のレイアウトを部品化できる
- SwiftUIの再利用性を高められる

---

## makeBody(configuration:)

Labelの表示方法を定義するメソッド

```
func makeBody(configuration: Configuration) -> some View {
}
```

システムは `Label` が表示されるたびにこのメソッドを呼び出す

**学んだこと**
- Labelの見た目を定義する場所
- LabelStyleで必須となるメソッド
- レイアウトのカスタマイズに利用される

---

## Configuration

Labelが持つ情報を格納したオブジェクト

```
configuration
```
には、Labelのテキストやアイコンが含まれている。

---

## 振り返り

このチュートリアルでは、Scrumdinger のカード画面を作成しながら、SwiftUI のデータ管理とUI設計の基本を学んだ。
- DailyScrum を利用したデータモデルの設計
- sampleData を利用した開発用データの管理
- CardView を利用したモデルとViewの分離
- Preview を活用した効率的なUI開発
- VStack、HStack、Spacer を使ったレイアウト構築
- padding や font を利用したUIの調整
- theme.mainColor と theme.accentColor を利用したテーマ管理
- ライトモード・ダークモードを考慮したUI設計
- LabelStyle を利用したコンポーネントの再利用
- アクセシビリティを考慮したUI設計
