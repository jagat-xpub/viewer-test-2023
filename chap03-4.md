## イタリック表示字形テスト

### 調査の概要／目的
　欧文では、著者名と作品名が連続で示される場合に作品名の部分をイタリック体にするなど、強調のバリエーションのひとつとしてイタリック体を使用する慣習がある。「イタリック体」は成り立ち的には筆記書体をルーツに持つ活版印刷用の書体であり、日本で一般的な写植の光学変形処理をルーツとする「斜体」とは別に扱われるべきものだが、現在のWebの規格ではイタリック体の代わりにソフトウェア的に変形処理を行った斜体（oblique）を使用することが許容されている。技術的な問題やフォントのソフトウェアライセンスの問題が絡むことによる判断と思われるが、小文字の「a」など、明らかに異なる字形になる文字が存在することもあり、本来的には専用に設計されたイタリック体の字形情報を呼び出して表示するべきなのは間違いない。

![イタリック体と斜体の字形の違い](../../../Dropbox/JAGAT_EPUB%E3%83%86%E3%82%B9%E3%83%88%E3%83%AC%E3%83%9B%E3%82%9A%E3%83%BC%E3%83%88%E7%94%A8%E5%8E%9F%E7%A8%BF/4-1.png)

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