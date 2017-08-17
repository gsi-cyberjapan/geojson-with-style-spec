geojson-with-style-spec
=======================
# スタイルつき GeoJSON 規約
※この規約は検討中のものであり、今後変更する可能性がある。
## 適用範囲
この文書は、スタイル属性を GeoJSON ファイルの内部に埋め込む方法を定義する。スタイル属性を埋め込んだ GeoJSON ファイル（以下「スタイルつき GeoJSON」という）は、今後「[KMLウェブ地図プロファイル](https://maps.gsi.go.jp/help/pdf/16Jun2015_kmp.pdf)」（PDF）を置き換えていくことを想定している。

## 規約
1. properties に、Leaflet の path オプションその他のスタイル属性を埋め込む。但し、スタイル用のオプションであることを明示するために、オプション名の前にはアンダーバー(_)を加える。
2. スタイル属性は、Leaflet の Icon, DivIcon, Circle, CircleMarker に用いられているものを用いる。また、これらのうちどのマーカー種類を使うか明示するため、_markerType にクラス名（Icon, DivIcon, Circle 又は CircleMarker）を記載する。

## サンプル
```json
{"type": "FeatureCollection", "features": [
{
  "type": "Feature",
  "geometry": {"type": "Point", "coordinates": [135, 35]},
  "properties": {
    "名称": "○○公園",
    "住所": "○○県○○市○○",
    "_markerType": "Icon", 
    "_iconUrl": "https://cyberjapandata.gsi.go.jp/portal/sys/v4/symbols/010.png", 
    "_iconSize": [20, 20],
    "_iconAnchor": [10, 10],
    "_className": "park"
  }
}
]}
```

## スタイル属性一覧

|属性名|属性値|デフォルト|
|:----|:----|:--|
|_markerType|Icon/DivIcon/Circle/CircleMarker|Icon|
|_className, _stroke, _color, _weight, _opacity, _fill, _fillColor, _fillOpacity, _dashArray, _lineCap, _lineJoin, _clickable|L.Pathの仕様による|L.Pathの仕様による|
|_iconUrl, _iconSize, _iconAnchor|L.Iconの仕様による|L.Iconの仕様による|
|_html,|L.DivIconの仕様による|L.DivIconの仕様による|
|_radius,|L.Circle, L.CircleMarkerの仕様による|L.Circle, L.CircleMarkerの仕様による|

## サンプルサイト
スタイルつき GeoJSONをLaefletで表示するサンプルです。
- 外部ファイルを表示
https://gsi-cyberjapan.github.io/geojson-with-style-spec/sample1.html
- htmlに埋め込み
https://gsi-cyberjapan.github.io/geojson-with-style-spec/sample2.html

## 今後の課題
- 「KMLウェブ地図プロファイル」からの上位互換性の確保。
- ~~2015年7月15日現在、地理院地図（https://maps.gsi.go.jp/ ）では"_markerType": "CircleMarker"のファイルの読み込みに非対応。読み込んだ際、"_markerType": "Circle"として処理している。~~ 2016年3月14日、地理院地図（https://maps.gsi.go.jp/ ）は"_markerType": "CircleMarker"のファイルの読み込みに対応した。

## 参考文献
1. Leaflet リファレンス http://leafletjs.com/reference-0.7.7.html （特にIcon, DivIcon, Circle, CircleMarker 及び Path）
