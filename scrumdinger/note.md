# Using Stacks to Arrange Views

---

## 参考教材
https://developer.apple.com/tutorials/app-dev-training/using-stacks-to-arrange-views

---

## Viewの構成

### Viewとは

View はユーザーインターフェースの一部を定義するもので、アプリを構成する基本要素である。

**学んだこと**

- View は UI の部品
- SwiftUI は View の組み合わせで画面を構築する
- 複雑な画面は、小さくシンプルな View を組み合わせて作る

---

## Stack

SwiftUIでViewを並べるために用いる

- VStack：縦方向に並べる
- HStack：横方向に並べる

---

### VStackとは

VStack（Vertical Stack：垂直スタック）の略
- Viewを上から下へ縦に並べるコンテナ

```
VStack {
    Text("上")
    Text("下")
}
```

表示イメージ
```
上

下
```

---

### HStackとは

HStack（Horizontal Stack：水平スタック）の略
- Viewを左から右へ横に並べるコンテナ

```
HStack {
    Text("左")
    Text("右")
}
```

表示イメージ
```
左   右
```

---

## Label

 文字（Text）とアイコン（Image）をセットで表示するSwiftUIのView 

 ```
 Label("300", systemImage: "hourglass.tophalf.fill")
 ```

- `"300"` → 表示する文字
- `"hourglass.tophalf.fill"` → SF Symbolsのアイコン

### 学んだこと
- Text と Image をまとめて表示できる
- SF Symbols と組み合わせることで視覚的に分かりやすくなる
- アイコン付きの情報表示によく利用される

---

## alignment

- alignment: .leading：左揃え
- alignment: .trailing：右揃え
※デフォルトで中央揃え

**学んだこと**
- デフォルトは中央揃え
- `.leading` は先頭揃え
- `.trailing` は末尾揃え
- ローカライズ対応のため `left/right` ではなく `leading/trailing` を使用する

---

## Modifier

SwiftUIで View の見た目や動作を変更するための仕組み

**特徴**

- Viewをカスタマイズするために使用する
- Modifierは新しいViewを返す
- 複数のModifierを連結できる

### .font(.caption) とは
```
Text("Seconds Elapsed")
    .font(.caption)
```
この文字をcaptionサイズ(小さめの説明文サイズ)で表示してください

---

## Accessibility(アクセシビリティ)

- 視覚に障がいがある人
- 聴覚に障がいがある人
- 画面を見るのが難しい人
でもアプリを利用できるようにする仕組み

Apple では **VoiceOver** という画面読み上げ機能が提供されている


### Step1: 子ビューのアクセシビリティ情報を無視する
```
.accessibilityElement(children: .ignore)
```

**役割**
`HStack` 内の子ビューが持つ自動生成されたアクセシビリティ情報を無視する。

**学んだこと**
- VoiceOver は通常、子ビューを個別に読み上げる
- 情報が冗長になる場合がある
- 独自のアクセシビリティ情報を設定するための準備として利用する

### Step2: アクセシビリティラベルを設定する
```
.accessibilityLabel("Time remaining")
```

**役割**
VoiceOver に対して、その要素が何を表しているかを説明する。

**学んだこと**
- ユーザーに要素の目的を伝えられる
- 数値だけでは意味が伝わらない場合に有効
- 最も重要な情報を簡潔に伝えることが大切

### Step3: アクセシビリティ値を設定する
```
.accessibilityValue("10 minutes")
```

**役割**
アクセシビリティラベルに対応する具体的な値を設定する。

**学んだこと**
- `.accessibilityElement(children: .ignore)` を使用した場合は値も明示的に設定する
- VoiceOver 利用者に現在の状態を正しく伝えられる

### Step4: ボタンにアクセシビリティラベルを追加する
```
.accessibilityLabel("Next speaker")
```

**役割**
アイコンだけでは分からないボタンの意味を説明する。

**学んだこと**
- デフォルトでは VoiceOver はシステムイメージ名を読み上げる
- ユーザーに伝わりやすい説明を設定できる
- アイコンボタンでは特に重要

---

## 振り返り
 
このチュートリアルでは SwiftUI の基本構成を学んだ。
 
- View を組み合わせて画面を作る考え方
- VStack と HStack を利用したレイアウト
- Modifier を使った見た目の変更
- Accessibility を考慮した UI 設計
