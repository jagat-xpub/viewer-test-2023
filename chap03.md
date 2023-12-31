# 第3章　その他のEPUBビューア表示テスト

## 本扉配置指定テスト

### 調査の概要／目的
冊子体で綴じられた紙の本は、当たり前のことだが、見開きで読まれることを前提として作られてきた。このため、紙の本の体裁を引き継いで作られたリフロー型の電子書籍にも見開きを前提としたページ位置配置の規格がある。これは本扉、章扉などを見開き表示の際に縦書きならば左、横書きならば右に配置する指定に用いられる他、例えば絵画を題材として扱うような本で文中に挿入される見開きの図版を泣き別れにならないように表示させるために使われたりもする。これはEPUB内のOPFファイルにページ配置位置の指定を行うことで指定できるが、以前のテストの際には海外製のビューアを中心に未実装の例が目立った。これを踏まえ、今現在どういった状況にあるかを調査した。

### ページ配置位置の指定方法

EPUBで見開き表示の際に各XHTMLファイルを左右どちらに配置するかを指定するには、EPUB内のOPFファイルのSPINEブロックに以下のような記述を行う必要がある。

```
<spine page-progression-direction="rtl">
<itemref linear="yes" idref="p-cover" properties="page-spread-left" />
<itemref linear="yes" idref="p-toc" />
<itemref linear="yes" idref="p-001" />
<itemref linear="yes" idref="p-002" properties="page-spread-left" />
</spine>
```

「properties="page-spread-left"」が配置位置指定に該当する。「properties="page-spread-right"」なら右ページに配置、「properties="page-spread-left"」なら左ページに配置の指定となる。

### テスト結果

こちらはEPUB独自プロパティへの対応状況の調査となるため、「各OSで利用できるブラウザエンジンに依拠するもの」「独自レイアウトエンジンで動作するもの」への区分は設けず、対応状況を一覧表示した。また、見開き表示そのものに対応していないビューアも少なくないため、それに該当する場合は「-」としている。


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


## 文字の自動ツメ・アキ表示テスト

### 調査の概要／目的

![連続する約物のツメ処理を行わない場合／行った場合](https://github.com/jagat-xpub/viewer-test-2023/blob/main/chap3/img/3-1.png "連続する約物のツメ処理を行わない場合／行った場合")

　和文の組版処理では、一般的に句読点や全角カッコ類などの約物が連続する際には組版ソフト側の処理によって字間スペースの自動ツメ処理が行われ、字間が間延びして見えないように調整されている。

![和欧間自動スペース挿入処理を行わない場合／行った場合](https://github.com/jagat-xpub/viewer-test-2023/blob/main/chap3/img/3-2.png "和欧間自動スペース挿入処理を行わない場合／行った場合／行った場合")

　また、和文の文中に欧文の文字列が挿入された際には自動でスペースの挿入処理が行われ、単語間の区切りをわかりやすくする。これらは通常、組版ソフト側の自動処理で当たり前のように行われ、組版作業者は気づきにくいが、日本語の可読性を上げるための縁の下の力持ち的な技術のひとつと言える。ただ、Webや電子書籍の世界では、日本のみを対象として展開してきた一部の電子書籍ストアアプリやVivliostyleのようなWeb規格の先行実装を実現しているアプリケーションを除き、これまではほぼこういった処理は行われていなかった。

　しかし、W3C等での規格策定の進捗に合わせる形で2023年12月始めにGoogle Chromeに近日中に文字ツメ／アケ関連のプロパティが実装される予定とのアナウンスがあった（[参照](https://developer.chrome.com/blog/css-i18n-features?hl=ja)）。まだ規格策定の段階としてはWDであり、ようやく最初のブラウザ実装が出る程度の段階であるため、規格が確定してメジャーなブラウザ全てで使えるようになるにはしばらく時間はかかりそうだが、いずれは安定して使えるようになることを期待したい。  
　また、こういったW3Cの規格としての文字ツメ／アケ関連プロパティ実装の動きと並行する形で、各EPUBビューアで独自実装、強制適用という形で文字ツメ／アケ処理が行われるようになってきている状況がある。このため、このテストでは2023年12月時点での記録として各ビューアの状況をレポートすることとした。ただし上記のように正式なCSS規格の規格策定進展中という状態であるため、特に外部のブラウザエンジンをレンダリングに使用しているビューアでは将来的に挙動が変化する可能性があることは最初に注記しておく。なお、CSSの該当プロパティ、text-spacing-trim / text-autospace自体の先行実装を行っているVivliostyle Viewerはここではテストから除外した。  
　テストとしては各ビューアが「括弧類が行頭に来た場合に行頭に二分スペースが入るかどうか」「行中で約物が連続した場合にアキの自動ツメ処理を行うかどうか」「和欧文字間に自動でスペースを挿入する処理を行うかどうか」を観察した。

### 文字アケ・文字ツメの指定方法
こちらのテストは各ビューアのデフォルトの文字アケ・文字ツメの挙動を見るものであるため、特にCSSでの指定は行っていない。

### テスト結果

・表入る

「括弧類が行頭に来た場合に行頭に二分スペースが入るかどうか」のテストでも「OK」「NG」の表記を使っているが、こちらのテストで行頭二分下げの処理をすることが望ましいとする意図はないので留意されたい。単純な表示結果の区分として使っている。  
　「各OSで利用できるブラウザエンジンに依拠するアプリ」では、ツメ／アケの独自処理を行っているビューアは見当たらなかった。まだCSSでの正式規格化には至っていないので当然ではあるが、外部エンジンでレンダリング処理を行っている以上、将来的なOS等のアップデートに準じて対応が進む可能性はあるので注視しておきたい。  
　「独自レイアウトエンジンで動作するアプリ」では、以前からツメ／アケ処理を行っていたhonto、Kinoppy以外に、Kindle Previewer3での対応が目立った。これはつい数ヶ月前にWindows版／Mac版アプリのメジャーアップデート完了のアナウンスがあったことと符合するが、Windows版KindleとKindle Previerer3で和欧文字間のアケ処理の挙動に差が出ていることも気になる。Kindle Previerer3はiOS版Kindleとほぼ同じ挙動を示すという話があり、またMac版のKindleアプリはiOS版をベースに作られたらしいとの話もあるようなので、現状Windows版Kindleと他のもので挙動に差異があるということかもしれない。  
　Kindleは現在、全てのデバイスで外部EPUBデータを読み込んで販売時と同じように表示できるわけではないため（Send to Kindleで転送自体はできてもCSSが効かないなどの症状が出る）、テストファイルを用いての完全な検証はできないが、新旧のMac版Kindleアプリで明らかな挙動の違いが見られるため、最後に販売されている本の同一箇所のスクリーンショットを撮ったものを載せておく。左が旧Kindleアプリ（現在Kindle Classicというアプリ名に変わっている）、右が新Kindleアプリの表示画面になる。明らかに連続する約物のツメ処理が効いているのが見て取れる。

![新旧Mac版Kindleアプリの組版比較](https://github.com/jagat-xpub/viewer-test-2023/blob/main/chap3/img/3-3.png "新旧Mac版Kindleアプリの組版比較")

参照：「ティムール帝国」（講談社文庫メチエ）

## イタリック表示字形テスト

### 調査の概要／目的
　欧文では、著者名と作品名が連続で示される場合に作品名の部分をイタリック体にするなど、強調のバリエーションのひとつとしてイタリック体を使用する慣習がある。「イタリック体」は成り立ち的には筆記書体をルーツに持つ活版印刷用の書体であり、日本で一般的な写植の光学変形処理をルーツとする「斜体」とは別に扱われるべきものだが、現在のWebの規格ではイタリック体の代わりにソフトウェア的に変形処理を行った斜体（oblique）を使用することが許容されている。技術的な問題やフォントのソフトウェアライセンスの問題が絡むことによる判断と思われるが、小文字の「a」など、明らかに異なる字形になる文字が存在することもあり、本来的には専用に設計されたイタリック体の字形情報を呼び出して表示するべきなのは間違いない。

![イタリック体と斜体の字形の違い](https://github.com/jagat-xpub/viewer-test-2023/blob/main/chap3/img/4-1.png "イタリック体と斜体の字形の違い")

　それを踏まえてこちらのテストでは電書協ガイドのCSSで「font-style:italic」を指定した際に該当する文字がイタリック体の字形で表示されているかどうかをチェックした。また、電書協ガイドの範疇からは外れるが、埋め込みフォントを使用してイタリック体を指定した際に正しく表示されるかのテストも合わせて行っている。

### イタリック表示の指定方法
font-style:italicの指定は電書協ガイドの規定のstyle-standard.cssの記述をそのまま使って行い、特に追加の指示は入れていない。関係すると思われる箇所は以下。

```
html {
  font-family: serif-ja, serif;
}
```
```
.italic {
  font-style: italic;
}
```

フォント埋め込みは以下の形で指定している。埋め込みにはAdobeがSIL OPEN FONT LICENSEで公開しているSource Code Proを使用し、EPUB内に配置した上でOPFファイルのmanifestブロックにファイル追加のための記述を追加した。

OPF
```
<!-- font -->
<item media-type="application/font-sfnt" id="fonts.SourceCodePro-Medium.ttf" href="fonts/SourceCodePro-Medium.ttf" />
<item media-type="application/font-sfnt" id="fonts.SourceCodePro-MediumIt.ttf" href="fonts/SourceCodePro-MediumIt.ttf" />
```

CSS、XHTMLの記述は以下の通り。

CSS
```
/* フォント指定 */
@font-face {
	font-family:"SourceCodeProMedium";
	font-style:normal;
	src : url("../fonts/SourceCodePro-Medium.ttf");
}
@font-face {
	font-family:"SourceCodeProMedium";
	font-style:italic;
	src : url("../fonts/SourceCodePro-MediumIt.ttf");
}

@font-face {
	font-family:"SourceCodeProMediumIt";
	font-style:normal;
	font-weight:normal;
	src : url("../fonts/SourceCodePro-MediumIt.ttf");
}

.SourceCodeProMedium {
	font-family:"SourceCodeProMedium";
}
.SourceCodeProMediumIt {
	font-family:"SourceCodeProMediumIt";
}
```

XHTML
```
<h4 class="ko-midashi">「lang=&quot;en&quot; xml:lang =&quot;en&quot;」の部分言語指定を行った上で「font-style: italic」を指定</h4>
<p><span lang="en" xml:lang ="en">abc <span style="font-style: italic">abc</span></span> abc</p>

<h4 class="ko-midashi">全体に埋め込みフォントを指定した上で該当箇所に「font-style: italic」を指定</h4>
<p><span class="SourceCodeProMedium">abc <span style="font-style: italic">abc</span> abc</span></p>

<h4 class="ko-midashi">正体の部分とイタリックの部分で別の埋め込みフォントを指定</h4>
<p><span class="SourceCodeProMedium">abc </span><span class="SourceCodeProMediumIt">abc</span><span class="SourceCodeProMedium"> abc</span></p>
```


### テスト結果

＞表入る

　電書協ガイドのCSSのままで「font-style:italic」を指定してイタリック体の字形が表示されたのはhonto、Kinoppyのみ。これらは日本国内をターゲットとしたストアのビューアであるため、日本語表示の最適化のためにWeb標準を超えた相当なカスタマイズが行われていることが覗える。一方でフォント埋め込みの処理を行った場合にイタリック体で表示できたビューアは相当数あったが、アプリ側の表示設定で「オリジナル」「出版者のフォント」等を選ぶ必要があり、読者がそれとは異なるフォントを選んだ場合にはイタリック体で表示されなくなってしまった。ただ、mac版Apple Booksでは埋め込みフォントを指定した場合にはそちらを優先して表示に使う挙動が見られた。デバイスフォントより埋め込みフォントの表示を優先させたいケースはイタリック体の表示に限らずあるため（コンピュータ技術書でのコード部分での等幅フォント使用など）、この実装は制作者側としてはありがたくはある。
　全体として、全てのストアで確実にイタリック体で表示させる指定はなかったが、埋め込みフォント指定と部分言語指定を両方行っておき、該当箇所に「font-style:italic」の指定を行うことが現状での最適解ということになるだろうか。ただし、読者に「オリジナル」「出版者のフォント」等を指定して読んでもらう必要はあるため、そういった注意書きは必要になりそうだ。以下に参照コードを示しておく。


CSS
```
@font-face {
	font-family:"SourceCodeProMedium";
	font-style:normal;
	src : url("../fonts/SourceCodePro-Medium.ttf");
}
@font-face {
	font-family:"SourceCodeProMedium";
	font-style:italic;
	src : url("../fonts/SourceCodePro-MediumIt.ttf");
}
.SourceCodeProMedium {
	font-family:"SourceCodeProMedium";
}
```

XHTML
```
<p><span  lang="en" xml:lang ="en" class="SourceCodeProMedium">abc <span style="font-style: italic">abc</span> abc</span></p>
```

　なお、イタリック体の表示には各EPUBビューアが表示に使用しているOpentypeの日本語商用フォントが内部に持っていると考えられるイタリック体の字形情報を「font-feature-settings:ital」で呼び出す方法も考えられるが、これはビューア側の仕様変更で容易に表示が崩れる可能性があること、「font-feature-settings:ital」を併せて指定した場合に効果が重複して表示されるビューアがあったことから参考情報に留めておくこととしたい。

## 画像内代替文字検索／読み上げテスト

### 調査の概要／目的
EPUBビューア内の画像には読み上げ・検索用に代替文字（alt）を設定することができるが、長らくほとんどのビューアでは画像代替文字の読み上げ・検索はできなかった。しかし、2023年5月に正式規格化されたEPUB3.3ではアクセシビリティ対応を主要な変更点として謳っており、画像の読み上げ・検索対応は喫緊の課題となっている。これを踏まえ、各EPUBビューアが画像の読み上げ・検索に対応しているかを調査した。

### 画像内代替文字の指定方法
画像のalt属性の値として、画像内の文字と同じものを記述し、読み上げ／検索が効くかどうかを調査した。

```
<p><img class="fit" src = "../image/image001.png" alt = "智に働けば角が立つ。情に棹させば流される。意地を通せば窮屈だ。とかくに人の世は住みにくい。住みにくさが高じると、安い所へ引き越したくなる。どこへ越しても住みにくいと悟った時、詩が生れて、画が出来る。人の世を作ったものは神でもなければ鬼でもない。やはり向う三軒両隣りにちらちらするただの人である。ただの人が作った人の世が住みにくいからとて、越す国はあるまい。あれば人でなしの国へ行くばかりだ。人でなしの国は人の世よりもなお住みにくかろう。" /></p>
```

### テスト結果
