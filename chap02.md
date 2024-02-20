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

### 2-1-3 本調査におけるテスト環境の一覧

#### 2-1-3-1 掲載したテスト環境の一覧

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
    <td bgcolor="#c9daf8" align="center">Kindle *¹</td>
    <td bgcolor="#c9daf8" align="center">Kindle Previewer3 (Mac)</td>
    <td bgcolor="#c9daf8" align="center">Mac mini M1, 2020</td>
    <td bgcolor="#c9daf8" align="center">macOS Sonoma 14.2.1</td>
    <td bgcolor="#c9daf8" align="center">3.74.0</td>
    <td bgcolor="#c9daf8" align="center">村上</td>
    <td bgcolor="#c9daf8" align="center">2023/12/28</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle *¹</td>
    <td bgcolor="#c9daf8" align="center">Mac</td>
    <td bgcolor="#c9daf8" align="center">Mac mini M1, 2020</td>
    <td bgcolor="#c9daf8" align="center">macOS Sonoma 14.2.1</td>
    <td bgcolor="#c9daf8" align="center">7.0.0.100 (1.316222)</td>
    <td bgcolor="#c9daf8" align="center">村上</td>
    <td bgcolor="#c9daf8" align="center">2023/12/28</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle *¹</td>
    <td bgcolor="#c9daf8" align="center">Kindle Previewer3 (Win)</td>
    <td bgcolor="#c9daf8" align="center"></td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Pro 22H2</td>
    <td bgcolor="#c9daf8" align="center">3.74.0</td>
    <td bgcolor="#c9daf8" align="center">村上</td>
    <td bgcolor="#c9daf8" align="center">2024/01/09</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle *¹</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center"></td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Pro 22H2</td>
    <td bgcolor="#c9daf8" align="center">2.3.0 (70673)</td>
    <td bgcolor="#c9daf8" align="center">村上</td>
    <td bgcolor="#c9daf8" align="center">2024/01/09</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle *¹</td>
    <td bgcolor="#c9daf8" align="center">Android</td>
    <td bgcolor="#c9daf8" align="center">OPPO A55s 5G</td>
    <td bgcolor="#c9daf8" align="center">Android 12</td>
    <td bgcolor="#c9daf8" align="center">8.89.3.0 (2.0.2766.0)</td>
    <td bgcolor="#c9daf8" align="center">村上</td>
    <td bgcolor="#c9daf8" align="center">2024/01/09</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle *¹</td>
    <td bgcolor="#c9daf8" align="center">iPad</td>
    <td bgcolor="#c9daf8" align="center">iPad mini (第5世代)</td>
    <td bgcolor="#c9daf8" align="center">iPadOS 17.1.2</td>
    <td bgcolor="#c9daf8" align="center">7.0.1</td>
    <td bgcolor="#c9daf8" align="center">村上</td>
    <td bgcolor="#c9daf8" align="center">2024/01/09</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle *¹</td>
    <td bgcolor="#c9daf8" align="center">iOS</td>
    <td bgcolor="#c9daf8" align="center">iPhone13mini</td>
    <td bgcolor="#c9daf8" align="center">iOS 17.2.1</td>
    <td bgcolor="#c9daf8" align="center">7.1</td>
    <td bgcolor="#c9daf8" align="center">古門</td>
    <td bgcolor="#c9daf8" align="center">2024/01/21</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">kobo（kobo-1）*¹</td>
    <td bgcolor="#d9ead3" align="center">iOS</td>
    <td bgcolor="#d9ead3" align="center">iphone13mini</td>
    <td bgcolor="#d9ead3" align="center">iOS17.2.1</td>
    <td bgcolor="#d9ead3" align="center">10.4.3</td>
    <td bgcolor="#d9ead3" align="center">古門（追試）</td>
    <td bgcolor="#d9ead3" align="center">2024/02/01</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">kobo（kobo-2）</td>
    <td bgcolor="#d9ead3" align="center">Android</td>
    <td bgcolor="#d9ead3" align="center">Galaxy Tab S8 Ultra</td>
    <td bgcolor="#d9ead3" align="center">Android　13</td>
    <td bgcolor="#d9ead3" align="center">9.4.8.1</td>
    <td bgcolor="#d9ead3" align="center">仁科</td>
    <td bgcolor="#d9ead3" align="center">2023/08/20</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">kobo（kobo-3）</td>
    <td bgcolor="#c9daf8" align="center">専用タブレット</td>
    <td bgcolor="#c9daf8" align="center">Kobo Libra 2</td>
    <td bgcolor="#c9daf8" align="center"></td>
    <td bgcolor="#c9daf8" align="center">4.37.21586 (42535ad976, 2023/07/06)</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/07/25</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">kobo（kobo-3）</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">N/A *²</td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Pro (22H2　19045.3208)</td>
    <td bgcolor="#c9daf8" align="center">4.37.19051</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/07/25</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">kobo（kobo-3）</td>
    <td bgcolor="#c9daf8" align="center">Mac</td>
    <td bgcolor="#c9daf8" align="center">MacBook (Retina, 12-12inch, Early 2016)</td>
    <td bgcolor="#c9daf8" align="center">macOS Monterey 12.6.6</td>
    <td bgcolor="#c9daf8" align="center">4.37.17113</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/08/20</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">kobo（kobo-3）*¹</td>
    <td bgcolor="#c9daf8" align="center">Mac</td>
    <td bgcolor="#c9daf8" align="center">MacBook (Retina, 12-12inch, Early 2016)</td>
    <td bgcolor="#c9daf8" align="center">macOS Monterey 12.7.2</td>
    <td bgcolor="#c9daf8" align="center">楽天Koboデスクトップ 4.37.17113</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2024/01/30</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">ブック</td>
    <td bgcolor="#d9ead3" align="center" valign="top">iOS</td>
    <td bgcolor="#d9ead3" align="center">iPhone13mini</td>
    <td bgcolor="#d9ead3" align="center">iOS16.4.1 (a)</td>
    <td bgcolor="#d9ead3" style="color:#0000ff" align="center">N/A *³</td>
    <td bgcolor="#d9ead3" align="center">古門</td>
    <td bgcolor="#d9ead3" align="center">2023/05/20</td>
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
    <td bgcolor="#d9ead3" align="center">ブック</td>
    <td bgcolor="#d9ead3" align="center">Mac</td>
    <td bgcolor="#d9ead3" align="center">MacBook Pro 13-inch, 2019, Four Thunderbolt 3 ports</td>
    <td bgcolor="#d9ead3" align="center">13.6.3 (22G436)</td>
    <td bgcolor="#d9ead3" align="center">5.2</td>
    <td bgcolor="#d9ead3" align="center">小形</td>
    <td bgcolor="#d9ead3" align="center">2024/02/07</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">ブック*¹</td>
    <td bgcolor="#d9ead3" align="center">Mac</td>
    <td bgcolor="#d9ead3" align="center">MacBook Pro 13-inch, 2019, Four Thunderbolt 3 ports</td>
    <td bgcolor="#d9ead3" align="center">13.6.3 (22G436)</td>
    <td bgcolor="#d9ead3" align="center">5.2</td>
    <td bgcolor="#d9ead3" align="center">小形</td>
    <td bgcolor="#d9ead3" align="center">2024/02/08</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">ブック</td>
    <td bgcolor="#d9ead3" align="center">Mac</td>
    <td bgcolor="#d9ead3" align="center">MacBookAir M2 2022</td>
    <td bgcolor="#d9ead3" align="center">14.1.1（23B81）</td>
    <td bgcolor="#d9ead3" align="center">6.1</td>
    <td bgcolor="#d9ead3" align="center">小形</td>
    <td bgcolor="#d9ead3" align="center">2024/02/09</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">ブック*¹</td>
    <td bgcolor="#d9ead3" align="center">Mac</td>
    <td bgcolor="#d9ead3" align="center">MacBookAir M2 2023</td>
    <td bgcolor="#d9ead3" align="center">14.1.1（23B81）</td>
    <td bgcolor="#d9ead3" align="center">6.1</td>
    <td bgcolor="#d9ead3" align="center">小形</td>
    <td bgcolor="#d9ead3" align="center">2024/02/10</td>
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
    <td bgcolor="#d9ead3" align="center">MURASAKI</td>
    <td bgcolor="#d9ead3" align="center">Mac</td>
    <td bgcolor="#d9ead3" align="center">MacBookAir M2 2022</td>
    <td bgcolor="#d9ead3" align="center">14.1.1 (23B81)</td>
    <td bgcolor="#d9ead3" align="center">2.4.1</td>
    <td bgcolor="#d9ead3" align="center">小形</td>
    <td bgcolor="#d9ead3" align="center">2024/02/08</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">MURASAKI*¹</td>
    <td bgcolor="#d9ead3" align="center">Mac</td>
    <td bgcolor="#d9ead3" align="center">MacBook Pro 13-inch, 2019, Four Thunderbolt 3 ports</td>
    <td bgcolor="#d9ead3" align="center">13.6.3 (22G436)</td>
    <td bgcolor="#d9ead3" align="center">5.2</td>
    <td bgcolor="#d9ead3" align="center">小形</td>
    <td bgcolor="#d9ead3" align="center">2024/02/08</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">honto *¹</td>
    <td bgcolor="#c9daf8" align="center">iOS</td>
    <td bgcolor="#c9daf8" align="center">iPhone13mini</td>
    <td bgcolor="#c9daf8" align="center">iOS17.2.1</td>
    <td bgcolor="#c9daf8" align="center">6.62.0</td>
    <td bgcolor="#c9daf8" align="center">古門</td>
    <td bgcolor="#c9daf8" align="center">2024/01/24</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">BOOK☆WALKER</td>
    <td bgcolor="#d9ead3" align="center">iOS</td>
    <td bgcolor="#d9ead3" align="center">iPhone13mini</td>
    <td bgcolor="#d9ead3" align="center">iOS16.4.1 (a)</td>
    <td bgcolor="#d9ead3" align="center">7.4.7</td>
    <td bgcolor="#d9ead3" align="center">古門</td>
    <td bgcolor="#d9ead3" align="center">2023/05/20</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">BOOK☆WALKER for Android</td>
    <td bgcolor="#d9ead3" align="center">Android</td>
    <td bgcolor="#d9ead3" align="center">Galaxy Tab S8 Ultra</td>
    <td bgcolor="#d9ead3" align="center">Android　13</td>
    <td bgcolor="#d9ead3" align="center">7.5.0</td>
    <td bgcolor="#d9ead3" align="center">仁科</td>
    <td bgcolor="#d9ead3" align="center">2023/08/21</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kinoppy *¹</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">N/A *²</td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Pro 22H2</td>
    <td bgcolor="#c9daf8" align="center">3.2.19</td>
    <td bgcolor="#c9daf8" align="center">村上</td>
    <td bgcolor="#c9daf8" align="center">2023/12/07</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Voyager *¹</td>
    <td bgcolor="#c9daf8" align="center">Android</td>
    <td bgcolor="#c9daf8" align="center">Galaxy Tab S8 Ultra</td>
    <td bgcolor="#c9daf8" align="center">Android 13</td>
    <td bgcolor="#c9daf8" align="center">N/A *³ / Chrome114.0.5735.196</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/07/23</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Voyager *¹</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">N/A *²</td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Pro</td>
    <td bgcolor="#c9daf8" align="center">N/A *³ / Chrome114.0.5735.199 *⁴</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/07/23</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">BiB/i</td>
    <td bgcolor="#d9ead3" align="center">Windows</td>
    <td bgcolor="#d9ead3" align="center">N/A *²</td>
    <td bgcolor="#d9ead3" align="center">Windows 11 PRO</td>
    <td bgcolor="#d9ead3" align="center">1.2.0 / Chrome 113.0.5672.127 (64ビット) *⁴</td>
    <td bgcolor="#d9ead3" align="center">古門</td>
    <td bgcolor="#d9ead3" align="center">2023/05/28</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">BiB/i</td>
    <td bgcolor="#d9ead3" align="center">Windows</td>
    <td bgcolor="#d9ead3" align="center">N/A *²</td>
    <td bgcolor="#d9ead3" align="center">Windows 11 PRO</td>
    <td bgcolor="#d9ead3" align="center">1.2.0 / Edge 113.0.1774.57 (64ビット) *⁴</td>
    <td bgcolor="#d9ead3" align="center">古門</td>
    <td bgcolor="#d9ead3" align="center">2023/05/28</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">超縦書</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">N/A *²</td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Home 21H2</td>
    <td bgcolor="#c9daf8" align="center">2.3.1</td>
    <td bgcolor="#c9daf8" align="center">田嶋</td>
    <td bgcolor="#c9daf8" align="center">2023/05/23</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">超縦書 *¹</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">N/A *²</td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Pro 22H2</td>
    <td bgcolor="#c9daf8" align="center">2.3.2</td>
    <td bgcolor="#c9daf8" align="center">小形</td>
    <td bgcolor="#c9daf8" align="center">2024/02/13</td>
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
    <td bgcolor="#d9ead3" align="center">Vivliostyle Viewer *¹</td>
    <td bgcolor="#d9ead3" align="center">iOS</td>
    <td bgcolor="#d9ead3" align="center">iPad第6世代</td>
    <td bgcolor="#d9ead3" align="center">17.3.1</td>
    <td bgcolor="#d9ead3" align="center">2.27.0 / Safari</td>
    <td bgcolor="#d9ead3" align="center">田嶋</td>
    <td bgcolor="#d9ead3" align="center">2024/02/13</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">Thorium Reader</td>
    <td bgcolor="#d9ead3" align="center">Windows</td>
    <td bgcolor="#d9ead3" align="center">N/A *²</td>
    <td bgcolor="#d9ead3" align="center">Windows 11 PRO</td>
    <td bgcolor="#d9ead3" align="center">2.3.0</td>
    <td bgcolor="#d9ead3" align="center">古門</td>
    <td bgcolor="#d9ead3" align="center">2023/09/25</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">Thorium Reader</td>
    <td bgcolor="#d9ead3" align="center">Mac</td>
    <td bgcolor="#d9ead3" align="center">MacBook Air (M1, 2020) </td>
    <td bgcolor="#d9ead3" align="center">macOS12.6.7</td>
    <td bgcolor="#d9ead3" align="center">2.2.0</td>
    <td bgcolor="#d9ead3" align="center">田嶋</td>
    <td bgcolor="#d9ead3" align="center">2023/08/25</td>
  </tr>
</table>

#### 2-1-3-2 掲載しなかったテスト環境の一覧

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
    <td bgcolor="#c9daf8" align="center">Kindle</td>
    <td bgcolor="#c9daf8" align="center">Android</td>
    <td bgcolor="#c9daf8" align="center">Moto G30</td>
    <td bgcolor="#c9daf8" align="center">Android　11</td>
    <td bgcolor="#c9daf8" align="center">8.81.1.0 (1.3.290180.0)</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/05/22</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle</td>
    <td bgcolor="#c9daf8" align="center">Android</td>
    <td bgcolor="#c9daf8" align="center">Galaxy Tab S8 Ultra</td>
    <td bgcolor="#c9daf8" align="center">Android　13</td>
    <td bgcolor="#c9daf8" align="center">8.81.1.0 (1.3.290180.0)</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/722</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle</td>
    <td bgcolor="#c9daf8" align="center">Android</td>
    <td bgcolor="#c9daf8" align="center">Xperia 10 IV</td>
    <td bgcolor="#c9daf8" align="center">Android　13</td>
    <td bgcolor="#c9daf8" align="center">8.81.1.0 (1.3.290180.0)</td>
    <td bgcolor="#c9daf8" align="center">木龍</td>
    <td bgcolor="#c9daf8" align="center">2023/07/25</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle</td>
    <td bgcolor="#c9daf8" align="center">専用タブレット</td>
    <td bgcolor="#c9daf8" align="center">Fire HD 10 Plus (第11世代)</td>
    <td bgcolor="#c9daf8" align="center">FireOS 7.3.2.8</td>
    <td bgcolor="#c9daf8" align="center">14.81.160 (1.3.290180)</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/05/21</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle *¹</td>
    <td bgcolor="#c9daf8" align="center">専用タブレット</td>
    <td bgcolor="#c9daf8" align="center">Kindle Paperwhite Signature Edition (第11世代)</td>
    <td bgcolor="#c9daf8" align="center">専用タブレット</td>
    <td bgcolor="#fff2cc" align="center"> </td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/05/21</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">N/A *⁴</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Home 21H2</td>
    <td bgcolor="#c9daf8" align="center">田嶋</td>
    <td bgcolor="#c9daf8" align="center">2023/05/22</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">N/A *⁴</td>
    <td bgcolor="#c9daf8" align="center">Kindle for PC</td>
    <td bgcolor="#c9daf8" align="center">2.0.1 (70350)</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/10/24</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">N/A *⁴</td>
    <td bgcolor="#c9daf8" align="center">Kindle for PC</td>
    <td bgcolor="#c9daf8" align="center">1.40.1 (65535)</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/05/21</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle*²</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">N/A *⁴</td>
    <td bgcolor="#c9daf8" align="center">Kindle for PC</td>
    <td bgcolor="#c9daf8" align="center">2.0.0 (70301)</td>
    <td bgcolor="#c9daf8" align="center">木龍</td>
    <td bgcolor="#c9daf8" align="center">2023/08/22</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle</td>
    <td bgcolor="#c9daf8" align="center">Mac</td>
    <td bgcolor="#c9daf8" align="center">Macbook 12-inch, Early 2016</td>
    <td bgcolor="#c9daf8" align="center">macOS Monterey 12.6.6</td>
    <td bgcolor="#c9daf8" align="center">Kindle for Mac 1.40.1 (65624)</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/05/22</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle</td>
    <td bgcolor="#c9daf8" align="center">Kindle Previewer3 (Win)</td>
    <td bgcolor="#c9daf8" align="center">N/A *⁴</td>
    <td bgcolor="#c9daf8" align="center">Kindle Previewer3(Win)</td>
    <td bgcolor="#fff2cc" align="center"></td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/05/22</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle</td>
    <td bgcolor="#c9daf8" align="center">Kindle Previewer3 (Mac)</td>
    <td bgcolor="#c9daf8" align="center">MacBook 12-inch, Early 2016</td>
    <td bgcolor="#c9daf8" align="center">macOS Monterey 12.6.6</td>
    <td bgcolor="#c9daf8" align="center">3.72.0</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/05/22</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">kobo</td>
    <td bgcolor="#d9ead3" align="center">iOS</td>
    <td bgcolor="#d9ead3" align="center">iPhone13mini</td>
    <td bgcolor="#d9ead3" align="center">iOS16.4.1 (a)</td>
    <td bgcolor="#d9ead3" align="center">10.3.7</td>
    <td bgcolor="#d9ead3" align="center">古門</td>
    <td bgcolor="#d9ead3" align="center">2023/05/20</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">honto</td>
    <td bgcolor="#c9daf8" align="center">iOS</td>
    <td bgcolor="#c9daf8" align="center">iPhone13mini</td>
    <td bgcolor="#c9daf8" align="center">iOS16.4.1 (a)</td>
    <td bgcolor="#c9daf8" align="center">6.60.0</td>
    <td bgcolor="#c9daf8" align="center">古門</td>
    <td bgcolor="#c9daf8" align="center">2023/05/20</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">honto</td>
    <td bgcolor="#c9daf8" align="center">Android</td>
    <td bgcolor="#c9daf8" align="center">Galaxy Tab S8 Ultra</td>
    <td bgcolor="#c9daf8" align="center">Android 13</td>
    <td bgcolor="#c9daf8" align="center">6.60.0</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/08/20</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kinoppy *³</td>
    <td bgcolor="#c9daf8" align="center">iOS</td>
    <td bgcolor="#c9daf8" align="center">iPhone13mini</td>
    <td bgcolor="#c9daf8" align="center">iOS</td>
    <td bgcolor="#c9daf8" align="center">3.9.17.415162200</td>
    <td bgcolor="#c9daf8" align="center">古門</td>
    <td bgcolor="#c9daf8" align="center">2023/10/23</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kinoppy for Android *³</td>
    <td bgcolor="#c9daf8" align="center">Android</td>
    <td bgcolor="#c9daf8" align="center">Galaxy Tab S8 Ultra</td>
    <td bgcolor="#c9daf8" align="center">Android 13</td>
    <td bgcolor="#c9daf8" align="center">3.10.7 (913557c)</td>
    <td bgcolor="#c9daf8" align="center">仁科</td>
    <td bgcolor="#c9daf8" align="center">2023/10/18</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kinoppy</td>
    <td bgcolor="#c9daf8" align="center">Windows</td>
    <td bgcolor="#c9daf8" align="center">N/A *⁴</td>
    <td bgcolor="#c9daf8" align="center">Windows 10 Home 21H2</td>
    <td bgcolor="#c9daf8" align="center">Ver.3.2.19</td>
    <td bgcolor="#c9daf8" align="center">田嶋</td>
    <td bgcolor="#c9daf8" align="center">2023/5/23</td>
  </tr>
</table>

## 2-2 CSS表示テストの結果

### 2-2-1 メジャーなEPUBリーダーでサポートされているCSS機能

<table>
  <tr>
    <td style="color:#434343" align="right"></td>
    <th><span  style="writing-mode: vertical-rl">Selectors Level 3<span  style="writing-mode: vertical-rl"></span></th>
    <td><span  style="writing-mode: vertical-rl">部分文字列マッチング属性セレクタ [att^=val]</span></td>
    <td><span  style="writing-mode: vertical-rl">部分文字列マッチング属性セレクタ[att$=val]</span></td>
    <td><span  style="writing-mode: vertical-rl">部分文字列マッチング属性セレクタ[att*=val]</span></td>
    <td><span  style="writing-mode: vertical-rl">:root 擬似クラス</span></td>
    <td><span  style="writing-mode: vertical-rl">:nth-child() 擬似クラス</span></td>
    <td><span  style="writing-mode: vertical-rl">:nth-last-child() 擬似クラス</td>
    <td><span  style="writing-mode: vertical-rl">:nth-of-type() 擬似クラス</span></td>
    <td><span  style="writing-mode: vertical-rl">:nth-last-of-type() 擬似クラス</td>
    <td><span  style="writing-mode: vertical-rl">:last-child 擬似クラス</span></td>
    <td><span  style="writing-mode: vertical-rl">:only-child 擬似クラス</span></td>
    <td><span  style="writing-mode: vertical-rl">:first-of-type 擬似クラス</span></td>
    <td><span  style="writing-mode: vertical-rl">:last-of-type 擬似クラス</span></td>
    <td><span  style="writing-mode: vertical-rl">:only-of-type 擬似クラス</span></td>
    <td><span  style="writing-mode: vertical-rl">:empty 擬似クラス</span></td>
    <td><span  style="writing-mode: vertical-rl">:not 擬似クラス</span></td>
    <td><span  style="writing-mode: vertical-rl">::first-letter 擬似要素</span></td>
    <td><span  style="writing-mode: vertical-rl">::before 擬似要素</span></td>
    <td><span  style="writing-mode: vertical-rl">::after 擬似要素</span></td>
    <td><span  style="writing-mode: vertical-rl">後続兄弟結合子 E ~ F</span></td>
    <th valign="bottom">CSS Cascading and Inheritance Level 4</th>
    <td valign="bottom">プロパティの値 initial</td>
    <th valign="bottom">CSS Backgrounds and Borders Level 3</th>
    <td valign="bottom">border-radius プロパティ</td>
    <td valign="bottom">box-shadow プロパティ</td>
    <th valign="bottom">CSS User Interface Module Level 3</th>
    <td valign="bottom">outline プロパティ</td>
    <th valign="bottom">CSS Counter Styles Level 3</th>
    <td valign="bottom">定義済みカウンタースタイル lower-greek</td>
    <td valign="bottom">定義済みカウンタースタイル katakana</td>
    <td valign="bottom">定義済みカウンタースタイル katakana-iroha</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kindle</td>
    <td valign="bottom"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">kobo-1 (iOS)</td>
    <td valign="bottom"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">kobo-2 (Android)</td>
    <td valign="bottom"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">kobo-3</td>
    <td valign="bottom"></td>
    <td style="color:#ff0000" align="center">NG</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">ブック</td>
    <td valign="bottom"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">MURASAKI</td>
    <td valign="bottom"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">honto</td>
    <td valign="bottom"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td style="color:#ea4335" align="center">NG</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td style="color:#ea4335" align="center">NG</td>
    <td align="center"></td>
    <td style="color:#ea4335" align="center">NG</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">BOOK☆ WALKER</td>
    <td valign="bottom"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Kinoppy</td>
    <td valign="bottom"></td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td align="center"></td>
    <td style="color:#ea4335" align="center">NG</td>
    <td align="center"></td>
    <td style="color:#1f1f1f" align="center">OK</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td align="center"></td>
    <td style="color:#ea4335" align="center">NG</td>
    <td align="center"></td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">Voyager</td>
    <td valign="bottom"></td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td align="center"></td>
    <td style="color:#ea4335" align="center">NG</td>
    <td align="center"></td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td align="center"></td>
    <td style="color:#ea4335" align="center">NG</td>
    <td align="center"></td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
    <td style="color:#ea4335" align="center">NG</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">BiB/i</td>
    <td valign="bottom"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td bgcolor="#f3f3f3" align="center">OK / NG *¹</td>
    <td align="center"></td>
    <td bgcolor="#f3f3f3" align="center">OK *²</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
  </tr>
  <tr>
    <td bgcolor="#c9daf8" align="center">超縦書</td>
    <td valign="bottom"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">Vivliostyle Viewer</td>
    <td valign="bottom"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
  </tr>
  <tr>
    <td bgcolor="#d9ead3" align="center">Thorium Reader</td>
    <td valign="bottom"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center"></td>
    <td align="center">OK</td>
    <td align="center">OK</td>
    <td align="center">OK</td>
  </tr>
</table>


### 2-2-2 おもにモダンブラウザ系でサポートされているCSS機能


