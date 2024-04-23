# EPUBリーダー表示テスト報告書（2023年度）

このリポジトリは、JAGAT次世代パブリッシング研究会が2023年度に実施した、EPUBリーダー表示テストの報告書制作を目的に作成されました。

## 成果の公開

- EPUBリーダー表示テスト報告書（2023年度）
  - [第1章 この調査の目的と方法](https://github.com/jagat-xpub/viewer-test-2023/blob/main/chap01.pdf)
  - [第2章 CSS表示テスト](https://github.com/jagat-xpub/viewer-test-2023/blob/main/chap02.pdf)
  - [第3章 その他のEPUBリーダー表示テスト](https://github.com/jagat-xpub/viewer-test-2023/blob/main/chap03.pdf)
  - [第4章 国内EPUBリーダーにおける本文／alt属性の読み上げの状況（ダイジェスト版）](https://github.com/jagat-xpub/viewer-test-2023/blob/main/ALT_text_check_JEPAVersion_20240424.pdf)

## プレビュー、ビルドの方法（第1章〜第3章）

1. 準備：[VSCode](https://azure.microsoft.com/ja-jp/products/visual-studio-code)に、機能拡張[vivliostyle-cli-helper](https://marketplace.visualstudio.com/items?itemName=Libroworks.vivliostyle-cli-helper)をインストールしておく
2. このリポジトリをローカルに同期かダウンロードして、VSCodeで開く
3. 第1章〜第3章のいずれかを開く
4. プレビュー：編集画面で以下の順に選択
  4-1. 右クリック＞vivliostyle-cli-helper＞これプレビューvivliostyle preview (Current File)
5. プレビューウィンドウを閉じる
6. PDF作成：編集画面で以下の順に選択
  6-1. 右クリック＞vivliostyle-cli-helper＞これビルドvivliostyle build (Current File)