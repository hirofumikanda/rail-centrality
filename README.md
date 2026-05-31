# 鉄道ノード中心性ビューワ

[国土数値情報の鉄道データ](https://nlftp.mlit.go.jp/ksj/gml/datalist/KsjTmplt-N02-2025.html)を使って、日本の鉄道ノードの中心性を可視化する Web ビューアです。

鉄道区間の接続点と駅区間の端点をマージしてノード化し、さらに同じ駅名のノードを距離で縮約したうえで NetworkX による地域別の中心性を解析しています。コミュニティ検出には Louvain を使い、地域内で局所化した中心性として扱っています。

複数の中心性指標（地域内の次元中心性・媒介中心性・近接中心性・固有ベクトル中心性・ページランク）を切り替え、上位ノードを地図上で確認できます。

## ファイル構成

- `index.html`: ビューア UI と地図スタイル定義
- `rail_edge.pmtiles`: 地域別に集約した鉄道エッジのベクタータイル
- `rail_node.pmtiles`: 地域別に集約した鉄道ノードのベクタータイル

## 操作方法

- プルダウン `centrality-select`
- `ALL`: すべての鉄道ノードを表示
- その他の指標: 選択した地域内中心性で `rank <= 3` かつ `community_size >= 100` のノードのみ表示

## 可視化の考え方

- 本ビューアの主題は「地域別に縮約した駅ノード中心性の比較」です。
- 指標ごとに地域内上位ノードだけを地図上に表示し、駅グループごとの重要度の違いを直感的に確認できます。

## URL ハッシュパラメータ

地図の表示状態とプルダウン選択は、URL ハッシュに保存されます。

例:

- `#map=10/35.681/139.767`
- `#map=10/35.681/139.767&metric=pagerank_in_community`

`metric` に指定できる値:

- `degree_centrality_in_community`
- `betweenness_centrality_in_community`
- `closeness_centrality_in_community`
- `eigenvector_centrality_in_community`
- `pagerank_in_community`

`metric` が未指定または不正な場合は `ALL` が使われます。
