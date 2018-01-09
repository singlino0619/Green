# CHAPTER 4 CDS and Default Probabilities
## 4.1 Survival Probabilities and CVA
Survival probabilities(生存確率)はCVAの計算の中心を担うものであり，本章ではこの関数について詳しく取り扱う．
以下，本節の簡単な概要である．
- CVA計算において，生存確率はCDSスプレッドより得る事ができる．
- 過去の計算ではヒストリカル(実確率)の生存確率を用いてきた．
- 現在では，ヒストリカルとマーケットインプライの生存確率のどちらを用いるかについて状況により選んでいて，それぞれでメリットデメリットがある．これらについては4.2節で詳しく述べられる．
- CDSのプライシングモデルについては4.3節で紹介される．
- ブートストラップ法を用いて生存確率関数を導出する方法があり，これについては4.4節で述べられる．モデルは複雑なのであまりCVAのプライシングには用いられない．
- バーゼルIIIの規制によれば，CDSをCVAのヘッジに用いて規制資本の計算を行うことになっている．4.5節で詳しく紹介される．

ハザードレート $\lambda{(t)}$ がポワソン過程に従ったデフォルト過程のモデルを考える．このとき，生存確率は次のように与えられる．
$$
P(\tau > T) = \exp{(-\int^{T}_{t}\lambda(s)ds)}．

$$
この生存確率を用いると，デフォルト確率は確率１から生存確率を引けば良く，デフォルト時刻を $\tau (< T)$ とすると，
$$
P(\tau \leq T) = 1 - \exp{(-\int^{T}_{t}\lambda(s)ds)}
$$

## 4.2 Historical Versus Implied Survival Probabilities
- これまでの信用リスクの評価
  - 個々のCPに対してPD(Probability of default)モデルを適用
  - バーゼルIIの規制の下で，FIRB(Foundation internal ratings based approach)を承認された銀行については，独自のPDモデルを用いていた
  - 独自のPDモデルはヒストリカルデフォルトレートを用いていて，そのレートについては各社において経験的にあたえられるものであった．
  - したがって，格付けには上記のようないわゆる内部格付けと，格付け会社による外部格付けが存在する．

- CVAプライシングとの関わり
  - ヒストリカルの確率を用いている会社も存在する
  - しかしながら現在のマーケット慣行では，CDSスプレッドからインプライされたrisk neutralなPDを用いてCVAのプライシングを行うの通例となっている．

- risk neutralのPDが慣行となっている3つの理由
  - CVAはデリバティブの評価調整であり，デリバティブのプライシング自体はリスクニュートラルで行われるため．つまり，デリバティブのプライシングとconsistentにするため．
  - そもそものCVAを評価する目的は，自身のポートフォリオに孕むcredit riskを把握して，リスクヘッジしようというものであった．リスクニュートラルなインプライドPDであればCDSを用いてcredit riskをヘッジすることができるため．
  - バーゼルIIIの規制の枠組みにおいて，CVAの規制資本計算にCDSを使う事とかいてあるから．

## 4.3 CREDIT default Swap Valuation
### 4.3.1 Credit default Swap
CDSのキャッシュフロー
- premium legとdefault legの二つがある
- premium legはprotectionの買い手が売り手に支払う方向に向いており，参照債務(reference obiligation)がデフォルト，あるいはデフォルトせずにCDSの満期を迎えるまで支払う．
- default legはprotectionの売り手が買い手に支払う方向であり，参照債務がデフォルトした時に支払う．

CDSのトレーディングについて
- 利息は買い手から売り手に払われる
- 決済はbond or cash.
-

Market standardについて
- CDSの取引は4ヶ月ごとのIMM月の20日に終わる.
- CDS marketはIRS marketの市場慣行とは違っている．IRSはテナーや日にちがdailyで変化する．

Restructuring Calusesについて
- クレジットイベント(デフォルト)の定義を定めたもの.

ISDA Big Bang and Small Bang Protocolsについて
- 2009年，ISDAがCDSのmarket conventionを変えた時の２つの条項

## 4.4 Bootstraping the survival probability function
クォートされているCDS spread
- 6M, 1Y, 2Y, 3Y, 4Y, 5Y, 7Y, 10Y, 20Y, 30Y
- これらのCDS spreadをinputとして用いればbootstrabingによりsurvival Probabilityを求めることができる.
- 次のCDS評価式を用いることでbootstrapを行える(swap pricingの式から
  DFをbootstrapするのと似ている)
$$
V_{\text{CDS}} = V_{\text{prem}} + V_{\text{accured}} -
V_{\text{prot}}
$$

具体的なbootstrapingのイメージ
- survaival probabilityは次のように与えられる時
$$
P(\tau > T) = \exp(- \int_{s=0}^{T}\lambda(s) ds)
$$
- ハザードレートの形を仮定することでsurvival probabilityを求めることができる．ハザードレートの形を指定すれば，あとはCDSの価値をゼロにするような
等式をNewton-Raphson法などで解いてsurvival probabilityを求めることができる.仮定する形は次の3つが代表的

  - piecewise constant
  - piecewise linear
  - cubic spline

- piecewise constantの仮定がもっとも用いられいる．
  - 階段関数なので数値的に扱いやすい．挙動が安定している
  - 市場観測されている値同士の最も単純な仮定である(例えば,
    0-6Mは6MのCDSの値, 6M-1Yは1YのCDSの値等)
  - 20th of the IMMに関連しているらしいが...

ハザードレートを定数にする期間の選び方
- 基本的にはCDS spreadがクォートされている期間の間を定数とする
- 0-6M, 6M-1Y, 1Y-2Y, ...などのようにこの間をそれぞれ定数とする．

解き方
- ハザードレートを上記のように仮定したら，4.15式で$V_{CDS}$ を0にした式を
Newton-Raphson法などでとく．

テーブルと図の例
- 表4.1にはCDS spreadの例
- 例えば，0-6Mは46bp, 6M-1Yは52bpを用いて，bootstrappingを行う．
- 図4.2がbootstrappingで求めたHazard rateの例.

#### piecewise linearを仮定する方法について
##### 概要
- 連続関数であることが利点
- CDS spreadのセグメントはpiecewise constantの時と同じようにやる.
- アカデミックで研究されているが，実務ではpiecewise constantが使われている．

##### 問題点
- 解が不安定(Newton-Raphsonが安定しない?)
- survival probablityが負になってしまう．

#### cubic splineを用いる方法について
##### 概要
- yeild curveのbootstrapping法では3次補間が用いられているけど，credit curveの構築ではあまり用いられていない.
- 一番の利点は，瞬間的なデフォルト確率とみなせる，ハザードレートが滑らかな連続関数になること．
- ある年限のswap rateがシフトすると，カーブ全体に影響するので，直感的ではないリスクが出てきてしまう恐れがある．
- CDS トレーダーはロール中のhazard rateそのものを知ることができないので(CDS　spreadはあるが)，あっているかどうか
わからない．それを使うぐらいなら，定数と思っていた方がよいということ?


### 4.4.1 Upfront payment
- マーケットクォートされているCDS spreadはCDSをparにする取引であるはず
- ディーラーはcredit eventが認識されるようになると，プライスを高めにつけるはずで，さらに期中のpaymentも高めに出すはずである．

### 4.4.2 Choice of Hazard rate function adn CVA: CVA carry
- CVAはポートフォリオベースで計算されるので，キャシュフローに大きく依存する
- なのでCVAの計算においてハザードレートの仮定や，どの期間をsegmentとするかなどはCVAに大きな影響を与える.
- CDS rollの少し前の日をsegmentとするか，CDS rollの翌営後(business day)をsegmentとする場合に
ハザードレートが少し異なる.(図4.3)

### 4.4.3 Calibration problem
#### piecewise constantの仮定におけるCalibrationの問題点
- ハザードレートがnegativeになる
- 長期のCDS spreadは流動性があまりなく，spreadが大きめに出る．したがって長期の比較的大きめのCDS spreadの値が
キャリブレーションがうまくいかない原因になっている．
- この問題の解決策は，CDS spreadの値を調節することである．
- 次のsegmentのCDS spreadの範囲を予測することができる

- 長期のCDS spreadは流動性があまりなく，spreadも高めにでている
- キャリブレーションがうまくいかない原因になっている．
- 長期のCDS spreadの値を前のsegmentの値から推計して，カーブを引くという方法を解決策としている

n番目のCDS spreadを用いたキャリブレーションの例
- 前提
  - n個のCDS spreadがクォートされており，n-1個目までのsurvival functionはn-1個のCDS spreadを用いて求められているとする．
  - accuredは簡単のため0とする

- n番目のCDSのparの価値は次のように計算される
  $$
  0 = V_{\text{CDS}}^{n}(t_{0})=V_{\text{prem}}^{n}(t_{0}) -
  V_{\text{prot}}^{n}(t_{0})
  $$

- $V_{\text{prot}}^{n}(t_{0})$
は時間を
  $$t_{0} = u_{0} < ... < u_{\alpha} < ... <u_{\hat{A}}=t_{n-1}<...<u_{A}=t_{n}$$
  と分割して教科書のようにかける．

- $V_{\text{prem}}^{n}(t_{0})$ も同様に時間を分割

- n番目のCDS spread $s_{n}$ については，$\lambda_{0} \rightarrow 0$の極限で$s_{\text{min}}$ を求める．この極限は"デフォルト"しないことに対応している.
  $$
  s_{n} > s_{\text{min}} = \frac{V_{\text{prot}}^{n-1}}
  {\frac{1}{s_{n-1}}V_{\text{prem}}^{n-1} +
  P(\tau > t_{n-1})\sum_{b=\hat{B}}^{B}\alpha_{i}B(t_{0},v_{b})}
  $$
  $s_n$と$s_{min}$ の間を使って，キャリブレーションが落ちないようにCDS spreadの値を調節する．

## 4.5 CDS and Capital relief
CDSは参照債券のデフォルト時の保険に用いられるだけでなく，CVAのヘッジにも用いられる．

##### バーゼルIIIの元ではCVAのヘッジによって自己資本額を減らせると定められている
- 自己資本額の緩和がヘッジによって許されているならば，CDSのプライシングにおいてもその効果を取り入れるべきである．

##### 難しさ
- すべての企業についてsingle name CDSがあるわけではない
- CDSをヘッジの方法は銀行毎にモデルが異なるので，すべて同じbenefitを得られるわけではない．
- 理論的には，マーケット参加者同士ごとに異なる資本軽減の方法があるので，それがOTC CDSに対し，異なる値の
プライシングを生み出してしまう．

##### 資本軽減が示唆していること・もしCDSに資本軽減効果を取り入れた場合
- CDSのvalueはCDSのプライシングモデルの中にcapital protectionのlegを導入することで,
資本軽減の効果を反映すべきである．
- そのモデルを用いることで，資本軽減効果を反映したハザードレートが算出され，CDS spreadとして，
資本削減効果を反映した値がクォートされるようになる．


自己資本額軽減について
1. ヘッジを考慮したCDSのプライシングにより，ヘッジを考慮したhazard rate が算出
2. その値を用いてCVAを計算するので，CVA額が小さくなる
3. そのCVAを用いてRWAを計算するので，結果的に資本の軽減につながる

効果
- Kenyon and Greenの論文によると20%-50%ほど緩和できる

## 4.6 liquid and illiquid counterparties
デリバティブが優先無担保債務との優先順位付けを行う通常の場合、CVAはカウンターパーティーのCDSスプレッドを用いて表示される

- senior debt: シニア債とよばれる．証券化商品などで債券をリスク度合いで３つに分類したときに，最も格付けの高い低リスクのものをいう．

- singlenameのCDSが存在する先については，CDS spreadがクォートされている値を用いて理論的にはヘッジ可能である．

#### 流動性のない企業に対してのcredit curveをどう引くか
##### 背景
- マーケットクォートされているのは全世界ベースでみても3000社ぐらいなので，銀行が取引しているcounterpartyの中でCDSが
存在するものは数少ない．
- 流動性のある会社の債券を参考にCDSの値がわかればよいが，そうではない限り，代表的なCDSカーブを作って，それを流動性のない会社にマッピングする作業が必要になる
- 実際の会社のCDSを参照しているわけではないので，mappingの仕方によってリスクの大きさも異なる．
このリスクは"warehoused"と呼ばれている？

##### バーゼルIIIでの条件
- mappingの方法については，各銀行が勝手にロジックを持って良いけど，監査を通らないといけないとなっていたが...
- バーゼルIIIでは，IMMの承認を得るために，credit curve のマッピング方法に条件が課せられた．
- BarselIIではmappingの方法として,illiquidのcounterparyについては3つの項目で分類されるべきと書いている
  - industry sector(産業)
  - rating(格付け)
  - geography(地域:Asia, America, Europeとか)
- 銀行にとっては，これらの要因が利用できる最小の分類である

##### コメント  
- これらの要因には問題もある．
- アメリカはCDSの流動性が，他の地域に比べると多い国である
- したがって，アメリカの地域については上記の分類を多くできる(サンプルが多い：様々な産業について，どの格付けがつけられているのか
  がわかる．その産業，その格付けの企業についてカーブを引くことができ，他の地域よりも多くカーブを引くことができる．)
- その意味では，ある程度market impliedのcurveを多く引くことができる．
- アメリカ以外の地域では，なかなかCDSの流動性がないので，mappingに苦労する．
- かといって，地域を無視すると，似たような産業，似たような格付けの会社をUS CDSから探さなければいけないので
これも大変である．


### 4.6.1 Mapping to representative CDS
#### mappingの方法の一つ
##### 別の企業のsingle name CDSをilliquidの会社にそのまま適用する方法
- 理想的には，似たような信用力があり，似たようなセクターで同じ地域であることが望ましい
- けど，それは難しい．
- 利点は何かというと，single nameは流動性があるので，すぐに取引可能である.
- また，mappingの選択が適当なら流動性のない企業にたいしてcredit riskを把握することができるようになる．

##### この方法をとることの問題点
- illiquid nameのCDSはliquid nameに連動することで，問題が生じる．
  - 例えば，illiquid nameと共通しない特異な性質をliquid nameが持っていたとすると，
  それにより片方だけCDS spreadがwideningすべきなのに，両方wideningしていまう現象がおこる.(逆も然り)

以下，liquid nameをAとし，illiquid nameをBと表記する．  
カウンタパーティBのデリバティブ取引から生じるCVAのヘッジについて，AのCDS契約を用いている場合に起こりうること
- AがデフォルトしBがデフォルトしない時
  - CDS契約は清算される.
  - CVAデスクは結果として，棚ぼた利益を得られる．
  - Bのヘッジを別の方法で補わなければいけない．
- BがデフォルトしてAがデフォルトしない時
  - CDS契約は清算されない．
  - CVAデスクは損失を被る

### 4.6.2 Mapping to Baskets and Indices
