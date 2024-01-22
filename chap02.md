---
link:
  - rel: 'stylesheet'
    href: 'css/main.css'
lang: 'ja'
---

# 第1章 CSS表示テストの結果

## はじめに

### CSS表示テストの目的

最新のEPUB仕様である[EPUB 3.3](https://www.w3.org/TR/epub-33/)では、「EPUB 3は、[CSS Snapshot](https://www.w3.org/TR/CSS/) で定義されたCSSをサポートする」と明記されている（[§1.3.3 Relationship to CSS](https://www.w3.org/TR/epub-33/#sec-overview-relations-css)）。いくつかの -epub- 接頭辞付きのCSSプロパティは後方互換性のために残されてはいるが、「EPUB制作者は接頭辞なしのプロパティを使用するべきで、リーディングシステムは現行のCSS仕様をサポートするべき」、「Working Groupは、EPUBの次のメジャーバージョンでこれらの接頭辞付きプロパティをサポートする見込みがないため、現在これらの接頭辞付きプロパティを使用しているEPUBクリエーターは、サポートが可能になり次第、接頭辞なしバージョンに移行することを推奨する」とのことである（[$6.3.1.3 Prefixed properties](https://www.w3.org/TR/epub-33/#sec-css-prefixed)）。

それでは各社のEPUBリーディングシステムが現行のCSS仕様をどれだけサポートしているのか、-epub- 接頭辞付きプロパティはもう使わなくてよいのか、気になるところである。そこで、[CSS Snapshot 2023](https://www.w3.org/TR/css-2023/) でCSSの公式的な定義とされているCSSモジュールを中心にチェックリストを作成した。

### CSSの公式的な定義に含まれるCSSモジュール

「2023年現在の CSS （ Cascading Style Sheets ）は、 以下に挙げる仕様で定義される」（[CSS Snapshot 2023 - §2.1. Cascading Style Sheets (CSS) — The Official Definition](https://www.w3.org/TR/css-2023/#css-official)）

- [CSS Level 2, latest revision](https://www.w3.org/TR/CSS2/) (including errata)
- [CSS Syntax Level 3](https://www.w3.org/TR/css-syntax-3/)
- [CSS Style Attributes](https://www.w3.org/TR/css-style-attr/)
- [Media Queries Level 3](https://www.w3.org/TR/css3-mediaqueries/)
- [CSS Conditional Rules Level 3](https://www.w3.org/TR/css-conditional-3/)
  - [ ] @supports ルール
- [Selectors Level 3](https://www.w3.org/TR/selectors-3/)
  - [ ] 部分文字列マッチング属性セレクタ `[att^=val]`, `[att$=val]`, `[att*=val]`
  - [ ] :root 擬似クラス
  - [ ] :nth-child(), :nth-last-child(), :nth-of-type(), :nth-last-of-type() 擬似クラス
  - [ ] :last-child, :only-child, :first-of-type, :last-of-type, :only-of-type 擬似クラス
  - [ ] :empty 擬似クラス
  - [ ] :not() 擬似クラス
  - [ ] ::first-line, ::first-letter, ::before, ::after 擬似要素
  - [ ] 後続兄弟結合子 `E ~ F`
- [CSS Namespaces](https://www.w3.org/TR/css-namespaces/)
- [CSS Cascading and Inheritance Level 4](https://www.w3.org/TR/css-cascade-4/)
  - [ ] all プロパティ
  - [ ] プロパティの値 initial, unset, revert
- [CSS Values and Units Level 3](https://www.w3.org/TR/css-values-3/)
  - 長さの単位
    - [ ] ch
    - [ ] rem
    - [ ] vw, vh, vmin, vmax
    - [ ] Q
- [CSS Custom Properties for Cascading Variables Module Level 1](https://www.w3.org/TR/css-variables-1/)
  - [ ] CSS変数
- [CSS Box Model Level 3](https://www.w3.org/TR/css-box-3/)
- [CSS Color Level 4](https://www.w3.org/TR/css-color-4/)
  - [ ] opacity プロパティ
  - [ ] rgb() 関数のコンマなし形式　例: rgb(0 255 0 / .5)
  - [ ] 16進数のRGBA形式（8桁、4桁）　例: #88FF44CC, #8F4C
  - [ ] hsl() 関数
  - [ ] hwb() 関数
- [CSS Backgrounds and Borders Level 3](https://www.w3.org/TR/css-backgrounds-3/)
  - [ ] 複数の背景画像　例: background-image: url(a.png), url(b.png), url(c.png);
  - [ ] border-radius プロパティ
  - [ ] border-image プロパティ
  - [ ] box-shadow プロパティ
- [CSS Images Level 3](https://www.w3.org/TR/css-images-3/)
  - グラデーション関数
    - [ ] linear-gradient()
    - [ ] radial-gradient()
    - [ ] repeating-linear-gradient(), repeating-radial-gradient()
  - [ ] object-fit プロパティ
  - [ ] object-position プロパティ
- [CSS Fonts Level 3](https://www.w3.org/TR/css-fonts-3/)
  - [ ] @font-face ルール
  - [ ] unicode-range 記述子
  - [ ] font-kerning プロパティ
  - [ ] font-variant プロパティ
  - [ ] font-feature-settings プロパティ
- [CSS Writing Modes Level 3](https://www.w3.org/TR/css-writing-modes-3/)
  - [ ] writing-mode プロパティ
  - [ ] text-orientation プロパティ
  - [ ] text-combine-upright プロパティ
- [CSS Multi-column Layout Level 1](https://www.w3.org/TR/css-multicol-1/)
  - [ ] columns プロパティ
  - [ ] column-gap プロパティ
  - [ ] column-rule プロパティ
  - [ ] column-span プロパティ
  - [ ] column-fill プロパティ
- [CSS Flexible Box Module Level 1](https://www.w3.org/TR/css-flexbox-1/)
  - [ ] display プロパティの値 flex および inline-flex
  - [ ] flex-flow プロパティ
  - [ ] order プロパティ
  - [ ] flex プロパティ
  - [ ] justify-content, align-items, align-self, align-content プロパティ
- [CSS User Interface Module Level 3](https://www.w3.org/TR/css-ui-3/)
  - [ ] box-sizing プロパティ
  - [ ] outline プロパティ
- [CSS Containment Module Level 1](https://www.w3.org/TR/css-contain-1/)
  - [ ] contain プロパティ
- [CSS Transforms Level 1](https://www.w3.org/TR/css-transforms-1/)
  - [ ] transform プロパティ
- [CSS Compositing and Blending Level 1](https://www.w3.org/TR/compositing-1/)
  - [ ] mix-blend-mode プロパティ
  - [ ] isolation プロパティ
  - [ ] background-blend-mode プロパティ
- [CSS Easing Functions Level 1](https://www.w3.org/TR/css-easing-1/)
- [CSS Counter Styles Level 3](https://www.w3.org/TR/css-counter-styles-3/)
  - [ ] @counter-style ルール
  - 定義済みカウンタースタイル
    - [ ] cjk-decimal
    - [ ] hiragana, hiragana-iroha, katakana, katakana-iroha
    - [ ] cjk-earthly-branch
    - [ ] cjk-heavenly-stem
    - [ ] japanese-informal

### かなり安定しているが実装経験が限定的なCSSモジュール

「以下のモジュールは設計作業が完了し、かなり安定しているが、まだテストと実装の経験があまりない」（[§2.2. Fairly Stable Modules with limited implementation experience](https://www.w3.org/TR/css-2023/#fairly-stable)）

- [Media Queries Level 4](https://www.w3.org/TR/mediaqueries-4/)
- [CSS Display Module Level 3](https://www.w3.org/TR/css-display-3/)
- [CSS Writing Modes Level 4](https://www.w3.org/TR/css-writing-modes-4/)
- [CSS Fragmentation Module Level 3](https://www.w3.org/TR/css-break-3/)
  - [ ] break-before, break-after プロパティ
  - [ ] break-inside プロパティ
  - [ ] orphans, widows プロパティ
  - [ ] box-decoration-break プロパティ
- [CSS Box Alignment Module Level 3](https://www.w3.org/TR/css-align-3/)
- [CSS Shapes Module Level 1](https://www.w3.org/TR/css-shapes-1/)
- [CSS Text Module Level 3](https://www.w3.org/TR/css-text-3/)
  - [ ] word-break プロパティ
  - [ ] line-break プロパティ
  - [ ] hyphens プロパティ
  - [ ] overflow-wrap プロパティ
  - [ ] text-align-last プロパティ
  - [ ] hanging-punctuation プロパティ
- [CSS Text Decoration Level 3](https://www.w3.org/TR/css-text-decor-3/)
  - [ ] text-decoration-line, text-decoration-style, text-decoration-color プロパティ
  - [ ] text-underline-position プロパティ
  - [ ] text-emphasis-color, text-emphasis-style, text-emphasis プロパティ
  - [ ] text-emphasis-position プロパティ
- [CSS Masking Level 1](https://www.w3.org/TR/css-masking-1/)
- [CSS Scroll Snap Module Level 1](https://www.w3.org/TR/css-scroll-snap-1/)
- [CSS Speech Module Level 1](https://www.w3.org/TR/css-speech-1/)
- [CSS Scrollbars Styling Module Level 1](https://www.w3.org/TR/css-scrollbars-1/)
- [CSS View Transitions Module Level 1](https://www.w3.org/TR/css-view-transitions-1/)

### 大まかな相互運用性のあるCSSモジュール

「以下のモジュールは、大まかな相互運用性を確保した上で広く展開されているが、その詳細は十分に練られておらず、また十分な仕様もないため、さらなるテストとバグ修正が必要」 （[	§2.3. Modules with Rough Interoperability](https://www.w3.org/TR/css-2023/#rough-interop)）

- [CSS Transitions Level 1](https://www.w3.org/TR/css-transitions-1/)
- [CSS Animations Level 1](https://www.w3.org/TR/css-animations-1/)
- [CSS Grid Layout Module Level 1](https://www.w3.org/TR/css-grid-1/)
  - [ ] display プロパティの値 grid および inline-grid
  - [ ] grid-template, grid プロパティ
  - [ ] grid-row, grid-column, grid-area プロパティ
- [CSS Grid Layout Module Level 2](https://www.w3.org/TR/css-grid-2/)
- [CSS Will Change Level 1](https://www.w3.org/TR/css-will-change-1/)
- [Filter Effects Module Level 1](https://www.w3.org/TR/filter-effects-1/)
- [CSS Font Loading Module Level 3](https://www.w3.org/TR/css-font-loading/)
- [CSS Box Sizing Level 3](https://www.w3.org/TR/css-sizing-3/)
  - [ ] width・height プロパティの値 min-content と max-content
- [CSS Transforms Level 2](https://www.w3.org/TR/css-transforms-2/)
- [CSS Lists and Counters Module Level 3](https://www.w3.org/TR/css-lists-3/)
- [CSS Logical Properties and Values Level 1](https://www.w3.org/TR/css-logical-1/)
  - 論理プロパティ
    - [ ] block-size, inline-size, min-block-size, min-inline-size, max-block-size, max-inline-size
    - [ ] margin-block-start, margin-block-end, margin-inline-start, margin-inline-end
    - [ ] margin-block, margin-inline
    - [ ] inset-block-start, inset-block-end, inset-inline-start, inset-inline-end
    - [ ] inset-block, inset-inline, inset
    - [ ] padding-block-start, padding-block-end, padding-inline-start, padding-inline-end
    - [ ] padding-block, padding-inline
    - [ ] border-block-start-width, border-block-end-width, border-inline-start-width, border-inline-end-width
    - [ ] border-block-width, border-inline-width
    - [ ] border-block-start-style, border-block-end-style, border-inline-start-style, border-inline-end-style
    - [ ] border-block-style, border-inline-style
    - [ ] border-block-start-color, border-block-end-color, border-inline-start-color, border-inline-end-color
    - [ ] border-block-color, border-inline-color
    - [ ] border-block-start, border-block-end, border-inline-start, border-inline-end
    - [ ] border-block, border-inline
    - [ ] border-start-start-radius, border-start-end-radius, border-end-start-radius, border-end-end-radius
- [CSS Positioned Layout Module Level 3](https://www.w3.org/TR/css-position-3/)
- [Resize Observer](https://www.w3.org/TR/resize-observer-1/)
- [Web Animations](https://www.w3.org/TR/web-animations-1/)
- [CSS Fonts Module Level 4](https://www.w3.org/TR/css-fonts-4/)
- [CSS Color Adjustment Module Level 1](https://www.w3.org/TR/css-color-adjust-1/)
- [CSS Conditional Rules Module Level 4](https://www.w3.org/TR/css-conditional-4/)
  - [ ] @supports selector() ルール
- [CSS Cascading and Inheritance Level 5](https://www.w3.org/TR/css-cascade-5/)
  - [ ] @layer ルール

### CSS Snapshot 2023 に載っていないが、最新のブラウザで利用できるもの

- [Selectors Level 4](https://www.w3.org/TR/selectors-4/)
  - [ ] :is() 擬似クラス
  - [ ] :where() 擬似クラス
  - [ ] :has() 擬似クラス


## CSS表示テストの結果


### はじめに


### すべてのEPUBリーダーでサポートされているもの



### ほとんどのEPUBリーダーでサポートされているもの



### メジャーなEPUBリーダーでサポートされているもの



### モダンブラウザ系でのみサポートされているもの

