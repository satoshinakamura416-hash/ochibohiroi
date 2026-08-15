# 一花屋より

なかむらさとし（花屋の店主）の雑感集。

https://nakamurasatoshi.com

小さな花屋を続けながら、考えていること。その日の商いを終えたあとに、書き留めています。

※ リポジトリ名 `ochibohiroi` は開設当初のサイト名の名残。Cloudflare の連携先になっているため変更していない。

## 中身

`index.html` の一枚だけで動くサイト。全記事がこのファイルに入っている。
外部のライブラリもフォントも読み込まないので、このファイル単体をブラウザで開けばそのまま読める。

| ファイル | 中身 |
|---|---|
| `public/index.html` | サイト本体（一覧・全記事・スタイル・記事切替） |
| `wrangler.jsonc` | Cloudflare Workers の設定。`public/` をそのまま配信する |

## 公開の仕組み

Cloudflare Workers（静的アセット配信）。`main` に push すると自動でデプロイされる。
ビルドは無し。`public/` の中身がそのまま公開される。

## 記事を足すとき

`public/index.html` の2箇所に追記する。

1. 一覧に `<button class="entry" data-open="eNNN">` を足す（新しいものが上）
2. 本文に `<article class="article" id="eNNN" hidden>` を足す

記事の種別は2つ。

- **雑感** — 走り書きそのまま（`kind--raw`）
- **覚え書き** — 考えを整理したもの（`kind--note`）
