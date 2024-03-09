# SwiftUIチュートリアル5

## モデルの作成

### データソースファイルの追加

追加したいフォルダをXCodeのファイルナビゲーションにドラッグ&ドロップ

### 構造体の定義

例

```swift
struct Landmark: Hashable, Codable {
    var id: Int
    var name: String
    var park: String
    var state: String
    var description: String
}
```

・`Hashble`:ハッシュ値の使用ができるという設定

・`Codable`:jsonなどをこのデータ型に変換できるという設定

### 画像の名前を取得するプロパティと画像を読み込むプロパティの設定

例

```swift
struct Landmark: Hashable, Codable {
    var id: Int
    var name: String
    var park: String
    var state: String
    var description: String

    private var imageName: String
    var image: Image{
        Image(imageName)
    }
}
```

・画像の名前は直接使用することはないため、`privarte`にしておく

### 座標用のプロパティを追加する

例

```swift
struct Landmark: Hashable, Codable {
    var id: Int
    var name: String
    var park: String
    var state: String
    var description: String

    private var imageName: String
    var image: Image{
        Image(imageName)
    }
    
    private var coordinates: Coodinates
    
    struct Coodinates: Hashable, Codable{
        var latitude: Double
        var longitude: Double
    }
}
```

・`coordinates`プロパティの形として`Coodinates`構造体をネストしている

>[!NOTE]
>kotlinのデータクラスとして考えると、この構造は
>
> ```kotlin
> data class Landmark(
>   val id: Int,
>   val name: String,
>   val park: String,
>   val state: String,
>   val description: String,
>   val coordinates: Coordinates
> )
> data class Coordinates(
>   val latitude: Double,
>   val longitude: Double
> )
> ```
> と変換することができる

### Mapの緯度と軽度を表す`CLLocationCoordinate2D`プロパティの追加

例

```swift
struct Landmark: Hashable, Codable {
    var id: Int
    var name: String
    var park: String
    var state: String
    var description: String

    private var imageName: String
    var image: Image{
        Image(imageName)
    }
    
    private var coordinates: Coodinates
    
    var locationCoordinate: CLLocationCoordinate2D{
        CLLocationCoordinate2D(
            latitude: coordinates.latitude,
            longitude: coordinates.longitude
        )
    }
    
    struct Coodinates: Hashable, Codable{
        var latitude: Double
        var longitude: Double
    }
}
```

### JSONデータを取得する

例

```swift
func load<T: Decodable>(_ filename: String) -> T {
    let data: Data
    
    guard let file = Bundle.main.url(forResource: filename, withExtension: nil)
    else{
        fatalError("Couldn't find \(filename) in main bundle.")
    }
    //ファイルデータを読み出し
    do{
        data = try Data(contentsOf: file)
    } catch{
        fatalError("Couldn't load \(filename) from main bundle:\n\(error)")
    }
    //
    do{
        let decoder = JSONDecoder()
        return try decoder.decode(T.self, from: data)
    }catch{
        fatalError("Couldn't parse \(filename) as \(T.self):\n\(error)")
    }
}
```

・`<T DEcodable>`:`Decodable`な任意の形を読み込み、デコードする

・`(_ fileName: String)`:　`_`はデコードするオブジェクトの型を推論する、 `fileName`はデコードしたいファイル名

・`guard let~`：デコードしたいファイルのURLを取得する。失敗時は`else`ブロックのエラーを出す






