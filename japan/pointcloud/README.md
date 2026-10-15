# 点群の見本（COPC）

## atami-08NF2392.copc.laz

- 出典：VIRTUAL SHIZUOKA（静岡県）熱海市 3 次元点群データ 2019 航空レーザ 図郭 08NF2392
- ページ：https://www.geospatial.jp/ckan/dataset/atami-3d
- 元ファイル：https://virtual-shizuoka.s3.ap-northeast-1.amazonaws.com/2019/LP/Ground/08/NF/23/08NF2392.zip
- 利用条件：CC BY 4.0（元データは CC BY 4.0 / ODbL のデュアルライセンス）
- 表示：「VIRTUAL SHIZUOKA（静岡県）, CC BY 4.0」を添えて使う。下の変換を加えている。

### 元の LAS

- LAS 1.2・点の形式 3（GPS 時刻＋RGB）・9,510,494 点・TerraScan 出力
- 分類：1（未分類）7,717,826／2（地面）1,792,668
- 範囲（平面直角 VIII 系）：X 52799.79〜53200.02・Y −99000.03〜−98699.97・Z 61.72〜238.1 m
- 座標系の記載なし（VLR 0 本）。CKAN の説明＝JGD2011 平面直角座標系 第 8 系

### 変換

PDAL 2.10.2（PROJ 9.9.0）で EPSG:6676 を与えて COPC 化：

```
pdal translate 08NF2392.las atami-08NF2392.copc.laz --writer writers.copc --readers.las.spatialreference="EPSG:6676"
```

- 結果：COPC（LAS 1.4・点の形式 7）・9,510,494 点・scale 0.01・77,290,637 B
- WKT（VLR 2112）＝EPSG 6676。PROJ 9.9 の EPSG 辞書では名前が「JGD2024 / Japan Plane Rectangular CS VIII」（基準 6668・パラメータは JGD2011 と同じ）
- sha256：e8e1cba8f44905a4b68b52628ed733ebc55f07a102aeb309ad0714a1a0e4e6c2

Range で読むので gzip せずに生のまま置く。
