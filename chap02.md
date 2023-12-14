---
link:
  - rel: 'stylesheet'
    href: 'css/main.css'
lang: 'ja'
---

# EPUBリーダー表示テスト報告書（2023年）

## 第2章CSS表示テストの結果


### はじめに


### すべてのEPUBリーダーでサポートされている
- CSS Values and Units Level 3
    - 長さの単位 rem
### ほとんどのEPUBリーダーでサポートされている
- Selectors Level 3
    - 部分文字列マッチング属性セレクタ [att^=val]
    - 部分文字列マッチング属性セレクタ[att$=val]
    - 部分文字列マッチング属性セレクタ[att*=val]
    - :root 擬似クラス
    - :nth-child() 擬似クラス
    - :nth-last-child() 擬似クラス
    - :nth-of-type() 擬似クラス
    - :nth-last-of-type() 擬似クラス
    - :last-child 擬似クラス
    - :only-child 擬似クラス
    - :first-of-type 擬似クラス
    - :last-of-type 擬似クラス
    - :only-of-type 擬似クラス
    - :empty 擬似クラス
    - :not 擬似クラス
    - ::first-letter 擬似要素
    - ::before 擬似要素
    - ::after 擬似要素
    - 後続兄弟結合子 E ~ F
    - ::first-line 擬似要素（モダンブラウザ系以外では、honto でOK）
- CSS Values and Units Level 3
    - 長さの単位 ch / 長さの単位 vw / 長さの単位 vh / 長さの単位 vmin / 長さの単位 vmax / 長さの単位 Q（モダンブラウザ系以外では、Kobo、honto、Konoppy、超縦書（Q 以外）でOK）


### メジャーなEPUBリーダーでサポートされている
- CSS Color Level 4
    - opacity プロパティ（honto、Kinoppy、Voyager でNG）
- CSS Backgrounds and Borders Level 3
    - border-radius プロパティ（honto、Kinoppy、Voyager でNG）
    - box-shadow プロパティ（honto、Kinoppy、Voyager でNG）
- CSS User Interface Module Level 3
    - outline プロパティ（honto、Kinoppy、Voyager でNG）


### モダンブラウザ系でのみサポートされている
- CSS Cascading and Inheritance Level 4
    - all プロパティ（ただし、BiB/i でNG）
    - プロパティの値 unset / プロパティの値 revert（モダンブラウザ系以外では、honto でOK）
- CSS Custom Properties for Cascading Variables Module Level 1
    - CSS変数
- CSS Color Level 4
    - rgb() 関数のコンマなし形式　例: rgb (0 255 0 / .5)
    - 16進数のRGBA形式（8桁）
    - 16進数のRGBA形式（4桁）
    - hsl() 関数
    - hwb() 関数
- CSS Backgrounds and Borders Level 3
    - 複数の背景画像（モダンブラウザ系以外では、Kobo、Kinoppy iOS版アプリ、超縦書 でOK）
    - border-image プロパティ（モダンブラウザ系以外では、Kobo、超縦書 でOK）
- CSS Images Level 3
    - グラデーション関数 linear-gradient() （モダンブラウザ系以外では、Kobo、超縦書 でOK）
    - グラデーション関数 radial-gradient() （モダンブラウザ系以外では、Kobo、超縦書 でOK）
    - グラデーション関数 repeating-linear-gradient() （モダンブラウザ系以外では、Kobo、超縦書 でOK）
    - グラデーション関数 repeating-radial-gradient()（モダンブラウザ系以外では、Kobo、超縦書 でOK）
    - object-fit プロパティ contain（モダンブラウザ系以外では、超縦書 でOK）
    - object-fit プロパティ cover（モダンブラウザ系以外では、超縦書 でOK）
    - object-position プロパティ（モダンブラウザ系以外では、超縦書 でOK）
- CSS Fonts Level 3
    - @font-face ルール（モダンブラウザ系以外では、Kobo、Kinoppy、超縦書 でOK）
    - unicode-range 記述子（モダンブラウザ系以外では、Kobo、超縦書 でOK）
    - font-kerning プロパティ
    - font-variant プロパティ
    - font-feature-settings プロパティ
- CSS Writing Modes Level 3
    - writing-mode プロパティ vertical-rl（モダンブラウザ系以外では、honto、Kinoppy、Voyager でOK）
    - text-orientation プロパティ upright（モダンブラウザ系以外では、honto、Kinoppy、Voyager でOK）
    - text-orientation プロパティ sideways（モダンブラウザ系以外では、honto、Kinoppy、Voyager でOK）
- CSS Multi-column Layout Level 1（ただし、BOOK☆WALKER Android版アプリ でNG）
    - 段組 2段組
    - 段組 段間罫
    - 段抜き：column-span プロパティ
    - 段バランス：column-fill: balance
    - 段バランス：column-fill: auto
- CSS Flexible Box Module Level 1
    - Flexboxによる上下中央揃え（モダンブラウザ系以外では、超縦書 でOK）
- CSS User Interface Module Level 3（モダンブラウザ系以外では、Kobo、超縦書 でOK）
    - box-sizing プロパティ border-box
    - box-sizing プロパティ content-box
- CSS Containment Module Level 1
    - contain プロパティ
- CSS Transforms Level 1
    - transform プロパティ
- CSS Compositing and Blending Level 1
    - mix-blend-mode プロパティ
    - isolation プロパティ
    - background-blend-mode プロパティ
- CSS Counter Styles Level 3
    - @counter-style ルール（ただし、Vivliostyle Viewer でNG）
    - 定義済みカウンタースタイル cjk-decimal（モダンブラウザ系以外では、Kindle、Kobo、honto、超縦書 で一部がOK）
    - 定義済みカウンタースタイル lower-greek（モダンブラウザ系以外では、Kindle、Kobo、honto、超縦書 で一部がOK）
    - 定義済みカウンタースタイル hiragana（モダンブラウザ系以外では、Kindle、Kobo、honto、超縦書 で一部がOK）
    - 定義済みカウンタースタイル hiragana-iroha（モダンブラウザ系以外では、Kindle、Kobo、honto、超縦書 で一部がOK）
    - 定義済みカウンタースタイル katakana（モダンブラウザ系以外では、Kindle、Kobo、honto、超縦書 で一部がOK）
    - 定義済みカウンタースタイル katakana-iroha（モダンブラウザ系以外では、Kindle、Kobo、honto、超縦書 で一部がOK）
    - 定義済みカウンタースタイル cjk-earthly-branch（モダンブラウザ系以外では、Kindle、Kobo、honto、超縦書 で一部がOK）
    - 定義済みカウンタースタイル cjk-heavenly-stem（モダンブラウザ系以外では、Kindle、Kobo、honto、超縦書 で一部がOK）
    - 定義済みカウンタースタイル japanese-informal（モダンブラウザ系以外では、Kindle、Kobo、honto、超縦書 で一部がOK）

