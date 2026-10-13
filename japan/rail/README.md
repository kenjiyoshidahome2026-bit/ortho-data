# japan/rail — 日本の鉄道: 国土数値情報（N02）の路線・駅 × Wikipedia の台帳

配布物（このディレクトリ）: `lines.geopbf`（運営者 × 路線 597 本・1.0 MB）・`stations.geopbf`（駅レコード 10,234 点・0.45 MB）・`station-groups.geopbf`（乗換で一体の駅 9,046 点・0.36 MB）・`stats.json`（件数）、同じ中身の表 `stations.csv`・`lines.csv`・`station-groups.csv`・`operators.csv`・`unmatched.csv`（結べなかった駅）。
いずれも [GeoPBF](https://github.com/kenjiyoshidahome2026-bit/geopbf)（precision 5 ≈ 1 m・gzip）。読み方: `https://kenjiyoshidahome2026-bit.github.io/ortho-data/japan/rail/lines.geopbf`。
台帳を組むスクリプトと Wikidata の生データはプロジェクトの共有フォルダ `rail/` にある（`scripts/` の 01 取得 → 02 結び → 03 表 → 04 geopbf）。

## 件数（`stats.json`）

| 項目 | 値 |
| --- | --- |
| 駅レコード（`stations.csv`＝N02 の駅 × 路線） | **10,234** |
| 　Wikidata の項目に結べた | **10,231（99.97%）**、未結び 3（大山ケーブルの 3 駅＝Wikidata に項目が無い、`unmatched.csv`） |
| 　日本語版 Wikipedia の記事あり | **10,221**（うち 223 は運営者別の項目に記事が無く、同名・近接の項目から記事を借りた＝`article_qid`） |
| 　英語版の記事あり | 9,832 |
| 　記事なし 10 | ケーブルカーの駅（御岳山・滝本・高尾山・清滝・府中・傘松・宮脇・筑波山頂・山麓・山上）＝Wikidata に項目はあるが記事が無い |
| 　Wikidata で廃止になっている | 5（留萌線 4 駅 2026-04-01、西黒崎 2026-07-31＝N02-25 は 2025 年度の姿） |
| 　位置が 2 km 以上ずれる | 4（Wikidata 側の座標の誤り: 立花 20 km、坂田/田村 は同じ座標、阿仁合 2.2 km） |
| 駅グループ（`station-groups.csv`＝N02_005g・乗換で一体の駅） | 9,046、記事あり 9,033、記事が複数に割れる 14（新橋・新宿・品川など運営者で記事が分かれる駅） |
| 路線（`lines.csv`＝運営者 × 路線名） | 597（うち 1 本は N02 の区間に運営者と路線名が入れ替わった誤記 `えちぜん鉄道/三国芦原線`） |
| 　Wikidata の項目に結べた | **596/596** |
| 　日本語版の記事あり | 578（残り 18 は区間ごとの項目＝札幌市電の 4 線・富山軌道線の 4 線・とさでん 3 線・岡電 2 線・豊橋鉄道東田本線・京福嵐山本線・万葉線高岡軌道線・広島新交通1号線・御岳登山鉄道。上位の路線の記事を `article_qid` で借りた物あり） |
| 運営者（`operators.csv`） | 176、結べた 175（未: 一般財団法人青函トンネル記念館） |

## 結び方（`scripts/02-match.mjs`）

1. **駅** = 駅名（NFKC・「駅/停留場/電停/仮乗降場」と括弧を外した形）が同じ Wikidata 項目を候補にし、N02 の駅線分の中点からの距離（8 km 以内、近いほど高得点）・所属路線 P81 が路線の QID と合う（+5）・運営者 P137 が合う（+2）・廃止 P576（−3）・記事あり（+1）・別名での一致（−1）の点数で選ぶ。
2. **路線** = 1 回目の駅の結びで出た P81 の多数決（名前も合う物を優先、駅の 30% 以上か 3 駅以上）。決まらない物は名前（号線・括弧・「本」を外した形）× 運営者で引く。
3. 路線の QID が決まったら、駅をもう一度結ぶ（同名の駅が近くに複数ある時の決め手＝黄檗駅 (京阪)/(JR西日本)、弘明寺、三宮…）。
4. **手動層** `scripts/manual.json`: 駅コード → QID（立花＝Wikidata の座標が 20 km ずれる、東山・おかでんミュージアム、ガイドウェイバス守山、BRT 化した豊前桝田/筑前岩屋）、路線 → QID（御岳登山鉄道、大山鋼索線）。

路線名のゆれは駅の多数決で吸収する（N02「東海道線」→ 東海道本線、「11号線半蔵門線」→ 東京メトロ半蔵門線、「常磐新線」→ つくばエクスプレス、「東京臨海新交通臨海線」→ ゆりかもめ）。票が 50% を切るのは 2 本だけ（函館市電湯の川線＝区間項目、宮津線＝京都丹後鉄道の運行系統名が P81 に多い）。

## 属性

| ファイル | 地物 | 属性 |
| --- | --- | --- |
| `lines.geopbf` | 運営者 × 路線名ごとに N02 の区間を束ねた MultiLineString（597） | operator, operator_qid, line, class1（鉄道区分）, class2（事業者種別）, qid, wiki_ja, wiki_en, article_qid（記事を借りた上位路線）, length_km（区間の実長）, length_km_wd（Wikidata P2043）, stations（N02 の駅数）, opened, closed |
| `stations.geopbf` | 駅レコード（駅 × 路線・10,234 点＝N02 の駅線分の中点） | code（N02_005c）, group（N02_005g）, name, operator, operator_qid, line, line_qid, class1, class2, qid, wiki_ja, wiki_en, article_qid（記事を借りた元の項目）, opened, closed |
| `station-groups.geopbf` | 乗換で一体の駅（N02_005g）ごとに 1 点・記事 1 本（9,046 点） | group, name, records（レコード数）, operators, lines（「、」区切り）, qid, wiki_ja, wiki_en |

## 出典・利用条件

- 国土数値情報 鉄道データ（N02-25・2025 年度）国土交通省 — 国土数値情報ダウンロードサイトのコンテンツ利用規約（政府標準利用規約 2.0 準拠・出典の明記）。「国土数値情報（鉄道データ）（国土交通省）を加工して作成」。
- Wikidata（CC0）／Wikipedia の記事名（CC BY-SA 4.0）。`www.wikidata.org/w/api.php` は共有 IP で 429 になるため、すべて `query.wikidata.org`（SPARQL）で取っている。

## 気づいた点

- N02-25 の区間 1 本（えちぜん鉄道 三国芦原線）で N02_003 と N02_004 が入れ替わっている。駅側は正しい。
- Wikidata には運営者別の駅項目（JR 東京駅・東京メトロ東京駅…）が増えており、記事はまとめて 1 本。`qid` は運営者別の項目、`article_qid`/`wiki_ja` は記事側、と分けて持っている。
- 大山ケーブルカー（大山ケーブル・大山寺・阿夫利神社）は Wikipedia に記事があるが Wikidata に項目が無い（手で作ると結べる）。
