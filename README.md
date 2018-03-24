# BopomofoLayoutTest
Test Browser ruby position: inter-charater implement and OpenType feature to tuning Tone Mark position in both horizontal and vertical writing.

## 標注注意事項

- 由於調號（輕聲˙、二聲ˊ、三聲ˇ、四聲ˋ）在UTR#50中會轉90度，所以需要在rt元素中加入text-orientation: upright來使方向一致，調整位置才會正確。
- Chrome的Ruby接受對齊語法，所以需要在rt元素中加入text-align: center讓注音符號居中對齊。
- 注音字體指定若僅套用在ruby標籤時，會因為Fallback在Chrome上加寬與被標註漢字間的距離，所以須在body使用font-family: BopomofoGPOS, serif 來調整。

## 3/22更新字體

詢問Adobe Dr.Ken Lunde，建議使用OpenType GPOS 'vert'，But提供新版字體，追加Case 6。

## 其他測試與相容性

相容於[LibreOffice](https://github.com/harfbuzz/harfbuzz/issues/532#issuecomment-375284467)
