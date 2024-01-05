## 実ページ番号表示テスト

### 調査の概要／目的
紙の本には当然ながらページ番号が記述されており、これはその本の内部での参照や他の本からの参照の方法として使われている。リフロー型電子書籍では文字サイズ・画面サイズによってページが随時生成されるため、紙の本と同じようにページ番号を利用した参照はできなかった。ただ、電子教科書では複数人が指示された特定のページを開く必要があるというニーズがあったため、早くからEPUB内に紙の本のページ番号を記述する方法は規格化されていた。だがこれの実装は一部を除いて一般向けのEPUBビューアには普及していなかった状況があった。  

しかし、2023年4月に正式にW3C規格化されたEPUB Accessibility 1.1内で「EPUB requirements」として「Page navigation」の記述が入り、EPUB Accessibilityを取り込んで2023年5月に規格化されたEPUB3.3でも主な変更点としてアクセシビリティ対応を謳っている状況がある。これを踏まえて、各EPUBビューアが現時点でどこまでリフロー型EPUB内への紙の本のページ番号の記述に対応しているかを調査した。

### 紙の本のページ番号の指定方法
EPUB内に紙の本のページ番号の記述を指定するには、ナビゲーション文書と本文内の各ページ開始位置にそれぞれ記述を行う必要がある。  

ナビゲーション文書の指定は以下のような形になる。

```
<nav epub:type="page-list">
 <ol>
   <li><a href="xhtml/p-002.xhtml#page001">1</a></li>
   <li><a href="xhtml/p-002.xhtml#page002">2</a></li>
   <li><a href="xhtml/p-002.xhtml#page003">3</a></li>
   <li><a href="xhtml/p-002.xhtml#page004">4</a></li>
   <li><a href="xhtml/p-002.xhtml#page005">5</a></li>
   <li><a href="xhtml/p-002.xhtml#page006">6</a></li>
   <li><a href="xhtml/p-002.xhtml#page007">7</a></li>
   <li><a href="xhtml/p-002.xhtml#page008">8</a></li>
   <li><a href="xhtml/p-002.xhtml#page009">9</a></li>
 </ol>
</nav>
```

本文内に入れる各ページ開始位置の指定の記述は以下。

```
<p>本文本文本文本文<span id="page001" epub:type="pagebreak" role="doc-pagebreak" aria-label="1" title="1"/>本文本文本文本文本文</p>
```

「```<span id="page001" epub:type="pagebreak" role="doc-pagebreak" aria-label="1" title="1"/>```」が指定に該当する。なお、title属性の値はビューアで表示する際の指定なので、目次など前付けのブロックにローマ数字を採用している本などにも問題なく対応できる。

### テスト結果
こちらはEPUB独自プロパティへの対応状況の調査となるため、「各OSで利用できるブラウザエンジンに依拠するもの」「独自レイアウトエンジンで動作するもの」への区分は設けず、対応状況を一覧表示した。