# SwiftUIチュートリアル2

## 画像の追加とカスタム画像Viewの作成

### 画像の追加

`Assets.xcodeassets`フォルダを選択→画像をドラッグ&ドロップ

### 新しいSwiftUIViewの作成

`File`>`New`>`File`→`SwiftUI View`を選択→名前をつけてCreate

### 画像の配置

→`Image()`を使用

表示したい画像名を渡す

例

```swift
struct CircleImage: View {
    var body: some View {
        Image("turtlerock")
    }
}
```

### 形状の加工

→`.clipShape()`を使用

例（円形にする）

```swift
Image("turtlerock")
    .clipShape(Circle())
```

### オーバーレイの作成

`.overlay`を使用

例（画像の周りに4の太さのグレーの線をつける）

```swift
 Image("turtlerock")
            .clipShape(Circle())
            .overlay{
                Circle().stroke(.gray, lineWidth: 4)
            }
```

### 影の作成（浮いてるように見せる）

→`.shaddow`を使用、`radius`属性に影の大きさを指定する

### 円形画像Viewの完成例

```swift
struct CircleImage: View {
    var body: some View {
        Image("turtlerock")
            .clipShape(Circle())
            .overlay{
                Circle().stroke(.white, lineWidth: 4)
            }
            .shadow(radius: 7)
    }
}
```
