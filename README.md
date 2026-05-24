# 鉄道ノード中心性ビューワ

MapLibre GL JS と PMTiles を使って、[国土数値情報の鉄道ノード](https://nlftp.mlit.go.jp/ksj/gml/datalist/KsjTmplt-N02-2025.html)の中心性を可視化する Web ビューアです。
複数の中心性指標（次元中心性・媒介中心性・近接中心性・固有ベクトル中心性・ページランク）を切り替え、上位ノードを地図上で確認できます。

## ファイル構成

- `index.html`: ビューア UI と地図スタイル定義
- `rail_edge.pmtiles`: 鉄道エッジのベクタータイル z4-14
- `rail_node.pmtiles`: 鉄道ノードのベクタータイル z4-14

## 操作方法

- プルダウン `centrality-select`
- `ALL`: すべての鉄道ノードを表示
- その他の指標: 選択した中心性指標で `rank <= 20` のノードのみ表示

## 可視化の考え方

- 本ビューアの主題は「鉄道ノード中心性の比較」です。
- 指標ごとに上位ノードだけを地図上に表示し、駅・接続点の重要度の違いを直感的に確認できます。

## URL ハッシュパラメータ

地図の表示状態とプルダウン選択は、URL ハッシュに保存されます。

例:

- `#map=10/35.681/139.767`
- `#map=10/35.681/139.767&metric=pagerank`

`metric` に指定できる値:

- `degree_centrality`
- `betweenness_centrality`
- `closeness_centrality`
- `eigenvector_centrality`
- `pagerank`

`metric` が未指定または不正な場合は `ALL` が使われます。
