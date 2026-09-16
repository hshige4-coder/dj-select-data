# dj-select-data

DJ SELECTの週次データを管理するためのリポジトリです。

## 目的

SHIGEDX本体のコードと曲データを分離し、毎週のDJ SELECT更新をこのリポジトリのJSON更新だけで完了できるようにします。

最終目標は、ChatGPTに「DJ SELECT更新して」と依頼すると、最新曲を選定・確認し、このリポジトリの本番JSONを更新できる状態です。

## データ構成

- `weekly-charts.example.json` : 正式なJSONフォーマットのテンプレート
- `weekly-charts.json` : 本番用データ（現在のSHIGEDXデータを移行後に作成）

### DJ SELECT

- `djSelect20` : 総合20曲
- `genres.dance` : DANCE 10曲
- `genres.hiphop` : HIP HOP 10曲
- `genres.rnb` : R&B 10曲
- `genres.house` : HOUSE 10曲
- `genres.reggae` : REGGAE / DANCEHALL 10曲
- `genres.pop` : POP 10曲

各曲の基本項目:

- `rank`
- `title`
- `artist`
- `comment`
- `status` (`NEW` / `急上昇` / `SELECT`)
- `appleMusicUrl`
- `jacketFrom`
- `jacketTo`

## 安全な移行手順

1. 現在SHIGEDXで使用しているDJ SELECTの曲データを取得する
2. `weekly-charts.example.json` の形式に変換する
3. Apple Music JP Catalogで曲名・アーティスト・URLを検証する
4. 実データ入りの `weekly-charts.json` を作成する
5. SHIGEDX側をGitHub上の `weekly-charts.json` を読むように変更する
6. 表示確認後、以後は本体を再デプロイせずJSONだけを更新する

本番データを移行する前に、空の `weekly-charts.json` をSHIGEDXから参照しないこと。
