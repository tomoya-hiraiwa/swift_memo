# SwiftUIチュートリアル7

## Previewのカスタマイズ

### Previewに名前をつける

例

```swift
#Preview("Turtle Rock") {
    LandmarkRow(landmark: landmarks[0])
}

#Preview("Salmon"){
    LandmarkRow(landmark: landmarks[1])
}
```

### Previewのグループ化

例

```swift
#Preview("Turtle Rock") {
    Group{
        LandmarkRow(landmark: landmarks[0])
        LandmarkRow(landmark: landmarks[1])
    }
}
```

このようにすると、Previewが縦に並んで表示される

