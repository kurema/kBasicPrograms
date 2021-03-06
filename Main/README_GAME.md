#ゲームについて

##ゲームは
数当て・バトルシップ・マインスイーパ・擬似ナンバープレースがあります。

##メニューについて
通常メニューまたは数字指定方式です。
番号を入力しセレクトキーを押します。
番号表示は下端です。

##遊び方
###数当て
起動すると
> New. Less XXX.（XXXは数字）

と表示されます。これはXXXより小さな数字ですよ、という意味です。  
それより小さな数字が答えです。  
これが答えだ、と思った数字を入力して下さい。  
大きい、なら入力した数字が大きすぎる。  
小さい、なら入力した数字が小さすぎる。  
という意味です。  
当たれば「正解  YYY」（YYYは答えです）という、ダイアログが出ます。  
一桁ずつ絞り込むのがコツです。  

###マインスイーパ
適当に押して出た数字が周り八マスに有る地雷の数です。  
左下の数字 (XX/YY) でXXは埋めた数、YYは地雷でないマスの数です。  
マスは10×10。変更可能。

###バトルシップ
意外と知られていない傑作ボードゲームです。  
4,3,2,2の長さの船を配置し、同様に配置された敵の船を叩くゲームです。  
先に全部沈めた方が勝ちです。  
敵も案外強いです。  
色で内容が違います。  
青:味方の船 黄色:攻撃を受けた味方の船 緑:味方の攻撃（外れ） 赤:味方の攻撃（当たり） 水色:敵の攻撃（外れ）  
コツは、
* 船は互いに二マス空けて配置する。
* 攻撃は、間隔を空けてする。  
（残りの船が2の長さなら一マス毎、3,4なら2,3）
くらいです。

###ナンバープレースもどき
皆様おなじみの数独です。  
答に辿り着ける保証がありません。答え合わせ機能も有りません。  

選択後
数字で数字入力。
*（アスタリスク）でカンニング。
右ソフトキーで数字で固定数字入力。
（自分でうつす時等）


##設定について
###マインスイーパ難易度設定  
マインスイーパの難しさです。  
少ないほど難。地雷の数が増えます。  
レベルXの時地雷数平均100/X+2です。  

###アシスト機能
マインスイーパむけ。  
零がでたときの反応です。

番号 | 内容
---  | ---
0    | 何も無し
1    | 周り八マスのみ
2    | 繋がってる部分全て（時間がかかります。）

###選択方法
座標指定かカーソル指定か

番号 | 内容
---  | ---
0|座標指定（チェック機能不可）
1|カーソル指定

###チェック機能 色数
チェック機能の色数です。

番号 | 内容
---  | ---
0|無効
1-6|色の数

###結果表示
ダイアログ表示の設定です。

番号 | 内容
---  | ---
0|マインスイーパで終了後表示無し
1|通常表示
2|忘れましたが何か問題のある選択肢だったと思います

###フォントサイズ
二回ダイアログが出ます。  
一回目は、通常画面、つまりメニューと数当てです。
二回目は、マインスイーパとバトルシップです。
0-3 フォントサイズ

番号 | 内容
---  | ---
0|極小
1|小
2|中
3|大
2 3 にするとチェック機能で文字の一部と重なる仕様があります。
VGA画面等特殊仕様向けに作ったメニューです。

###マインスイーパサイズ
マインスイーパの盤のサイズです。
実質的なものは5から25くらいまで
2-99 マインスイーパサイズ。XX*XXのサイズになります。
10で無いときは座標指定はカーソル操作にしてください。

###カラーパターン
画面カラー設定

番号 | 内容
---  | ---
0| 定番黒白パターン
1| 液晶のイメージ
2| 白黒パターン
3| 灰色パターン
4| 純色パターン
5| 黒板パターン
6| 黒緑パターン
設定によって、バトルシップの色が見にくくなったりします。

###再描画機能
マインスイーパ時にカーソル移動したとき、数字をもう一度書き込むかです。
マインスイーパサイズ設定時に自動設定されます。

番号 | 内容
---  | ---
0|off
1|on

###NP数
ナンバープレースの表示される数の数（大体）を設定します。
正確ではありません

番号 | 内容
---  | ---
0|オフ
1-99|ナンバープレース数
