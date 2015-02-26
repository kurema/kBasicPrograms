#携帯Basic プログラミングリファレンス
##はじめに
この内容は携帯Basicにおけるプログラミングの手法やコツを示したものです。
携帯Basicのプログラミングは言語仕様と環境上かなり独特なものとなっており、他のプログラミング言語を既に知っている人にとってはとっつきづらい部分も少なくありません。
ここでは、当時の記憶を辿って携帯Basicの奥深さを示していきたいと思います。
##特徴
携帯BasicはWindows以前のBasicライクな文法を備え、構造化やオブジェクト指向に対応していない、携帯電話上で動くBasicです。
もともとDocomoで動くiBASICという環境が有り、それをsatoo様がVodafone向けに改良・移植したものです。  
Basicらしく、ローカル変数は存在しない、データ型はなく文字列を場合によって数値と解釈、特殊な変数が存在するなど、分かり易い仕様になっています。  
この環境の何より魅力的なのは、**実機上でプログラミングが可能**でかつその場で実行可能な点です。唯一手許にあって、自由に使えるコンピューターが携帯電話であるというときにこれは本当に魅力的でした。  
プログラミングで注意しなければいけない事は幾つかありますが、最も大事で否応なく気付かされることは携帯Basicは「**とてつもなく遅い**」という事です。  
プログラミングをする時はこの事に注意し、対策していかなければなりません。
##言語仕様
satoo様のホームページより。
###基本
データ型は存在せず、全て文字列です。文字列の内容が数字である時に限って数として取り扱えます。数字は32ビット符号なし整数で浮動小数点数はもちろん固定小数点数も標準では扱えません[テクニック/数値型の自前実装]。ブール関数は数字を返します。  
複数スレッドに渡るプログラムを書く事が出来ますが、その場合先頭文字が大文字の場合は共通してアクセスできるのでスレッド間通信として利用できます。  
配列も存在し、\[\]で囲むことで示すことができます。配列の要素番号には負数も利用できます。  
変数であれ、配列であれ宣言は不要です。
###条件分岐・繰り返し
代入は通例通り"="で可能です。文字列は""で囲みます。数字は囲んでも囲まなくとも結果に影響はありません。
```
string="hello"
number=1234
```

条件分岐はif命令が用意されています。
```
if number>1000 then result=1 else result=0 endif
```

ジャンプにはgotoとgosubを使います。行番号は存在せずラベルを使います。gotoはスタックを破壊するので戻る事が出来ませんが、gosubでは戻れます。関数やクラスは存在しません。
```
gosub"sub"
goto terminate

label"sub"
value=value+1
return

label terminate
exit
```
gotoやgosubの引数は文字列です。これによってリフレクションに似たに動作が可能です[テクニック/関数ポインタ]。

whileやforといった命令も用意されています。
```
while value=1
gosub"check"
wend
```
```
for i=0 to 9 step 2
value=value+i
next
```
while内でendを実行する事は出来ません。[テクニック/while内でのend]

実行中スレッドの終了は``end``、アプリの終了は``exit``を使います。

コメントは``rem``や``'``で可能です。``'コメント'``の様に行内のコメントも可能です。
###命令
####演算子
演算子は以下が用意されています。
> ( ) * / % + - not (単項演算子)  
> \+ - (二項演算子)  
> = < <= > >= <> and or xor  

(http://satoo.jp/i/basic/ref03.shtml)

####戻り値なし関数
関数|内容
---|---
text(a1,a2,a3)|座標(a2,a3)に文字列a1を描画.a3はﾍﾞｰｽﾗｲﾝ(下)
setfont(a1)|フォントのサイズを指定。a1は"T"（極小）,"S"（小）,"M"（中）,"L"（大）を指定。初期設定では"T"
clear(a1,a2,a3,a4)|座標(a1,a2)から幅a3,高さa4を消去
line(a1,a2,a3,a4)|座標(a1,a2)から座標(a3,a4)まで線を引く
rect(a1,a2,a3,a4)|座標(a1,a2)から幅a3,高さa4の四角を描画
frect(a1,a2,a3,a4)|座標(a1,a2)から幅a3,高さa4の矩形を塗りつぶす
color(R,G,B)|描画色を設定
arc(a1,a2,a3,a4)|座標(a1,a2)から幅a3,高さa4の楕円を描画
farc(a1,a2,a3,a4)|座標(a1,a2)から幅a3,高さa4の楕円を塗り潰す
origin(a1,a2)|座標(a1,a2)に以降の描画操作の原点を設定
lock()|unlockするまで描画内容が画面へ反映されない
unlock(a1)|lockした画面を描画.a1がｾﾞﾛの場合前にlock()した回数だけ呼び出すと描画反映、a1が非ｾﾞﾛならすぐに描画反映
clearinput()|入力ﾊﾞｯﾌｧを消去
thread(a1,a2)|ﾀｲﾄﾙa1のﾌﾟﾛｸﾞﾗﾑを新たなｽﾚｯﾄﾞ名a2で起動.ﾛｰｶﾙ変数はｺﾋﾟｰされる.描画原点や描画色はされない.ｽﾚｯﾄﾞ名がすでに存在したら既存ｽﾚｯﾄﾞ強制終了.ｱﾌﾟﾘ内にｽﾚｯﾄﾞが無くなるとｱﾌﾟﾘ終了
join(a1)|ｽﾚｯﾄﾞa1の終了まで待機
kill(a1)|ｽﾚｯﾄﾞa1を強制終了
yield()|他ｽﾚｯﾄﾞにCPU時間を譲る
sleep(a1)|a1ﾐﾘ秒ｽﾚｯﾄﾞを休眠
gc()|ｶﾞﾍﾞｰｼﾞｺﾚｸﾄ
onvib()|ﾊﾞｲﾌﾞON
offvib()|ﾊﾞｲﾌﾞOFF
onlight()|バックライトON
offlight()|バックライトOFF
soft1(a1)|ソフトキー1の名前にa1を設定
soft2(a1)|ソフトキー2の名前にa2を設定
save(a1)|プログラムのセーブ領域にa1を保存する
input()|何かキー入力があるまで待つ
loadimg(a1,a2)|変数a1に画像ソース"a2"をロードする
drawimg(a1,a2,a3)|画像a1をa2,a3の位置に描画する
imgdispose(a1)|画像a1を破棄する
dispose(a1)|変数a1を破棄する
(http://satoo.jp/i/basic/ref04.shtml)

####戻り値有り関数
関数|内容
---|---
abs(a1)|a1の絶対値
max(a1,a2)|a1,a2で大きい方
min(a1,a2)|a1,a2で小さい方
strwidth(a1)|文字列a1を描画した時の幅
input()|入力ﾊﾞｯﾌｧから一文字読み込む.ﾊﾞｯﾌｧが空なら入力を待つ
input(a1)|input()の入力待ちがa1ﾐﾘ秒でﾀｲﾑｱｳﾄし0が返る
pow(a1,a2)|a1のa2乗
fact(a1)|a1の階乗
sin(a1),cos(a1),tan(a1)|角度はa1度.100倍した値を返す
strwidth(a1)|指定した文字列a1の幅を取得します。 
strlen(a1)|a1の文字列の長さ
stridx(a1,a2)|a1からa2を探して場所を返す.無いと-1
substr(a1,a2,a3)|文字列a1のa2番目からa3文字
strat(a1)|文字列のa1番目の文字を返す。最初の文字のインデックスは0からはじまる。
load()|プログラムのセーブ領域の値をロードして返す
imgwidth(a1)|画像a1の幅を取得します。
imgheight(a1)|画像a1の高さを取得します。
(http://satoo.jp/i/basic/ref05.shtml)

####予約変数
変数名|内容
---|---
tick|UTC 1970/1/1 00:00:00からのﾐﾘ秒
rand|ﾗﾝﾀﾞﾑな値(符号付)
width|画面の幅
height|画面の高さ
ascent|現在のフォントのアセント(ベースラインから上端までの長さ)を取得します。
descent|現在のフォントのディセント(ベースラインから下端までの長さ)を取得します。
strheight|フォントの高さを取得します。 この値はアセントとディセントの合計と等しくなります。
ampm|午前中はｾﾞﾛ,午後は1
date|現在の日付
dayofmonth|現在の日付 (dateと同じ) 
dayofweek|現在の曜日 (日曜日が1) 
hour|現在の時 (午前または午後の何時か) 
hourofday|現在の時 (24時間表記) 
millisecond|現在のﾐﾘ秒
minute|現在の分
month|現在の月
second|現在の秒
year|現在の年
scan|現在挿下されているｷｰｺｰﾄﾞ  
totalmemory|トータルヒープサイズを得る
freememory|空ヒープサイズを得る
(http://satoo.jp/i/basic/ref06.shtml)

キーコードは以下の通りです。

変数名|キー
---|---
key(key0等)|数字
keyup|上
keydown|下
keyleft|左
keyright|右
keyast|ｱｽﾀﾘｽ
keypound|#
keyselect|選択
keysoft1|左ｿﾌﾄ
keysoft2|右ｿﾌﾄ
(http://satoo.jp/i/basic/ref06.shtml)
##方針
携帯Basicの何よりの特徴は、とにかく遅い事です。
携帯BasicはJava上で構築されたインタープリターです。
ただでさえ遅い携帯電話の処理速度で、当時JITさえなかったJavaで、さらにBasicという言語を実装している関係上処理速度は大変遅くなります。
しかし、逆に言えば遅いのはBasicで書かれたプログラムの解釈・実行であってJava側・ネイティブコードで実装されている機能の実行はさほど遅くは有りません。
感覚で言えば、16bitコンピューターのBasic上より遅いくらいの感覚でしょうか。

他の制約として、携帯電話上でのプログラミングの関係上、文字のスクロールが遅いという問題もあります。
テキストエディタの種類にもよりますが、ファイル全体をテキストボックスで編集するタイプだととてつもなく遅くなります。
一方でスクロールは読み込みのみで、一画面分を編集するアプリだとかなり早くなります。
とはいっても目的の行を探すのは大変なので、行数を短く簡潔に、変数名も短く、コメントもつけない、という工夫が必要です。
これは実行速度にとっても有用な対策です。

以上から以下の様な方針が生まれました。
* 実行速度を最優先。行数が少なくなるようなプログラミングを心掛ける。
* 入力の手間を出来るだけ省く。変数名・ラベル名は簡単に。
* プログラム実行より文字処理は圧倒的に早い。文字処理に置き換えられる命令は文字処理でやる。
* コメントは打たない。他人は余り読まないし、それほど難しくはない。
* メモリは無限にある。解放は無用。
* gotoは使わない。例外はある。
* 再描画は抑える。と言うか不可能。

これらからいくつかのテクニックが生まれました。次に解説します。
##テクニック
携帯Basic特有と思われるテクニックを解説します。
###関数ポインタ
携帯Basicでは``gosub``・``goto``の引数は文字列です。そして、引数には実は変数が使えます。
つまり、それを使う事により関数ポインタのように使う事さえできるのです。
````
CommandList=":help:cd:type:"
if not(stridx(CommandList,":"+CommandName+":")=-1) then
tmp="Command_"+CommandName
gosub tmp

label Command_help
````
文字入力と組み合わせれば、簡単にCUIが作れます。
もちろん、同じことはIF文でもできますがこちらの方が圧倒的に簡潔で早いのです。
###三項演算子
携帯Basicでは真偽値のtrueは1、falseは0として扱われます。
それを使えば割と``if``文を省略できる場合が有ります。
````
maxnum=(a>=b)*a+(a<b)*b
````
これは以下と同じです。
````
if a>=b then maxnum=a else maxnum=b endif
````
上の方が簡潔です。
特に複数組み合わせると大きな差が生じます。
###while内でのend
携帯Basicではなぜか``while``内では``end``が出来ませんでした。その時は一度gotoで抜けてから``end``をすれば問題ありません。
````
while 1
gosub"keyCheck"
if pushedKey=keysoft2 then
goto"over"
endif
wend

label over
end
````
###連想配列
文字列処理の様な基本的な機能はJavaではなくネイティブコードで実装されています。
その為、携帯Basic上で処理を行うのに比べて文字列処理は異様に早く実行できます。
簡単な例は連想配列です。
````
stridx(dict,word)

````

###文字列処理の応用

````
label execPaint
len=0
tmp=paintList
color(0,0,0)
while not(tmp="")
cap=strat(tmp,0)
if cap="a" then
 arc(substr(tmp,2,3),substr(tmp,6,3),substr(tmp,10,3),substr(tmp,14,3))
len=18
elseif cap="b" then
 farc(substr(tmp,2,3),substr(tmp,6,3),substr(tmp,10,3),substr(tmp,14,3))
len=18
elseif cap="l" then
 line(substr(tmp,2,3),substr(tmp,6,3),substr(tmp,10,3),substr(tmp,14,3))
len=18
elseif cap="r" then
 rect(substr(tmp,2,3),substr(tmp,6,3),substr(tmp,10,3),substr(tmp,14,3))
len=18
elseif cap="s" then
 frect(substr(tmp,2,3),substr(tmp,6,3),substr(tmp,10,3),substr(tmp,14,3))
len=18
elseif cap="d" then
 clear(substr(tmp,2,3),substr(tmp,6,3),substr(tmp,10,3),substr(tmp,14,3))
len=18
elseif cap="c" then
 color(substr(tmp,2,3),substr(tmp,6,3),substr(tmp,10,3))
len=14
elseif cap="t" then
 text(substr(tmp,10,stridx(tmp,";")-10),substr(tmp,2,3),substr(tmp,6,3))
len=stridx(tmp,";")+1
endif
if strlen(tmp)>len then
tmp=substr(tmp,len,strlen(tmp)-len)
else
tmp=""
endif
wend
lastLen=len
return
````
