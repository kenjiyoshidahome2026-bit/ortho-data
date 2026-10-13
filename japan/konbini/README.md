# japan/konbini — 日本のコンビニ（OpenStreetMap）

配布物（このディレクトリ）: `konbini.geopbf`（48,940 点・1.7 MB）・`konbini.csv`（同じ店の全列・12.7 MB）・`brands.csv`（ブランド別の件数と表記ゆれ）・`stats.json`（件数）・`osm-coverage.md`（日本の OSM の種別ごとのカバー率の俯瞰）。
`konbini.geopbf` は [GeoPBF](https://github.com/kenjiyoshidahome2026-bit/geopbf)（precision 5 ≈ 1 m・gzip）。読み方: `https://kenjiyoshidahome2026-bit.github.io/ortho-data/japan/konbini/konbini.geopbf`。
取得・正規化のスクリプトと SQLite（差分更新つき）はプロジェクトの共有フォルダ `konbini/` にある（`scripts/` の 01 PBF 取得 → 02 抽出 → 03 組み立て → 05 geopbf）。

## 件数（`stats.json`・OSM 2026-10-07 版）

| 項目 | 値 |
| --- | --- |
| 店（`shop=convenience`） | **48,940**（node 33,437 ／ 建物などの面 15,503＝代表点） |
| 都道府県・市区町村 | 48,940 ／ 48,940（100%、OSM の行政界で包含判定） |
| ブランドが決まった | 46,899（95%）。根拠は brand:wikidata 38,724・brand の文字列 2,367・name の文字列 5,783 |
| 営業時間 ／ 24 時間 ／ 住所 | 15,287 ／ 13,880 ／ 9,608 |
| 都道府県別 上位 | 東京都 6,840、大阪府 3,682、神奈川県 3,405、埼玉県 2,725、愛知県 2,668、千葉県 2,446 |

| ブランド | 件数 | Wikidata |
| --- | --- | --- |
| セブン-イレブン | 17,635 | Q259340 |
| ファミリーマート | 12,888 | Q1191685 |
| ローソン | 10,798 | Q1557223 |
| （ブランド不明） | 2,020 |  |
| ミニストップ | 1,592 | Q1038929 |
| セイコーマート | 936 | Q11314123 |
| デイリーヤマザキ | 877 | Q5209392 |
| ローソンストア100 | 523 | Q11350960 |
| ヤマザキショップ | 393 | Q11345131 |
| NewDays | 266 | Q11234763 |
| サークルK | 210 | Q3268010 |
| ローソン・スリーエフ | 180 | Q24866804 |
| ポプラ | 112 | Q7229380 |
| サンクス | 79 | Q11305522 |
| ナチュラルローソン | 75 | Q11323850 |
| セーブオン | 60 | Q11314868 |

公式の店舗数（各社公表の概数）に対して大手 3 社は 8 割前後（セブン-イレブン 84%・ファミリーマート 81%・ローソン 74%）。都市部で高く地方で薄い。

## 属性

| ファイル | 中身 |
| --- | --- |
| `konbini.geopbf` | 点。id（`n`/`w`/`r` ＋ OSM の id）, name（正規ブランド名＋支店名）, branch, brand, brand_qid, opening_hours, open_24h（24/7 なら 1）, pref, pref_code, muni, muni_code（全国地方公共団体コード 5 桁）, ward（政令市の区）, address, osm_timestamp |
| `konbini.csv` | 上の列に加えて osm_type, osm_id, geom_source, brand_source（判定の根拠）, brand_raw / brand_wikidata_raw（OSM の原文）, operator, phone, website, postcode, ward_code, atm, toilets, wheelchair, parking, level, check_date, osm_version, region（BOM 付き UTF-8） |
| `brands.csv` | brand_qid, brand, count, 判定源ごとの件数, 原文の表記ゆれ |

ブランドの正規化: `brand:wikidata` を最優先し、同じブランドで項目が分かれているもの（ファミリーマート Q11247682→Q1191685 など）を寄せる。無い店は brand → name → operator の文字列を別名表（セブンイレブン／7-ELEVEN／セブン‐イレブン…）で判定。日本語のみ（多言語名は持たない）。

## 出典・利用条件

© [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors, **Open Database License (ODbL) 1.0**。このディレクトリのデータは OSM の派生データベースなので ODbL を引き継ぐ（帰属表示と、改変したデータベースを配る時の同一条件）。元データは download.openstreetmap.fr の日本の地域抽出。ブランドの QID は Wikidata（CC0）。
ブランドのロゴは含まない（表示はブランドの色と頭文字で描く想定）。
