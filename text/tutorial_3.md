# SwiftUI チュートリアル3

## 他のフレームワークのSwiftUIVIewを使用

### import

使用したいフレームワークを`import`でインポートする

例(MapKitの場合)

```swift
import MapKit
```

### Mapの中心座標と表示範囲を保持する変数を作成

例

```swift
struct MapView: View {
    var body: some View {
        Text(/*@START_MENU_TOKEN@*/"Hello, World!"/*@END_MENU_TOKEN@*/)
    }
    private var region: MKCoordinateRegion{
        MKCoordinateRegion(
            //中心座標を設定　緯度と軽度で指定
            center: CLLocationCoordinate2D(latitude: 34.011_236, longitude: -116.166_868),
            //表示範囲を指定、緯度・軽度ともに0.2度の範囲を表示
            span: MKCoordinateSpan(latitudeDelta: 0.2, longitudeDelta: 0.2)
        )
    }
}
```

### Mapを表示する

例(上で作成した位置を初期位置として　表示)

```swift
var body: some View {
        Map(initialPosition: .region(region))
    }
```




