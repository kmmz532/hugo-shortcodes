# hugo-shortcodes

Hugo サイトで記事の書式を利用するための Hugo Modules の部品です。ショートコード、Markdown の描画フック、OGP 索引（`/ogp/index.json`）を含みます。

- 管理画面の部品（`hugo-gh-admin`）とは独立しています。
- 見た目は本体のテーマが決めます。この部品はクラス名と構造だけを定めます。

## 含むもの

- ショートコード: `link-card`・`youtube`・`vimeo`・`niconico`・`tweet`・`instagram`・`facebook`・`soundcloud`
- 描画フック: `render-image`（画像の幅の指定）・`render-passthrough`（数式のビルド時描画）
- `partials/link-meta.html`: URL の OGP（タイトル・概要・画像）を取得する
- `ogp/single.json` と `content/ogp.md`: 記事中の `link-card` の OGP を `/ogp/index.json` に出す

## 取り込み方

本体の `hugo.toml` に入れます。

```toml
[[module.imports]]
  path = "github.com/kmmz532/hugo-shortcodes"
```

```sh
hugo mod get github.com/kmmz532/hugo-shortcodes@v0.1.0
```

版はタグで固定します。`hugo mod get -u` で更新する前に、差分を確認します。

## 本体（テーマ）との契約

- 画像の URL が `/` で始まるときは、サイトの `baseURL` のパス（サブパス）を付けて出力します（`/images/a.png` は、`/blog/` に置いたサイトでは `/blog/images/a.png` になる）。
- `link-card` は次のクラス名を出力します: `link-card`・`link-card-body`・`link-card-title`・`link-card-desc`・`link-card-host`・`link-card-thumb`。テーマはこれらのクラスに見た目を当てます。
- 埋め込みは次のクラス名で囲みます: `video-embed`・`twitter-tweet`・`instagram-embed`・`facebook-embed`・`audio-embed`。
- 記事の書式が解釈できないときは `shortcode-error` を出します。
- `link-meta.html` は `site.Params.appleIcon` を OGP 画像の既定値に使います。
- 編集画面のプレビューは `/ogp/index.json` を読みます。URL と形を変えるときは版を上げます。

## 見た目を変える

本体に同じ名前のファイルを置くと、この部品のファイルを上書きできます（例: `layouts/shortcodes/youtube.html`）。

## 版の約束

- 版は [Semantic Versioning](https://semver.org/lang/ja/) に従い、タグで示します。
- ショートコードの名前と引数、出力するクラス名、`/ogp/index.json` の形を変えるときは、メジャー版を上げ、`CHANGELOG.md` に書きます。
- 契約に触れない修正は、マイナー版かパッチ版にします。

## ライセンス

MIT（[LICENSE](LICENSE)）。
