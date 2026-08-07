# PR表記スニペット（素のHTML版）

Astro化が終わるまでの間、手書きの `index.html` や記事HTMLに直接貼れる版です。
`PrNotice.astro` と見た目・文言を揃えてあります。

---

## 1. 記事冒頭に貼るHTML

`<h1>` のすぐ下、本文の最初の段落より **上** に置きます。

```html
<aside class="pr-notice" aria-label="広告表記">
  <svg class="pr-notice__paw" viewBox="0 0 24 24" aria-hidden="true">
    <ellipse cx="7"  cy="8"   rx="2.1" ry="2.8" />
    <ellipse cx="12" cy="6.4" rx="2.1" ry="3" />
    <ellipse cx="17" cy="8"   rx="2.1" ry="2.8" />
    <path d="M12 11.2c3.1 0 5.4 2.3 5.4 4.9 0 2.1-1.7 3.3-3.6 3.3-.8 0-1.3-.3-1.8-.3s-1 .3-1.8.3c-1.9 0-3.6-1.2-3.6-3.3 0-2.6 2.3-4.9 5.4-4.9z" />
  </svg>
  <p>
    この記事はアフィリエイト広告（PR）を含みます。商品リンク経由でご購入があった場合、
    当サイトに収益が発生することがあります。
  </p>
</aside>
```

## 2. フッターに貼るHTML

全ページ共通。`<footer>` の中、コピーライト表記の上あたりに。

```html
<section class="pr-policy" aria-labelledby="pr-policy-heading">
  <h2 id="pr-policy-heading">広告掲載について</h2>
  <p>
    bonbon222では、記事内でご紹介している商品・サービスの一部にアフィリエイト広告
    （バリューコマース、Amazonアソシエイト等）を利用しています。リンク経由でご購入・お申し込みが
    あった場合、当サイトに広告収益が発生することがあります。
  </p>
  <p>
    収益の有無が商品の評価や掲載順に影響することはありません。価格・仕様は執筆時点のもので、
    最新の情報は各販売ページをご確認ください。
  </p>
</section>
```

## 3. CSS（`<style>` 内か共通CSSの末尾に追記）

```css
/* --- PR表記：記事冒頭用 --- */
.pr-notice {
  display: flex;
  align-items: flex-start;
  gap: 0.7em;
  margin: 0 0 2rem;
  padding: 0.85em 1.1em;
  background: var(--color-sand, #ece5d8);
  border-left: 3px solid var(--color-sage, #8a9a7b);
  border-radius: 0 8px 8px 0;
  font-family: "Zen Maru Gothic", system-ui, sans-serif;
}

.pr-notice__paw {
  flex: 0 0 auto;
  width: 1.15em;
  height: 1.15em;
  margin-top: 0.15em;
  fill: var(--color-sage, #8a9a7b);
  opacity: 0.85;
}

.pr-notice p {
  margin: 0;
  /* 「一般消費者が認識できる」大きさを確保。これ以上小さくしないこと */
  font-size: 0.875rem;
  line-height: 1.75;
  color: var(--color-text, #4a453e);
}

/* --- PR表記：フッター用 --- */
.pr-policy {
  margin: 3rem 0 0;
  padding: 1.5rem 0 0;
  border-top: 1px solid var(--color-sand, #ece5d8);
  font-family: "Zen Maru Gothic", system-ui, sans-serif;
}

.pr-policy h2 {
  margin: 0 0 0.75rem;
  font-size: 0.95rem;
  font-weight: 500;
  letter-spacing: 0.04em;
  color: var(--color-sage-dark, #6d7d5e);
}

.pr-policy p {
  margin: 0 0 0.75rem;
  font-size: 0.875rem;
  line-height: 1.9;
  color: var(--color-text-muted, #6b655c);
}

.pr-policy p:last-child { margin-bottom: 0; }

@media (max-width: 480px) {
  .pr-notice { padding: 0.8em 0.9em; }
}
```

---

## 貼る位置のルール

```
┌─────────────────────────┐
│  ヘッダー / ロゴ           │
├─────────────────────────┤
│  H1  自動猫トイレおすすめ… │
│  ┌───────────────────┐  │
│  │ 🐾 この記事はアフィリ… │  │ ← ここ。スクロール前に見える位置
│  └───────────────────┘  │
│  本文スタート…            │
└─────────────────────────┘
```

- **スクロールしないと見えない位置はNG**（記事末尾だけ、は危険）
- 折りたたみ・アコーディオンの中に隠すのもNG
- 文字サイズ `0.875rem`（14px相当）が下限。これ以上小さくしない
- 背景と文字のコントラストを下げない

## やりがちなNG表記

| NG | 理由 |
|---|---|
| `#ad` `#sponsored` だけ | 日本語話者が広告と判別しづらい |
| 「アフィリエイトリンクを使用しています」だけを最下部に | 位置が不適切 |
| 「一部プロモーションを含む場合があります」 | 「場合があります」でぼかすと弱い |
| 画像内に文字で埋め込む | テキストとして認識されない |

推奨は「**広告**」「**PR**」「**アフィリエイト広告**」を日本語で明示すること。

## Amazonアソシエイト提携後にやること

承認されたら、フッターに次の一文を**そのまま**追加（改変不可の指定文言）:

> Amazonのアソシエイトとして、bonbon222は適格販売により収入を得ています。

`PrNotice.astro` の footer variant 内にコメントアウトで仕込み済みです。
