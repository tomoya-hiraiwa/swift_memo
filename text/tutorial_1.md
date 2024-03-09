# Swift UI チュートリアル1

## ビューの作成と結合

### アプリのエントリーポイント

→`@main`属性

>[!TIP]
> ### PreViewが表示されない場合
>
>Xcode>Product>Clean Build Folderを実行

### Previewをキャンバスモードにする

Preview画面下部の矢印のアイコンをクリックして設定

`Command`+`Control`を押しながらUIをクリック→Show SwiftUI Inspectorを選択

### SwiftUIのCVIewをカスタマイズするには、`modifiers`というメソッドを呼びだす

（Jetpack Composeとも似ている）

例(Textのフォントをtitle、色を緑にする)

```swift
struct ContentView: View {
    var body: some View {
        Text("Hello SwiftUI!")
            .font(.title)
            .foregroundColor(.green)
    }
}
```

・SwiftUI Inspectorで行った設定はすぐにコードにも反映され、更新される

### スタックを利用する

・Stackを入れたいViewを`control`+クリックして、`Embed in Vstack`などを選択する

### ライブラリからViewの追加

Xcodeウィンドウ右上`+`をクリック→追加したいViewを入れたい場所にドラッグ&ドロップ

### Stack内のViewの配置レイアウトを指定

→alignment属性に定義

例(Viewの始端位置を合わせる)

```swift
struct ContentView: View {
    var body: some View {
        VStack(alignment:.leading) {
            Text("Hello SwiftUI!")
                .font(.title)
            Text("Joshua Tree National Park")
                .font(.subheadline)
        }
            
    }
}
```

### デバイスの幅いっぱいに使用する

→`Spacer()`を使用

### 周囲に余白をつける

→`.padding()`

例

```swift
struct ContentView: View {
    var body: some View {
        VStack(alignment:.leading) {
            Text("Hello SwiftUI!")
                .font(.title)
            HStack {
                Text("Joshua Tree National Park")
                    .font(.subheadline)
                Spacer()
                Text("California")
                    .font(.subheadline)
            }
        }
        .padding()
    }
}
```
