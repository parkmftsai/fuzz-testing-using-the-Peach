# fuzz-testing-using-the-Peach
```
20180508
今天針對fuzzy testing進行資料搜集，使用的套件為peach
詳請可見
http://book.51cto.com/art/201107/275204.htm
裡頭很多大陸用語，看了不甚習慣
```
```
20180510
大概知道peach的做法了，但是還更需要一些detail的部份（例如python上peach的語法XD）
其實還要考量XML的生成方式
網路上並沒有一個較有效的生成方式，所以我還是照舊使用python生成XML
當然，還是要以peach能接受的格式為主，以下網址講解還算清楚
http://book.51cto.com/art/201107/275204.htm
之後的架構大概是這樣
餵資料-->XML生成-->peach產生亂數資料-->測試
這麼做的用意如下
1.可以使用一種語言，一氣呵成
2.以python做XML格式生成，在使用以及維護這兩種層面上，較容易操作
3.架構簡潔=修改容易
```
```
20180720
peach 在linux底下似乎只能使用python2.7以下版本執行


這裡是peach與sulley比較，感覺peach比較專注在xml開發上，sulley似乎在使用上比較有彈性
，兩者各有優點，如要使用需要思考一下。
https://blog.csdn.net/u012397189/article/details/78122418

```
