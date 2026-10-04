# Creating a navigation hierarchy

---

## 参考教材
https://developer.apple.com/tutorials/app-dev-training/creating-a-navigation-hierarchy

---

## NavigationStack

画面遷移を管理するためのコンテナView
```
NavigationStack {
    List(scrums) { scrum in
        CardView(scrum: scrum)
    }
}
```
NavigationStackの中で画面を遷移すると、ビューがスタック構造で管理される。
**学んだこと**
- SwiftUIで画面遷移を管理するためのコンテナ
- 画面はスタック構造で保持される
- 詳細画面へ進むとスタックに追加される
- 戻るとスタックから削除される
- ルート画面では戻るボタンは表示されない

---

## NavigationLink

画面遷移を行うためのView
```
NavigationLink(
    destination: Text(scrum.title)
) {
    CardView(scrum: scrum)
}
```
ユーザーが行をタップすると、指定したViewへ遷移する。


### destination
destination は遷移先の画面を指定する。
```
destination: Text(scrum.title)
```

例えば、
```
scrum.title == "Design"
```
の場合、Text("Design")に遷移する。

**学んだこと**
- destinationで遷移先を指定する
- 任意のViewを遷移先に設定できる
- 今回は詳細画面の代わりとして Text を利用している
- 後で詳細画面(View)へ置き換えられる

---

## listRowBackground

Listの行背景を設定するModifier
```
.listRowBackground(scrum.theme.mainColor)
```

**学んだこと**
- Listの各行の背景色を変更できる
- NavigationLinkに適用することで行全体に反映できる
- Themeと組み合わせて統一感のあるUIを作れる

---

# navigationTitle

ナビゲーションバーのタイトルを設定するModifier
```
.navigationTitle("Daily Scrums")
```
ナビゲーションバー上部にタイトルを表示する。

**学んだこと**
- 画面タイトルを設定できる
- NavigationStackの表示に反映される
- ユーザーが現在の画面を認識しやすくなる

---

# Toolbar

ナビゲーションバーにボタンやメニューを追加するModifier
```
.toolbar {
    Button(action: {}) {
        Image(systemName: "plus")
    }
}
```

**学んだこと**
- ナビゲーションバーに機能を追加できる
- Buttonを配置できる
- 新規作成や編集などの操作に利用される

---

## DetailView

スクラムの詳細情報を表示するための画面（View）
```
struct DetailView: View {
    var body: some View {
        Text("Hello, World!")
    }
}
```
一覧画面から選択されたスクラムの詳細を表示する役割を持つ。

**学んだこと**
- 詳細画面用のViewを作成できる
- 1画面ごとにViewを分割して管理できる
- SwiftUIでは画面ごとに独立したViewを作成する

---

## DailyScrumの受け取り

DetailViewは表示するスクラム情報を受け取る必要がある。
```
let scrum: DailyScrum
```
これにより、選択されたスクラムのデータを画面で利用できる。

---

## Initializerの自動生成

```
let scrum: DailyScrum
```
を追加すると、Swiftが自動でイニシャライザを生成する。
```
DetailView(scrum: someScrum)
```
のように呼び出せるようになる。

**学んだこと**
- structのプロパティから自動でイニシャライザが生成される
- 必須パラメータを渡さないとコンパイルエラーになる
- データの受け渡しを安全に行える

---

## Previewへのデータ渡し

DetailViewに必須パラメータが追加されたため、Previewでも値を渡す必要がある。
```
#Preview {
    DetailView(
        scrum: DailyScrum.sampleData[0]
    )
}
```
サンプルデータを利用してプレビューを表示する。

**学んだこと**
- Previewでも実際のViewと同じ引数が必要
- sampleDataを活用して表示確認できる
- 開発中に実データがなくても確認できる

---

## Identifiable

ForEach や List が要素を識別するためのプロトコル
```
struct Attendee: Identifiable
```
SwiftUIは各要素を一意に識別して画面更新を行う

---

## attendeesの型変更

変更前
```
var attendees: [String]
```
変更後
```
var attendees: [Attendee]
```
参加者を単なる文字列ではなく、モデルとして管理する。

**学んだこと**
- データ構造をより柔軟にできる
- 名前以外の情報も追加しやすくなる
- Identifiableに対応できる

---

## map(_:)

コレクションの要素を別の型へ変換するメソッド
```
self.attendees = attendees.map {
    Attendee(name: $0)
}
```

イメージ
変更前
```
["A", "B", "C"]
```
変更後
```
[
    Attendee(name: "A"),
    Attendee(name: "B"),
    Attendee(name: "C")
]
```

**学んだこと**
- 配列の型変換ができる
- 変換後の新しい配列を作成できる
- Swiftで頻繁に利用される関数型メソッド

---

## ForEach

コレクションの要素を繰り返し表示するView
```
ForEach(scrum.attendees) { attendee in
}
```
参加者の数だけViewが生成される

**学んだこと**
- 配列を繰り返し表示できる
- SwiftUIで動的なUIを構築できる
- データ数に応じて自動で表示数が変わる

---

## NavigationLink

タップ操作による画面遷移を実現するView
```
NavigationLink(
    destination: MeetingView()
)

```

**学んだこと**
- タップで別画面へ遷移できる
- destinationに遷移先を指定する
- SwiftUIがナビゲーション状態を管理してくれる


---

## 振り返り

このチュートリアルでは、参加者一覧を詳細画面に表示する仕組みを学んだ。

- Attendeeモデルの作成
- Identifiableへの準拠
- UUIDによる一意な識別
- attendeesの型を[String]から[Attendee]へ変更
- map(_:)を利用したデータ変換
- Sectionによる情報整理
- ForEachによる繰り返し表示
- attendeeを利用したデータ取得
- Labelによるアイコン付き表示
- SwiftUIでの動的リスト生成
- 複数画面を組み合わせたアプリ構成の理解

これにより、固定のUIだけでなく、データの件数に応じて自動で画面を構築するSwiftUIの基本的な考え方を学ぶことができた。