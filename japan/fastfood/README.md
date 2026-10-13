# japan/fastfood — 日本のファストフード・カフェのチェーン店（OpenStreetMap）

配布物（このディレクトリ）: `fastfood.geopbf`（33,931 点・1.4 MB）・`fastfood.csv`（同じ店の全列・9.9 MB）・`brands.csv`（169 ブランドの件数・業態・表記ゆれ）・`stats.json`（件数）。
`fastfood.geopbf` は [GeoPBF](https://github.com/kenjiyoshidahome2026-bit/geopbf)（precision 5 ≈ 1 m・gzip）。読み方: `https://kenjiyoshidahome2026-bit.github.io/ortho-data/japan/fastfood/fastfood.geopbf`。
スクリプトと SQLite はプロジェクトの共有フォルダ `fastfood/` にある（仕組みは [konbini](../konbini/README.md) と同じで、チェーン判定は `scripts/brands.py`）。

## 件数（`stats.json`・OSM 2026-10-07 版）

| 項目 | 値 |
| --- | --- |
| OSM の飲食店（amenity=fast_food / cafe / restaurant / ice_cream） | 165,470 |
| うち **チェーン店**（このディレクトリの中身） | **33,931**・169 ブランド（ファストフード 15,941 ／ レストラン扱いのチェーン 12,695 ／ カフェ 4,911 ／ アイスクリーム 384） |
| 判定の根拠 | brand:wikidata 26,765 ／ name の先頭一致 5,980 ／ brand の文字列 1,186 |
| 都道府県・市区町村 | 100% |
| 営業時間 ／ 24 時間 ／ 住所 | 7,488 ／ 1,250 ／ 5,958 |

| ブランド | 件数 | 主な業態 | Wikidata |
| --- | --- | --- | --- |
| マクドナルド | 2,508 | ファストフード | Q38076 |
| すき家 | 1,478 | ファストフード | Q6137375 |
| スターバックス | 1,456 | カフェ | Q37158 |
| ガスト | 1,061 | レストラン | Q87724117 |
| ほっともっと | 1,032 | ファストフード | Q10850949 |
| モスバーガー | 992 | ファストフード | Q1204169 |
| 吉野家 | 984 | ファストフード | Q776272 |
| 松屋 | 973 | ファストフード | Q848773 |
| CoCo壱番屋 | 847 | レストラン | Q5986105 |
| サイゼリヤ | 836 | レストラン | Q886564 |
| ドトールコーヒーショップ | 834 | カフェ | Q11322732 |
| ケンタッキーフライドチキン | 821 | ファストフード | Q524757 |
| コメダ珈琲店 | 737 | カフェ | Q11302679 |
| ミスタードーナツ | 561 | ファストフード | Q1065819 |
| 餃子の王将 | 560 | レストラン | Q11666805 |
| 丸亀製麺 | 547 | ファストフード | Q10877253 |
| タリーズコーヒー | 537 | カフェ | Q3541983 |
| スシロー | 511 | ファストフード | Q11257037 |
| ドミノ・ピザ | 481 | ファストフード | Q839466 |
| はま寿司 | 460 | ファストフード | Q17220385 |
| くら寿司 | 457 | ファストフード | Q6445491 |
| ココス | 437 | レストラン | Q11301951 |
| ジョイフル | 416 | レストラン | Q11310517 |
| サーティワンアイスクリーム | 388 | アイスクリーム | Q584601 |
| 牛角 | 362 | レストラン | Q11349387 |
| なか卯 | 358 | ファストフード | Q11274132 |
| ほっかほっか亭 | 355 | ファストフード | Q5878035 |
| かつや | 349 | ファストフード | Q2855257 |
| デニーズ | 318 | レストラン | Q11320661 |
| バーミヤン | 291 | レストラン | Q11328598 |

公式の店舗数の概数に対して、マクドナルド 84%・松屋 97%・ガスト 85%・サイゼリヤ 80%・スターバックス 77%・すき家 75%・ケンタッキー 68%・ほっともっと 43%。

## チェーンの判定

- `brand:wikidata` が付いた店が 5 店以上ある QID をチェーンとみなす（データから表を作る）。正規名は `brand:ja` の最頻値。会社と店舗で項目が分かれているものは店数の多い方へ寄せる（`brands.csv` の merged_qids）。
- QID の無い店（約 2 割）は、チェーンの表記と手動の別名（KFC・マック・スタバ・やきとり大吉・山田うどん・松のや…）で name の先頭を照合。「カフェ」「ラーメン」などの一般語は別名にしない。QID の無いチェーン（やきとり大吉・山田うどん・かごの屋・銀のさら…）は brand_qid が空。
- 業態（category）は OSM の amenity のまま（スシローは fast_food、CoCo壱番屋は restaurant のように付け方が揺れる）。絞り込みは brand で。

## 属性

| ファイル | 中身 |
| --- | --- |
| `fastfood.geopbf` | 点。id, name（正規ブランド名＋支店名）, branch, brand, brand_qid, category（ファストフード／カフェ／レストラン／アイスクリーム）, cuisine, opening_hours, open_24h, drive_through, pref, pref_code, muni, muni_code, ward, address, osm_timestamp |
| `fastfood.csv` | 上の列に加えて osm_type, osm_id, amenity, brand_source, brand_raw, brand_wikidata_raw, operator, takeaway, delivery, phone, website, postcode, ward_code, wheelchair, level, check_date, osm_version, region（BOM 付き UTF-8） |
| `brands.csv` | brand, brand_qid, count, category, 判定源ごとの件数, merged_qids, 原文の表記ゆれ |

## 出典・利用条件

© [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors, **Open Database License (ODbL) 1.0**（OSM の派生データベースとして ODbL を引き継ぐ）。ブランドの QID は Wikidata（CC0）。ブランドのロゴは含まない。
