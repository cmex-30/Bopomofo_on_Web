# 注音符號數位化顯示計畫

（作者：@bobbytung 2018/4/19編輯，未完）

本Repo主要目的是：尋求讓中文注音符號，在Web以及其他環境下，能以更符合數位化需求的方式呈現的方法。

## 傳統的做法：注音字型

![](https://github.com/bobbytung/Bopomofo_on_Web/blob/master/images/bopomofofont.jpg)
（攝於國語日報社展示櫥窗）

活字印刷時代，注音符號於印刷上使用將漢字及注音符號鑄於一體銅膜來製作鉛字。若一字有多種讀音，則鑄造多種鉛字備用。

當轉到電腦字體時代時，依然保持相同的作法。將注音符號與漢字造於電腦字型的同一個字符（Glyph）中，並且按照教育部[一字多音審訂表](https://github.com/g0v/moedict-data-csld/blob/master/國語一字多音審訂表2012.csv)造成多組字型檔案。注音字型由於能夠確實重現[國語注音符號手冊](http://language.moe.gov.tw/001/Upload/files/site_content/M0001/juyin/index.html)上對印刷排版注音符號比例的需求，而成為主流的數位排版印刷採用的方式。

## 為什麼不建議使用注音字型

但注音字型在廣泛應用於數位環境時，會遇到多種問題，如：

- 缺乏語義資訊

注音字型若要使用在網頁上，則需要透過字體標注來切換，例如：

    CSS
     @font-face {
      font-family: "Bopomofo01";
      src: url("Bopomofo01.ttf");}
      .sound1 {
      font-family: "Bopomofo01";}
      ......重複1-6

    HTML
    <p>這個字唸<span class="sound1">作</span>什麼</p>

如此一來，在缺乏外部資料的狀況下，我們無法辨別該字的讀音為何。

- 無法顯示例外狀況

例外狀況包括：教育部一字多音審定表外的讀法，以及刻意的誤字（如教師出的試卷）。

-----

# Web使用HTML Ruby標註

早在2001年網頁標準的測定中，就已經將注音符號納入[Ruby規範](https://www.w3.org/TR/2001/WD-css3-ruby-20010216/)之中，但標註方式以及顯示方式，直到2012年HTML 5規格確立以後才底定。


## 注音符號使用的字元

聲調 | 符號 | Unicode代碼 | Unicode名稱
------- | ------- | ------- | -------
輕聲 | ˙ | U+02D9 | DOT ABOVE
二聲 | ˊ | U+02CA | MODIFIER LETTER ACUTE ACCENT
三聲 | ˇ | U+02C7 | CARON
四聲 | ˋ | U+02CB | MODIFIER LETTER GRAVE ACCENT


## 注音符號標注方式

二三四聲置於注音符號之後

    <ruby>我<rt>ㄨㄛˇ</rt></ruby>

輕聲置於注音符號之前

    <ruby>呢<rt>˙ㄋㄜ</rt></ruby>





# 注音符號版面呈現測試
Test Browser ruby position: inter-charater implement and OpenType feature to tuning Tone Mark position in both horizontal and vertical writing.

## 標注注意事項

- 由於調號（輕聲˙、二聲ˊ、三聲ˇ、四聲ˋ）在UTR#50中會轉90度，所以需要在rt元素中加入text-orientation: upright來使方向一致，調整位置才會正確。
- Chrome的Ruby接受對齊語法，所以需要在rt元素中加入text-align: center讓注音符號居中對齊。
- 注音字體指定若僅套用在ruby標籤時，會因為Fallback在Chrome上加寬與被標註漢字間的距離，所以須在body使用font-family: BopomofoGPOS, serif 來調整。

## 3/22更新字體

詢問Adobe Dr.Ken Lunde，建議使用OpenType GPOS 'vert'，But提供新版字體，追加Case 6。

## 其他測試與相容性

相容於[LibreOffice](https://github.com/harfbuzz/harfbuzz/issues/532#issuecomment-375284467)
