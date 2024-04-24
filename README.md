# EPUBリーダー表示テスト報告書（2023年度）

このリポジトリは、JAGAT次世代パブリッシング研究会が2023年度に実施した、EPUBリーダー表示テストの報告書制作を目的に作成されました。

## 成果の公開

- EPUBリーダー表示テスト報告書（2023年度）
  - [第1章 この調査の目的と方法［PDF］](https://github.com/jagat-xpub/viewer-test-2023/blob/main/PDF/chap01.pdf)
  - [第2章 CSS表示テスト［PDF］](https://github.com/jagat-xpub/viewer-test-2023/blob/main/PDF/chap02.pdf)
  - [第3章 その他のEPUBリーダー表示テスト［PDF］](https://github.com/jagat-xpub/viewer-test-2023/blob/main/PDF/chap03.pdf)
    - [付録：国内EPUBリーダーにおける本文／alt属性の読み上げの状況（ダイジェスト版）［PDF］](https://github.com/jagat-xpub/viewer-test-2023/blob/main/PDF/ALT_text_check_JEPAVersion_20240424.pdf)
  - [第4章 電書協EPUB3制作ガイドに基づく文字、画像、背景表示テスト［PDF］](https://github.com/jagat-xpub/viewer-test-2023/blob/main/PDF/DPFJ_EPUBCheck_Chap4_20240424.pdf)
- テストファイル開発リポジトリ（GitHub）
   - [EPUBリーダーのCSS仕様適合性テスト](https://github.com/jagat-xpub/epub-css-test/tree/main)
- テスト結果（Googleスプレッドシート）
  - [EPUBリーダー表示チェック（JAGAT次世代パブリッシング研究会）2023公開用](https://docs.google.com/spreadsheets/u/1/d/e/2PACX-1vSPaWWfqx2bZiRqK__XG_v_NEGY5OjB-lIcoG9Ll_D1aG5UA7RwpUi3dOq4fLTt40flSuFGhu38Iv7o/pubhtml#)

## JEPA（日本電子出版協会）セミナーでの発表

- [2024年4月24日 各社のEPUBリーダーは、現行CSS仕様やアクセシビリティをどれだけサポートしているのか？（2024年4月24日）](https://www.jepa.or.jp/seminar/20240424/)
  - JAGAT 次世代パブリッシング研究会の紹介：小形克宏（10分）16:00-16:10[［PDF］](https://github.com/jagat-xpub/viewer-test-2023/blob/main/PDF/20240424-chap2-ogata.pdf)
  - EPUBリーダー表示テスト報告書（2023年度）
    - 第2章 CSS表示テスト
      - 2-1 はじめに：小形克宏（5分）16:10-16:15[［PDF］](https://github.com/jagat-xpub/viewer-test-2023/blob/main/PDF/20240424-chap2-ogata.pdf)
      - 2-2 CSS表示テストの結果：村上真雄（10分）16:15-16:25[［PDF］](https://github.com/jagat-xpub/viewer-test-2023/blob/main/PDF/chap02-02.pdf)
      - 2-3 おわりに：小形克宏（5分）16:25-16:30[［PDF］](https://github.com/jagat-xpub/viewer-test-2023/blob/main/PDF/20240424-chap2-ogata.pdf)
      - 付録 使えたらうれしいCSSプロパティ：田嶋淳（5分）16:30-16:35[［PDF］](https://github.com/jagat-xpub/viewer-test-2023/blob/main/PDF/wantedCSSproperty.pdf)
    - 第3章 その他のEPUBリーダー表示テスト（15分）16:35-16:50[［PDF］](https://github.com/jagat-xpub/viewer-test-2023/blob/main/PDF/4_24_JEPA_TAJIMA.pdf)
      - 付録 国内EPUBリーダーにおける本文／alt属性の読み上げの状況：仁科哲（15分）16:50-17:05[［PDF］](https://github.com/jagat-xpub/viewer-test-2023/blob/main/PDF/ALT_text_check_JEPAVersion_20240424.pdf)
    - 第4章  EPUB内文字、画像、背景表示テスト：仁科哲（15分）17:05-17:20[［PDF］](https://github.com/jagat-xpub/viewer-test-2023/blob/main/PDF/DPFJ_EPUBCheck_Chap4_20240424.pdf)
  - 質疑応答：（10分）17:20-17:30

## 報告書のプレビュー、及びPDF作成の方法（第1章〜第3章）

1. 準備：[VSCode](https://azure.microsoft.com/ja-jp/products/visual-studio-code)に、機能拡張[vivliostyle-cli-helper](https://marketplace.visualstudio.com/items?itemName=Libroworks.vivliostyle-cli-helper)をインストールしておく
2. このリポジトリをローカルに同期かダウンロードして、VSCodeで開く
3. 第1章〜第3章のいずれかのMarkdownファイルを開く
4. プレビュー：編集画面で以下の順に選択
    - 右クリック＞vivliostyle-cli-helper＞これプレビューvivliostyle preview (Current File)
5. PDF作成：編集画面で以下の順に選択（プレビューしていた場合は必ずウィンドウを閉じる）
    - 右クリック＞vivliostyle-cli-helper＞これビルドvivliostyle build (Current File)

- 参考情報：[vivliostyle-cli-helper を使った本作り](https://vivliostyle.github.io/vivliostyle-cli-helper-doc/#/)