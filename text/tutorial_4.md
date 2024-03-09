#SwiftUIチュートリアル4

## 作成したViewを組み合わせる

### MapViewの追加

例(ContentView.swift)

```swift
struct ContentView: View {
    var body: some View {
        VStack{
            MapView()
                .frame(height: 300)
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
}
```

`.frame()`属性：`width`で横幅を、`height`で縦幅を指定できる

> [!NOTE]
> パラメータの指定をしない場合、Viewはコンテンツの幅に自動的に合わせる

### CircleImageを追加

例

```swift
struct ContentView: View {
    var body: some View {
        VStack{
            MapView()
                .frame(height: 300)
            CircleImage()
                .offset(y: -130)
                .padding(.bottom, -130)
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
}
```

`.offset()`属性:Viewを`x`,`y`で指定された分動かす

今回であればMapViewの下からyが-130の位置、つまりMapViewに-130ぶんだけ被せて表示される

`.padding()`で`bottom`に-130を指定することで、`.offset()`で引き上げた分の下部の余白を削っている

### 区切り線の追加

`Divider()`を使用する

### Stack内の全てのViewにスタイルを適用する

・使用しているStackの修飾子として設定すると、その中のすべてのViewに設定が適用される

例(fontと表示スタイルを指定)

```swift
 HStack {
    Text("Joshua Tree National Park")
    Spacer()
    Text("California")
}
.font(.subheadline)
.foregroundStyle(.secondary)
```

