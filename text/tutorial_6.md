# SwiftUIチュートリアル6

## リスト用の行Viewを作成する

### プロパティの追加

例(Landmark型のlandmark変数を追加)

```swift
struct LandmarkRow: View {
    var landmark: Landmark
    var body: some View {
        HStack {
            Text(/*@START_MENU_TOKEN@*/"Hello, World!"/*@END_MENU_TOKEN@*/)
        }
    }
}
```

### Previewを修正する

・プロパティを追加したことで、このviewにはLandmark型のデータが必要になったので、引数として渡す

```swift
#Preview {
    LandmarkRow(landmark: landmarks[0]) //ModelDataファイルのlandmarksプロパティの一つ目のデータを渡す
}
```

### データの表示

例

```swift
struct LandmarkRow: View {
    var landmark: Landmark
    var body: some View {
        HStack {
            landmark.image
                .resizable()
                .frame(width: 50, height: 50) //横幅、縦幅それぞれ50のサイズのViewにする
            Text(landmark.name)
            Spacer() //左寄せにするために右側の余白を埋めるSpacer()を入れる
        }
    }
}
```

`.resizable`:親のViewのサイズに合わせて自動的に画像をリサイズする
