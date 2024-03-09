# SwiftUIチュートリアル9

## リストと詳細画面とのナビゲーション

### リストをNavigatonSplitViewで囲む

例

```swift
struct LandmarkList: View {
    var body: some View {
        NavigationSplitView{
            List(landmarks){landmark in
                LandmarkRow(landmark: landmark)
            }
        } detail: {
            Text("Select a Landmark")
        }
    }
}
```
`NavigationSplitView`:リストと詳細画面を分割するように画面を遷移するもの

`detail`に書かれているものが詳細側のデフォルトのView

### タイトルを設定

例

```swift
struct LandmarkList: View {
    var body: some View {
        NavigationSplitView{
            List(landmarks){landmark in
                LandmarkRow(landmark: landmark)
            }
            //タイトルの設定
            .navigationTitle("Landmarks")
        } detail: {
            Text("Select a Landmark")
        }
    }
}
```

### 遷移先の指定

・`NavigatonLink`で設定

例

```swift
struct LandmarkList: View {
    var body: some View {
        NavigationSplitView{
            List(landmarks){landmark in
                NavigationLink{
                    LandmarkDetail()
                } label: {
                    LandmarkRow(landmark: landmark)
                }
            }
            .navigationTitle("Landmarks")
        } detail: {
            Text("Select a Landmark")
        }
    }
}
```

・`NavigationLink`内に遷移先のViewを指定

・`label`内に遷移元のViewを指定

## データを受け渡す

### CircleImageの変更

例

```swift
struct CircleImage: View {
    //ImageViewを引数で受ける
    var image: Image
    var body: some View {
        image
            .clipShape(/*@START_MENU_TOKEN@*/Circle()/*@END_MENU_TOKEN@*/)
            .overlay{
                Circle().stroke(.white, lineWidth: 4)
            }
            .shadow(radius: 7)
    }
}
#Preview {
    CircleImage(image: Image("turtlerock"))
}
```

### MapViewの変更

例

```swift
truct MapView: View {
    var coordinate: CLLocationCoordinate2D
    
    var body: some View {
        Map(position: .constant(.region(region)))
    }
    private var region: MKCoordinateRegion{
        MKCoordinateRegion(
            //中心座標を受け取った値で設定
            center: coordinate,
            span: MKCoordinateSpan(latitudeDelta: 0.2, longitudeDelta: 0.2)
        )
    }
}

#Preview {
    MapView(coordinate: CLLocationCoordinate2D(latitude: 34.011_286, longitude: -116.166_868))
}
```

`initialPosition`は地図の中心をユーザーが変更できる（地図を動かせる）のに対して、

`position`は渡された座標および表示範囲で固定される

### 詳細Viewおよび、一覧Viewの設定

・詳細

例

```
struct LandmarkDetail: View {
    var landmark: Landmark
    var body: some View {
        VStack{
            MapView()
                .frame(height: 300)
            CircleImage()
                .offset(y: -130)
                .padding(.bottom, -130)
            VStack(alignment:.leading) {
                Text("Turtle Rock")
                    .font(.title)
                HStack {
                    Text("Joshua Tree National Park")
                    Spacer()
                    Text("California")
                }
                .font(.subheadline)
                .foregroundStyle(.secondary)
            
                Divider()
                Text("About Turtle Rock")
                    .font(.title2)
                Text("Descriptive text goes here.")
            }
            .padding()
            Spacer()
        }
    }
}
```

・`landmark`プロパティの追加

・一覧

例

```swift
struct LandmarkList: View {
    var body: some View {
        NavigationSplitView{
            List(landmarks){landmark in
                NavigationLink{
                    LandmarkDetail(landmark: landmark)
                } label: {
                    LandmarkRow(landmark: landmark)
                }
            }
            .navigationTitle("Landmarks")
        } detail: {
            Text("Select a Landmark")
        }
    }
}
```

・`LnadmarkDetail`呼び出し時に、`landmark`データを渡す

### 詳細画面の値の引数受け渡し

例

```swift
struct LandmarkDetail: View {
    var landmark: Landmark
    var body: some View {
        VStack{
            MapView(coordinate: landmark.locationCoordinate)
                .frame(height: 300)
            CircleImage(image: landmark.image)
                .offset(y: -130)
                .padding(.bottom, -130)
            VStack(alignment:.leading) {
                Text(landmark.name)
                    .font(.title)
                HStack {
                    Text(landmark.park)
                    Spacer()
                    Text(landmark.state)
                }
                .font(.subheadline)
                .foregroundStyle(.secondary)
            
                Divider()
                Text("About \(landmark.name)")
                    .font(.title2)
                Text(landmark.description)
            }
            .padding()
            Spacer()
        }
    }
}
```

### スクロール可能にする

・全体を囲っている`VStack`を`ScrollView`に変更する

### ナビゲーションのタイトルと表示スタイルを設定する

例

```swift
struct LandmarkDetail: View {
    var landmark: Landmark
    var body: some View {
        ScrollView{
            MapView(coordinate: landmark.locationCoordinate)
                .frame(height: 300)
            CircleImage(image: landmark.image)
                .offset(y: -130)
                .padding(.bottom, -130)
            VStack(alignment:.leading) {
                Text(landmark.name)
                    .font(.title)
                HStack {
                    Text(landmark.park)
                    Spacer()
                    Text(landmark.state)
                }
                .font(.subheadline)
                .foregroundStyle(.secondary)
            
                Divider()
                Text("About \(landmark.name)")
                    .font(.title2)
                Text(landmark.description)
            }
            .padding()
        }
        //タイトルと表示スタイルを設定
        .navigationTitle(landmark.name)
        .navigationBarTitleDisplayMode(.inline)
    }
}
```

・これを設定すると、遷移した時に画面上部にそのランドマークの名前が表示される


