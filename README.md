# EPUBリーダー表示テスト報告書（2023年度）

このリポジトリは、JAGAT次世代パブリッシング研究会が2023年度に実施した、EPUBリーダー表示テストの報告書制作を目的に作成されました。

## 成果の公開

- EPUBリーダー表示テスト報告書（2023年度）
  - [第1章 この調査の目的と方法](https://github.com/jagat-xpub/viewer-test-2023/blob/main/chap01.pdf)
  - [第2章 CSS表示テスト](https://github.com/jagat-xpub/viewer-test-2023/blob/main/chap02.pdf)
  - [第3章 その他のEPUBリーダー表示テスト](https://github.com/jagat-xpub/viewer-test-2023/blob/main/chap03.pdf)
    - [付録：国内EPUBリーダーにおける本文／alt属性の読み上げの状況（ダイジェスト版）](https://github.com/jagat-xpub/viewer-test-2023/blob/main/ALT_text_check_JEPAVersion_20240424.pdf)
  - [第4章 電書協EPUB3制作ガイドに基づく文字、画像、背景表示テスト](https://github.com/jagat-xpub/viewer-test-2023/blob/main/EPUBviewerCheck_Chap4_20240424.pdf)
- テストファイル開発リポジトリ（GitHub）
   - [EPUBリーダーのCSS仕様適合性テスト](https://github.com/jagat-xpub/epub-css-test/tree/main)
- テスト結果（Googleスプレッドシート）
  - [EPUBリーダー表示チェック（JAGAT次世代パブリッシング研究会）2023公開用](https://docs.google.com/spreadsheets/u/1/d/e/2PACX-1vSPaWWfqx2bZiRqK__XG_v_NEGY5OjB-lIcoG9Ll_D1aG5UA7RwpUi3dOq4fLTt40flSuFGhu38Iv7o/pubhtml#)

## プレビュー、ビルドの方法（第1章〜第3章）

1. 準備：[VSCode](https://azure.microsoft.com/ja-jp/products/visual-studio-code)に、機能拡張[vivliostyle-cli-helper](https://marketplace.visualstudio.com/items?itemName=Libroworks.vivliostyle-cli-helper)をインストールしておく
2. このリポジトリをローカルに同期かダウンロードして、VSCodeで開く
3. 第1章〜第3章のいずれかのMarkdownファイルを開く
4. プレビュー：編集画面で以下の順に選択
    - 右クリック＞vivliostyle-cli-helper＞これプレビューvivliostyle preview (Current File)
5. PDF作成：編集画面で以下の順に選択（プレビューしていた場合は必ずウィンドウを閉じる）
    - 右クリック＞vivliostyle-cli-helper＞これビルドvivliostyle build (Current File)

- 参考：[vivliostyle-cli-helper を使った本作り](https://vivliostyle.github.io/vivliostyle-cli-helper-doc/#/)