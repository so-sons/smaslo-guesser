# スマスロゲッサー

スマートパチスロ（スマスロ）の機種を、タイプ・メーカー・導入年・通常純増・最高純増・コイン単価・コイン持ちのヒントから当てる推理ゲーム（ポケゲッサー風）。
ルームコードで友達とオンライン対戦できます。カギ付きリンクを知っている人だけが遊べます。

- 非公式ファンゲームです。機種データは [パチスロサミットONLINE](https://www.pachislot-summit.com/model/) のスマスロ機種一覧と [フリック7](https://flick7.net/ranking/coin-unit/) のメーカー公表値（コイン単価・コイン持ち・純増）を元にしています。
- 対戦モードの通信は PeerJS（WebRTC）。サーバー不要。
- エンジンは [inaguesser](https://github.com/so-sons/inaguesser) と共通。

## ファイル構成
| ファイル | 役割 |
|---|---|
| `config.js` | 題材ごとの設定（タイトル・ヒント項目・フィルター） |
| `data.src.js` | 機種データ（平文・コミットしない） |
| `build-data.js` | `data.src.js` を暗号化して `data.bin` を生成 |
| `index.html` / `style.css` / `app.js` / `loader.js` | 共通エンジン |
| `docs/新しい題材で作る.md` | 別の作品で作るときの手順書 |

## データ形式（`data.src.js`）
```js
{ n: "スマスロ北斗の拳", k: "ほくとのけん", a: "",           // 名前・かな・通称（検索用）
  i: "https://…/image.png",                                  // 画像URL
  mk: "サミー", ty: "AT", yi: 1, d: "2023.4.3",              // メーカー / タイプ / 導入年（lists.years の index） / 導入日
  j1: "2.7枚/G", j1n: 2.7, j2: "5.0枚/G", j2n: 5.0,          // 通常純増 / 最高純増（表示用文字列と数値）
  cu: "3.4円", cun: 3.4, cm: "31.0G", cmn: 31.0 }             // コイン単価 / コイン持ち
```
純増が「2.7 or 5.0枚/G」のように複数ある機種は最小値を通常純増、最大値を最高純増にしています。

## 更新のしかた
```bash
node build-data.js   # data.src.js を変えたとき
git add -A && git commit -m "..." && git push   # 約1分で GitHub Pages に反映
```
