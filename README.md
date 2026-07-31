# 海面高度シミュレーター

海面高度を自由に変更しながら、地球儀上でどこが陸地・海になるかを確認できるWebアプリです。標高データには [Terrarium](https://github.com/tilezen/joerd/blob/master/docs/formats.md#terrarium) (Mapzen / AWS Open Data) を使用しています。

## 使い方

`index.html` をブラウザで開くだけで動作します(ビルドやインストールは不要です)。GitHub Pages などの静的ホスティングにそのまま配置しても利用できます。

ローカルで確認する場合は、簡易サーバーを立てて開いてください。

```sh
python3 -m http.server 8000
# http://localhost:8000/index.html を開く
```

## 機能

- スライダー / プリセットボタン(全て陸地・現在・全て海) / ステッパーボタン(±1m・±10m・±100m)で海面高度を変更
- 現在の標高と設定した海面高度を比較して、陸地・海を色分け表示
- 素早い連続操作(スライダーのドラッグやステッパーの連打)時は、途中経過の描画を間引き、目的の高度まで飛ぶように表示することでパフォーマンスを確保
- 「3Dで見る」ボタンで視点を傾け、実際の標高に基づいた立体的な地形(山や谷の凹凸)を表示

## 技術構成

- [MapLibre GL JS](https://maplibre.org/maplibre-gl-js/docs/) による地球儀投影 (globe projection) 表示
- Terrarium形式の標高タイルをカスタムプロトコル(`elev://`)で読み込み、指定した海面高度に応じて陸地・海の色とヒルシェードをその場で計算
- 同じ標高タイルを `raster-dem` ソースとしても利用し、`map.setTerrain()` で3D地形を有効化

## データ出典

標高データ: Terrarium (Mapzen / AWS Open Data)
