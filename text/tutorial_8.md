# SwiftUIチュートリアル8

## リストを作成する

例

```swift
struct LandmarkList: View {
    var body: some View {
      List{
        LandmarkRow(landmark: landmarks[0])
        LandmarkRow(landmark: landmarks[1])
    }
  }
}
```

### リストを動的にする

例

```swift
struct LandmarkList: View {
    var body: some View {
        List(landmarks,id: \.id){landmark in
                LandmarkRow(landmark: landmark)
        }
    }
}
```

・`(landmarks,id:\.id)`:データは`landmarks`を使用し、各データは`id`変数で一意に識別する

・`landmark in`:データの個数分処理を繰り返す

### 記述を簡素化する

`Identifiable`をLandmarkに追加する

```swift
struct Landmark: Hashable, Codable, Identifiable
```

・`Identifiable`:その構造体が一意の`id`を持っていることを定義する

必ず`id`プロパティを定義しておく必要がある

これを行うと、リスト呼び出しの際に記述せずとも、自動で`id`で一意のデータを取得してくれる

```swift
// id:\.idの記述を省略
List(landmarks){landmark in
          LandmarkRow(landmark: landmark)
        }
    }
```
