---
link:
  - rel: 'stylesheet'
    href: 'css/main.css'
lang: 'ja'
---

# 第2章 CSS表示テスト

## 2-1 はじめに

### 2-1-1 CSS表示テストの目的と方法

最新のEPUB仕様である[EPUB 3.3](https://www.w3.org/TR/epub-33/)では、「EPUB 3は、[CSS Snapshot](https://www.w3.org/TR/CSS/) で定義されたCSSをサポートする」と明記されている（[§1.3.3 Relationship to CSS](https://www.w3.org/TR/epub-33/#sec-overview-relations-css)）。いくつかの `-epub-`接頭辞付きのCSSプロパティは後方互換性のために残されてはいるが、「EPUB制作者は接頭辞なしのプロパティを使用するべきで、リーディングシステム（EPUBリーダー）は現行のCSS仕様をサポートするべき」、「Working Groupは、EPUBの次のメジャーバージョンでこれらの接頭辞付きプロパティをサポートする見込みがないため、現在これらの接頭辞付きプロパティを使用しているEPUB制作者は、サポートが可能になり次第、接頭辞なしバージョンに移行することを推奨する」とのことである（[$6.3.1.3 Prefixed properties](https://www.w3.org/TR/epub-33/#sec-css-prefixed)）。

となると各社のEPUBリーダーが現行のCSS仕様を、どれだけサポートしているのか、本当に`-epub-`接頭辞付きプロパティは使わなくてもよいのかという疑問が湧いてくる。そこで、W3Cによる[CSS Snapshot 2023](https://www.w3.org/TR/css-2023/) でCSSの公式的な定義とされたCSSモジュールを中心にチェックすべきCSSモジュールのリストを作成した上で、実際に各社EPUBリーダーがどれだけ準拠しているのかテストしてみた。

テストの方法をもう少し詳しく説明しよう。まずチェックするCSSモジュールは、以下の基準によって選定した（選定結果は2-1-2参照）。

1. CSSの公式的な定義に含まれるCSSモジュール
2. かなり安定しているが実装経験が限定的なCSSモジュール
3. 大まかな相互運用性のあるCSSモジュール
4. CSS Snapshot 2023 に載っていないが、最新のブラウザで利用できるもの

つぎに、選定したCSSモジュールごとに、対応の可否を一目で識別できるテスト用EPUBファイルを制作した。これは以下のリポジトリで公開しているので、お読みの方はぜひ自分でも試していただきたい（なお、ライセンスは[CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/deed.ja)で、著作権を放棄している）。

- [EPUBリーダーのCSS仕様適合性テスト](https://github.com/jagat-xpub/epub-css-test/tree/main)

最後に、これらのテストベッドとなるEPUBリーダーを選定し、当研究会のメンバーごとに割り振ってテストを開始（テストしたEPUBリーダーは2-1-3参照）した。各担当者は前述テスト用EPUBファイルを自分が担当するEPUBリーダーにサイドロードし、テスト結果を以下のGoogleスプレッドシートに記録していったのである。

- [EPUBリーダー表示チェック（JAGAT次世代パブリッシング研究会）2023](https://docs.google.com/spreadsheets/d/1xKDlL4TrMHMa1qq2QsWcXLEGMPjx-JWcTdaw_8KkftE/edit?usp=sharing)

こうして得られたテスト結果をなるべく分かりやすく報告するのが、本章のミッションである。

### 2-1-2 選定したCSSモジュール

#### CSSの公式的な定義に含まれるCSSモジュール

「2023年現在の CSS （ Cascading Style Sheets ）は、 以下に挙げる仕様で定義される」（[CSS Snapshot 2023 - §2.1. Cascading Style Sheets (CSS) — The Official Definition](https://www.w3.org/TR/css-2023/#css-official)）

- [CSS Level 2, latest revision](https://www.w3.org/TR/CSS2/) (including errata)
- [CSS Syntax Level 3](https://www.w3.org/TR/css-syntax-3/)
- [CSS Style Attributes](https://www.w3.org/TR/css-style-attr/)
- [Media Queries Level 3](https://www.w3.org/TR/css3-mediaqueries/)
- [CSS Conditional Rules Level 3](https://www.w3.org/TR/css-conditional-3/)
  - @supports ルール
- [Selectors Level 3](https://www.w3.org/TR/selectors-3/)
  - 部分文字列マッチング属性セレクタ `[att^=val]`, `[att$=val]`, `[att*=val]`
  - :root 擬似クラス
  - :nth-child(), :nth-last-child(), :nth-of-type(), :nth-last-of-type() 擬似クラス
  - :last-child, :only-child, :first-of-type, :last-of-type, :only-of-type 擬似クラス
  - :empty 擬似クラス
  - :not() 擬似クラス
  - ::first-line, ::first-letter, ::before, ::after 擬似要素
  - 後続兄弟結合子 `E ~ F`
- [CSS Namespaces](https://www.w3.org/TR/css-namespaces/)
- [CSS Cascading and Inheritance Level 4](https://www.w3.org/TR/css-cascade-4/)
  - all プロパティ
  - プロパティの値 initial, unset, revert
- [CSS Values and Units Level 3](https://www.w3.org/TR/css-values-3/)
  - 長さの単位
    - ch
    - rem
    - vw, vh, vmin, vmax
    - Q
- [CSS Custom Properties for Cascading Variables Module Level 1](https://www.w3.org/TR/css-variables-1/)
  - CSS変数
- [CSS Box Model Level 3](https://www.w3.org/TR/css-box-3/)
- [CSS Color Level 4](https://www.w3.org/TR/css-color-4/)
  - opacity プロパティ
  - rgb() 関数のコンマなし形式　例: rgb(0 255 0 / .5)
  - 16進数のRGBA形式（8桁、4桁）　例: #88FF44CC, #8F4C
  - hsl() 関数
  - hwb() 関数
- [CSS Backgrounds and Borders Level 3](https://www.w3.org/TR/css-backgrounds-3/)
  - 複数の背景画像　例: background-image: url(a.png), url(b.png), url(c.png);
  - border-radius プロパティ
  - border-image プロパティ
  - box-shadow プロパティ
- [CSS Images Level 3](https://www.w3.org/TR/css-images-3/)
  - グラデーション関数
    - linear-gradient()
    - radial-gradient()
    - repeating-linear-gradient(), repeating-radial-gradient()
  - object-fit プロパティ
  - object-position プロパティ
- [CSS Fonts Level 3](https://www.w3.org/TR/css-fonts-3/)
  - @font-face ルール
  - unicode-range 記述子
  - font-kerning プロパティ
  - font-variant プロパティ
  - font-feature-settings プロパティ
- [CSS Writing Modes Level 3](https://www.w3.org/TR/css-writing-modes-3/)
  - writing-mode プロパティ
  - text-orientation プロパティ
  - text-combine-upright プロパティ
- [CSS Multi-column Layout Level 1](https://www.w3.org/TR/css-multicol-1/)
  - columns プロパティ
  - column-gap プロパティ
  - column-rule プロパティ
  - column-span プロパティ
  - column-fill プロパティ
- [CSS Flexible Box Module Level 1](https://www.w3.org/TR/css-flexbox-1/)
  - display プロパティの値 flex および inline-flex
  - flex-flow プロパティ
  - order プロパティ
  - flex プロパティ
  - justify-content, align-items, align-self, align-content プロパティ
- [CSS User Interface Module Level 3](https://www.w3.org/TR/css-ui-3/)
  - box-sizing プロパティ
  - outline プロパティ
- [CSS Containment Module Level 1](https://www.w3.org/TR/css-contain-1/)
  - contain プロパティ
- [CSS Transforms Level 1](https://www.w3.org/TR/css-transforms-1/)
  - transform プロパティ
- [CSS Compositing and Blending Level 1](https://www.w3.org/TR/compositing-1/)
  - mix-blend-mode プロパティ
  - isolation プロパティ
  - background-blend-mode プロパティ
- [CSS Easing Functions Level 1](https://www.w3.org/TR/css-easing-1/)
- [CSS Counter Styles Level 3](https://www.w3.org/TR/css-counter-styles-3/)
  - @counter-style ルール
  - 定義済みカウンタースタイル
    - cjk-decimal
    - hiragana, hiragana-iroha, katakana, katakana-iroha
    - cjk-earthly-branch
    - cjk-heavenly-stem
    - japanese-informal

#### かなり安定しているが実装経験が限定的なCSSモジュール

「以下のモジュールは設計作業が完了し、かなり安定しているが、まだテストと実装の経験があまりない」（[§2.2. Fairly Stable Modules with limited implementation experience](https://www.w3.org/TR/css-2023/#fairly-stable)）

- [Media Queries Level 4](https://www.w3.org/TR/mediaqueries-4/)
- [CSS Display Module Level 3](https://www.w3.org/TR/css-display-3/)
- [CSS Writing Modes Level 4](https://www.w3.org/TR/css-writing-modes-4/)
- [CSS Fragmentation Module Level 3](https://www.w3.org/TR/css-break-3/)
  - break-before, break-after プロパティ
  - break-inside プロパティ
  - orphans, widows プロパティ
  - box-decoration-break プロパティ
- [CSS Box Alignment Module Level 3](https://www.w3.org/TR/css-align-3/)
- [CSS Shapes Module Level 1](https://www.w3.org/TR/css-shapes-1/)
- [CSS Text Module Level 3](https://www.w3.org/TR/css-text-3/)
  - word-break プロパティ
  - line-break プロパティ
  - hyphens プロパティ
  - overflow-wrap プロパティ
  - text-align-last プロパティ
  - hanging-punctuation プロパティ
- [CSS Text Decoration Level 3](https://www.w3.org/TR/css-text-decor-3/)
  - text-decoration-line, text-decoration-style, text-decoration-color プロパティ
  - text-underline-position プロパティ
  - text-emphasis-color, text-emphasis-style, text-emphasis プロパティ
  - text-emphasis-position プロパティ
- [CSS Masking Level 1](https://www.w3.org/TR/css-masking-1/)
- [CSS Scroll Snap Module Level 1](https://www.w3.org/TR/css-scroll-snap-1/)
- [CSS Speech Module Level 1](https://www.w3.org/TR/css-speech-1/)
- [CSS Scrollbars Styling Module Level 1](https://www.w3.org/TR/css-scrollbars-1/)
- [CSS View Transitions Module Level 1](https://www.w3.org/TR/css-view-transitions-1/)

#### 大まかな相互運用性のあるCSSモジュール

「以下のモジュールは、大まかな相互運用性を確保した上で広く展開されているが、その詳細は十分に練られておらず、また十分な仕様もないため、さらなるテストとバグ修正が必要」 （[	§2.3. Modules with Rough Interoperability](https://www.w3.org/TR/css-2023/#rough-interop)）

- [CSS Transitions Level 1](https://www.w3.org/TR/css-transitions-1/)
- [CSS Animations Level 1](https://www.w3.org/TR/css-animations-1/)
- [CSS Grid Layout Module Level 1](https://www.w3.org/TR/css-grid-1/)
  - display プロパティの値 grid および inline-grid
  - grid-template, grid プロパティ
  - grid-row, grid-column, grid-area プロパティ
- [CSS Grid Layout Module Level 2](https://www.w3.org/TR/css-grid-2/)
- [CSS Will Change Level 1](https://www.w3.org/TR/css-will-change-1/)
- [Filter Effects Module Level 1](https://www.w3.org/TR/filter-effects-1/)
- [CSS Font Loading Module Level 3](https://www.w3.org/TR/css-font-loading/)
- [CSS Box Sizing Level 3](https://www.w3.org/TR/css-sizing-3/)
  - width・height プロパティの値 min-content と max-content
- [CSS Transforms Level 2](https://www.w3.org/TR/css-transforms-2/)
- [CSS Lists and Counters Module Level 3](https://www.w3.org/TR/css-lists-3/)
- [CSS Logical Properties and Values Level 1](https://www.w3.org/TR/css-logical-1/)
  - 論理プロパティ
    - block-size, inline-size, min-block-size, min-inline-size, max-block-size, max-inline-size
    - margin-block-start, margin-block-end, margin-inline-start, margin-inline-end
    - margin-block, margin-inline
    - inset-block-start, inset-block-end, inset-inline-start, inset-inline-end
    - inset-block, inset-inline, inset
    - padding-block-start, padding-block-end, padding-inline-start, padding-inline-end
    - padding-block, padding-inline
    - border-block-start-width, border-block-end-width, border-inline-start-width, border-inline-end-width
    - border-block-width, border-inline-width
    - border-block-start-style, border-block-end-style, border-inline-start-style, border-inline-end-style
    - border-block-style, border-inline-style
    - border-block-start-color, border-block-end-color, border-inline-start-color, border-inline-end-color
    - border-block-color, border-inline-color
    - border-block-start, border-block-end, border-inline-start, border-inline-end
    - border-block, border-inline
    - border-start-start-radius, border-start-end-radius, border-end-start-radius, border-end-end-radius
- [CSS Positioned Layout Module Level 3](https://www.w3.org/TR/css-position-3/)
- [Resize Observer](https://www.w3.org/TR/resize-observer-1/)
- [Web Animations](https://www.w3.org/TR/web-animations-1/)
- [CSS Fonts Module Level 4](https://www.w3.org/TR/css-fonts-4/)
- [CSS Color Adjustment Module Level 1](https://www.w3.org/TR/css-color-adjust-1/)
- [CSS Conditional Rules Module Level 4](https://www.w3.org/TR/css-conditional-4/)
  - @supports selector() ルール
- [CSS Cascading and Inheritance Level 5](https://www.w3.org/TR/css-cascade-5/)
  - @layer ルール

#### CSS Snapshot 2023 に載っていないが、最新のブラウザで利用できるもの

- [Selectors Level 4](https://www.w3.org/TR/selectors-4/)
  - :is() 擬似クラス
  - :where() 擬似クラス
  - :has() 擬似クラス

### 2-1-3 本調査におけるテスト環境の一覧

#### 掲載したテスト環境の一覧

<table>
  <tr>
    <th style="color:#434343" align="center">リーダー</th>
    <th style="color:#434343" align="center">種別</th>
    <th style="color:#434343" align="center">機材名</th>
    <th style="color:#434343" align="center">OS ver.</th>
    <th style="color:#434343" align="center">リーダーver.</th>
    <th style="color:#434343" align="center">担当者</th>
    <th style="color:#434343" align="center">テスト日</th>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle *ⁱ</td>
    <td bgcolor="#c9daf8" align="center">Kindle Previewer3 (Mac)</td>
    <td bgcolor="#c9daf8" align="center">Mac mini M1, 2020</td>
    <td bgcolor="#c9daf8" align="center">macOS Sonoma 14.2.1</td>
    <td bgcolor="#c9daf8" align="center">3.74.0</td>
    <td bgcolor="#c9daf8" align="center">村上</td>
    <td bgcolor="#c9daf8" align="center">2023/12/28</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle *ⁱ</td>
    <td bgcolor="#c9daf8" align="center">Mac</td>
    <td bgcolor="#c9daf8" align="center">Mac mini M1, 2020</td>
    <td bgcolor="#c9daf8" align="center">macOS Sonoma 14.2.1</td>
    <td bgcolor="#c9daf8" align="center">7.0.0.100 (1.316222)</td>
    <td bgcolor="#c9daf8" align="center">村上</td>
    <td bgcolor="#c9daf8" align="center">2023/12/28</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle *ⁱ</td>
    <td bgcolor="#c9daf8" align="center">Kindle Previewer3 (Win)</td>
    <td bgcolor="#c9daf8" align="center"></td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Pro 22H2</td>
    <td bgcolor="#c9daf8" align="center">3.74.0</td>
    <td bgcolor="#c9daf8" align="center">村上</td>
    <td bgcolor="#c9daf8" align="center">2024/1/9</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle *ⁱ</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center"></td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Pro 22H2</td>
    <td bgcolor="#c9daf8" align="center">2.3.0 (70673)</td>
    <td bgcolor="#c9daf8" align="center">村上</td>
    <td bgcolor="#c9daf8" align="center">2024/1/9</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle *ⁱ</td>
    <td bgcolor="#c9daf8" align="center">Android</td>
    <td bgcolor="#c9daf8" align="center">OPPO A55s 5G</td>
    <td bgcolor="#c9daf8" align="center">Android 12</td>
    <td bgcolor="#c9daf8" align="center">8.89.3.0 (2.0.2766.0)</td>
    <td bgcolor="#c9daf8" align="center">村上</td>
    <td bgcolor="#c9daf8" align="center">2024/1/9</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle *ⁱ</td>
    <td bgcolor="#c9daf8" align="center">iPad</td>
    <td bgcolor="#c9daf8" align="center">iPad mini (第5世代)</td>
    <td bgcolor="#c9daf8" align="center">iPadOS 17.1.2</td>
    <td bgcolor="#c9daf8" align="center">7.0.1</td>
    <td bgcolor="#c9daf8" align="center">村上</td>
    <td bgcolor="#c9daf8" align="center">2024/1/9</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle *ⁱ</td>
    <td bgcolor="#c9daf8" align="center">iOS</td>
    <td bgcolor="#c9daf8" align="center">iPhone13mini</td>
    <td bgcolor="#c9daf8" align="center">iOS 17.2.1</td>
    <td bgcolor="#c9daf8" align="center">7.1</td>
    <td bgcolor="#c9daf8" align="center">古門</td>
    <td bgcolor="#c9daf8" align="center">2024/1/21</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">kobo</td>
    <td bgcolor="#d9ead3" align="center">iOS</td>
    <td bgcolor="#d9ead3" align="center">iPhone13mini</td>
    <td bgcolor="#d9ead3" align="center">iOS16.4.1 (a)</td>
    <td bgcolor="#d9ead3" align="center">10.3.7</td>
    <td bgcolor="#d9ead3" align="center">古門</td>
    <td bgcolor="#d9ead3" align="center">2023/5/20</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">kobo</td>
    <td bgcolor="#d9ead3" align="center">Android</td>
    <td bgcolor="#d9ead3" align="center">Galaxy Tab S8 Ultra</td>
    <td bgcolor="#d9ead3" align="center">Android　13</td>
    <td bgcolor="#d9ead3" align="center">9.4.8.1</td>
    <td bgcolor="#d9ead3" align="center">仁科</td>
    <td bgcolor="#d9ead3" align="center">2023/8/20</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">kobo</td>
    <td bgcolor="#c9daf8" align="center">専用タブレット</td>
    <td bgcolor="#c9daf8" align="center">Kobo Libra 2</td>
    <td bgcolor="#c9daf8" align="center"></td>
    <td bgcolor="#c9daf8" align="center">4.37.21586 (42535ad976, 2023/07/06)</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/07/25</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">kobo</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">N/A *⁲</td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Pro (22H2　19045.3208)</td>
    <td bgcolor="#c9daf8" align="center">4.37.19051</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/07/25</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">kobo</td>
    <td bgcolor="#c9daf8" align="center">Mac</td>
    <td bgcolor="#c9daf8" align="center">MacBook (Retina, 12-12inch, Early 2016)</td>
    <td bgcolor="#c9daf8" align="center">macOS Monterey 12.6.6</td>
    <td bgcolor="#c9daf8" align="center">4.37.17113</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/08/20</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">kobo *ⁱ</td>
    <td bgcolor="#c9daf8" align="center">Mac</td>
    <td bgcolor="#fff2cc" align="center"></td>
    <td bgcolor="#fff2cc" align="center"></td>
    <td bgcolor="#fff2cc" align="center"></td>
    <td bgcolor="#fff2cc" align="center"></td>
    <td bgcolor="#fff2cc" align="center"></td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">ブック</td>
    <td bgcolor="#d9ead3" align="center" valign="top">iOS</td>
    <td bgcolor="#d9ead3" align="center">iPhone13mini</td>
    <td bgcolor="#d9ead3" align="center">iOS16.4.1 (a)</td>
    <td bgcolor="#d9ead3" align="center">N/A *³</td>
    <td bgcolor="#d9ead3" align="center">古門</td>
    <td bgcolor="#d9ead3" align="center">2023/5/20</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">ブック</td>
    <td bgcolor="#d9ead3" align="center" valign="top">Mac</td>
    <td bgcolor="#d9ead3" align="center">MacBookAir M2 2022</td>
    <td bgcolor="#d9ead3" align="center">13.6.3 (22G436)</td>
    <td bgcolor="#d9ead3" align="center">5.2 (5800.52)</td>
    <td bgcolor="#d9ead3" align="center">小形</td>
    <td bgcolor="#d9ead3" align="center">2024/01/05</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">MURASAKI</td>
    <td bgcolor="#d9ead3" align="center">Mac</td>
    <td bgcolor="#d9ead3" align="center">MacBookAir M2 2022</td>
    <td bgcolor="#d9ead3" align="center">13.4</td>
    <td bgcolor="#d9ead3" align="center">2.4.1</td>
    <td bgcolor="#d9ead3" align="center">小形</td>
    <td bgcolor="#d9ead3" align="center">2023/05/23</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">honto</td>
    <td bgcolor="#c9daf8" align="center">iOS</td>
    <td bgcolor="#c9daf8" align="center">iPhone13mini</td>
    <td bgcolor="#c9daf8" align="center">iOS16.4.1 (a)</td>
    <td bgcolor="#c9daf8" align="center">6.60.0</td>
    <td bgcolor="#c9daf8" align="center">古門</td>
    <td bgcolor="#c9daf8" align="center">2023/5/20</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">honto</td>
    <td bgcolor="#c9daf8" align="center">Android</td>
    <td bgcolor="#c9daf8" align="center">Galaxy Tab S8 Ultra</td>
    <td bgcolor="#c9daf8" align="center">Android　13</td>
    <td bgcolor="#c9daf8" align="center">6.60.0</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/8/20</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">honto</td>
    <td bgcolor="#c9daf8" align="center">iOS</td>
    <td bgcolor="#c9daf8" align="center">iPhone13mini</td>
    <td bgcolor="#c9daf8" align="center">iOS16.4.1 (a)</td>
    <td bgcolor="#c9daf8" align="center">6.60.0</td>
    <td bgcolor="#c9daf8" align="center">古門</td>
    <td bgcolor="#c9daf8" align="center">2023/5/20</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">honto *ⁱ</td>
    <td bgcolor="#c9daf8" align="center">iOS</td>
    <td bgcolor="#c9daf8" align="center">iPhone13mini</td>
    <td bgcolor="#c9daf8" align="center">iOS17.2.1</td>
    <td bgcolor="#c9daf8" align="center">6.62.0</td>
    <td bgcolor="#c9daf8" align="center">古門</td>
    <td bgcolor="#c9daf8" align="center">2024/1/24</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">BOOK☆WALKER</td>
    <td bgcolor="#d9ead3" align="center">iOS</td>
    <td bgcolor="#d9ead3" align="center">iPhone13mini</td>
    <td bgcolor="#d9ead3" align="center">iOS16.4.1 (a)</td>
    <td bgcolor="#d9ead3" align="center">7.4.7</td>
    <td bgcolor="#d9ead3" align="center">古門</td>
    <td bgcolor="#d9ead3" align="center">2023/5/20</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">BOOK☆WALKER for Android</td>
    <td bgcolor="#d9ead3" align="center">Android</td>
    <td bgcolor="#d9ead3" align="center">Galaxy Tab S8 Ultra</td>
    <td bgcolor="#d9ead3" align="center">Android　13</td>
    <td bgcolor="#d9ead3" align="center">7.5.0</td>
    <td bgcolor="#d9ead3" align="center">仁科</td>
    <td bgcolor="#d9ead3" align="center">2023/8/21</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kinoppy *ⁱ</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">N/A *⁲</td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Pro 22H2</td>
    <td bgcolor="#c9daf8" align="center">3.2.19</td>
    <td bgcolor="#c9daf8" align="center">村上</td>
    <td bgcolor="#c9daf8" align="center">2023/12/7</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Voyager</td>
    <td bgcolor="#c9daf8" align="center">Android</td>
    <td bgcolor="#c9daf8" align="center">Galaxy Tab S8 Ultra</td>
    <td bgcolor="#c9daf8" align="center">Android 13</td>
    <td bgcolor="#c9daf8" align="center">N/A *³ / Chrome114.0.5735.196</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/7/23</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Voyager</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">N/A *⁲</td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Pro</td>
    <td bgcolor="#c9daf8" align="center">N/A *³ / Chrome114.0.5735.199 *⁴</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/7/23</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">BiB/i</td>
    <td bgcolor="#d9ead3" align="center">Windows</td>
    <td bgcolor="#d9ead3" align="center">N/A *⁲</td>
    <td bgcolor="#d9ead3" align="center">Windows 11 PRO</td>
    <td bgcolor="#d9ead3" align="center">1.2.0 / Chrome 113.0.5672.127 (64ビット) *⁴</td>
    <td bgcolor="#d9ead3" align="center">古門</td>
    <td bgcolor="#d9ead3" align="center">2023/05/28</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">BiB/i</td>
    <td bgcolor="#d9ead3" align="center">Windows</td>
    <td bgcolor="#d9ead3" align="center">N/A *⁲</td>
    <td bgcolor="#d9ead3" align="center">Windows 11 PRO</td>
    <td bgcolor="#d9ead3" align="center">1.2.0 / Edge 113.0.1774.57 (64ビット) *⁴</td>
    <td bgcolor="#d9ead3" align="center">古門</td>
    <td bgcolor="#d9ead3" align="center">2023/05/28</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">超縦書</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">N/A *⁲</td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Home 21H2</td>
    <td bgcolor="#c9daf8" align="center">2.3.1</td>
    <td bgcolor="#c9daf8" align="center">田嶋</td>
    <td bgcolor="#c9daf8" align="center">22023/5/23</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">Vivliostyle Viewer</td>
    <td bgcolor="#d9ead3" align="center">Mac</td>
    <td bgcolor="#d9ead3" align="center">Mac mini M1, 2020</td>
    <td bgcolor="#d9ead3" align="center">macOS 13.4</td>
    <td bgcolor="#d9ead3" align="center">2.25.0 / Chrome 113 *⁴</td>
    <td bgcolor="#d9ead3" align="center">村上</td>
    <td bgcolor="#d9ead3" align="center">2023/05/23</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">Thorium Reader</td>
    <td bgcolor="#d9ead3" align="center">Windows</td>
    <td bgcolor="#d9ead3" align="center">N/A *⁲</td>
    <td bgcolor="#d9ead3" align="center">Windows 11 PRO</td>
    <td bgcolor="#d9ead3" align="center">2.3.0</td>
    <td bgcolor="#d9ead3" align="center">古門</td>
    <td bgcolor="#d9ead3" align="center">2023/09/25</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">Thorium Reader</td>
    <td bgcolor="#d9ead3" align="center">Mac</td>
    <td bgcolor="#d9ead3" align="center"></td>
    <td bgcolor="#d9ead3" align="center">macOS12.6.7</td>
    <td bgcolor="#d9ead3" align="center">2.2.0</td>
    <td bgcolor="#d9ead3" align="center">田嶋</td>
    <td bgcolor="#d9ead3" align="center">2023/08/25</td>
  </tr>
</table>

## 2-2 CSS表示テストの結果


### すべてのEPUBリーダーでサポートされているもの



### ほとんどのEPUBリーダーでサポートされているもの



### メジャーなEPUBリーダーでサポートされているもの



### モダンブラウザ系でのみサポートされているもの

