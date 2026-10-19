# Responding to events

---

## 参考教材
https://developer.apple.com/tutorials/app-dev-training/responding-to-events

---

## Scene

Sceneとは、システムが管理するアプリのUI単位。

```swift
@main
struct ScrumdingerApp: App {
    var body: some Scene {
        WindowGroup {
            ScrumsView()
        }
    }
}
```
SwiftUIでは `Scene` がView階層を保持し、表示やライフサイクルを管理する。 

**学んだこと**
- SceneはアプリのUIを管理する単位
- Sceneの中にView階層を配置する
- SwiftUIがライフサイクルを管理する
- アプリは1つ以上のSceneを持てる

---

## @main

アプリのエントリーポイントを表す属性。

```swift
@main
struct ScrumdingerApp: App {
}
```
アプリ起動時に最初に実行される構造体を指定する。 

---

## WindowGroup

SwiftUIが提供する代表的なScene。

```swift
WindowGroup {
    ScrumsView()
}
```
View階層を表示するためのコンテナとして利用する。

**学んだこと**
- Sceneとして利用できる
- ルートViewを表示できる
- SwiftUIアプリの基本構成で利用する

---
 
## scenePhase
 
現在のScene状態を取得する環境値。
 
```swift
@Environment(\.scenePhase)
private var scenePhase
```
 
利用できる状態
 
```swift
.active
```
 
```swift
.inactive
```
 
```swift
.background
```

**学んだこと**
- 現在のScene状態を取得できる
- 状態変化を監視できる
- フォアグラウンドやバックグラウンド処理に利用できる
 
---
 
## SwiftUIのイベント処理
 
SwiftUIではイベント発生後、状態変更を通じてUIが更新される。 
 
```text
イベント発生
↓
処理実行
↓
State変更
↓
SwiftUIが検知
↓
UI再描画
```

### 例
 
```swift
Button("Add") {
count += 1
}
```
ボタンタップでStateが変わると、関連するViewが自動的に更新される。

**学んだこと**
- Stateの変更がUI更新の起点になる
- UI更新処理は自動で行われる
- 宣言的UIの基本的な流れを理解できる
 
---
 
## View Life Cycle
 
Viewの表示・非表示に関するライフサイクル。
 
SwiftUIではViewの状態変化に応じて処理を実行できる。
 
---
 
## onAppear
 
Viewが画面に表示されたときに実行される。
 
```swift
.onAppear {
print("View appeared")
}
```
 
利用例
- データ取得
- タイマー開始
- 初期化処理

**学んだこと**
- View表示時に処理を実行できる
- 再表示時にも呼ばれる
- 初期化処理によく利用する
 
---
 
## onDisappear
 
Viewが画面から消えたときに実行される。
 
```swift
.onDisappear {
print("View disappeared")
}
```

利用例 
- タイマー停止
- データ保存
- リソース解放
 
**学んだこと**
- View終了時に処理を実行できる
- 後片付け処理に利用できる
- 不要な処理を停止できる
 
---
 
## 振り返り
 
このチュートリアルでは、SwiftUIのイベント処理とライフサイクル管理について学んだ。
 
- SceneによるUI管理
- `@main` の役割
- `WindowGroup` の利用方法
- Scene Phase（active / inactive / background）
- `scenePhase` を利用した状態取得
- イベント発生からUI更新までの流れ
- SwiftUIの宣言的UI
- View Life Cycle
- `onAppear`
- `onDisappear`
- タイマーやデータ保存への応用
 
SwiftUIでは、イベントが発生すると状態（State）が変化し、その状態変化をシステムが検知して自動的にUIを更新する。また、`onAppear` や `onDisappear` を利用することで、Viewの表示・非表示に応じた処理を簡潔に実装できることを学んだ。