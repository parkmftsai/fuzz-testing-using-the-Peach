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
```
20180723
首先我們使用python2.6 編譯Peach-2.3.7
在此遇到兩個蠻難處理的問題
1.4Suite的Ft無法順利import
2.No module named zlib found
首先，處理第一個問題，跑出以下狀況
Error loading 4Suite XML library.  This library can be installed 
from the dependencies folder or downloaded from http://4suite.org/.

於是，我們先進入peach.py找這一段敘述，可以看見以下程式碼
try:
	import Ft
except:
	print "\nError loading 4Suite XML library.  This library"
	print "can be installed from the dependencies folder or"
	print "downloaded from http://4suite.org/.\n\n"
	sys.exit(0)
所以大概可以猜測，Ft並沒有被找到，可能安裝4Suite路徑要修改
，路徑儲存在4Suite資料夾裡頭config.cache中，因為我們是使用python2.6版本，
所以必須看以下這段
[linux-x86_64-2.6]
docdir = /usr/local/share/doc/$name
localedir = /usr/local/share/locale
pythonlibdir = /usr/local/python2.6/lib/python2.6/site-packages
sysconfdir = /usr/local/etc/$name
exec_prefix = 
libdir = /usr/local/lib/$name
datadir = /usr/local/share/$name
localstatedir = /var/local/lib/$name
prefix = 
includedir = /usr/local/include/$name
debug = False
mandir = /usr/local/share/man
bindir = /usr/local/bin
compiler = 
其中pythonlibdir是4Suite安裝路徑，要修改成當前python2.6site-packages路徑，如下
pythonlibdir = /usr/local/lib/python2.6/site-packages

再來是第二個問題，No module named zlib found代表找不到zlib，
原來，python2.6在安裝時並無默認zlib，很奇怪在setup.py裡面反而有針對zlib安裝的code，怪哉
，欲解決此問題可以參考
https://blog.csdn.net/huanhuanq1209/article/details/72673236
以下這段很重要
    $ wget -c https://www.python.org/ftp/python/2.7.9/Python-2.7.9.tgz  
    $ tar -xzvf Python-2.7.9.tgz  
    $ cd Python-2.7.9/  
    $ LDFLAGS="-L/usr/lib/x86_64-linux-gnu" ./configure  
    $ make  
    $ sudo make install   
```
