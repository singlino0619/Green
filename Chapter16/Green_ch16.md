# 16.2 Choosing the calibration: Historical versus Implied
- モンテカルロの実装で，キャリブレーション方法の選択は初めに考えることである
- 4.2節では，default probabilityをヒストリカルとインプライドの両方のキャリブレーション方法を示した．
- どちらのキャリブレーション方法がエクスポージャー計算で用いるモンテカルロシミュレーションに適しているのかは議論すべき問題である．

## 16.2.1 The case for Historical Calibration
1st sentence
- キャリブレーションをすべき項はボラティリティ項とドリフト項に分けられる
- ヒストリカル: 時系列データから得られるボラティリティ、ドリフトから推計する

2nd sentence
- 信用リスクの管理でPFEの計算時にヒストリカルキャリブレーションを使っているから、その名残でCVA計算のモデルにも使っている。
- フルのインプライドモデルは比較的複雑

3rd sentence
- ヘッジを全くしないのであれば、ヘッジ対象に
- CVAはポートフォリオでの、デフォルトリスクを加味した将来の期待損失
- FVAはポートフォリオの将来の資金調達コスト

4th sentence
- いくつかのバンクはヒストリカルキャリブレーションモデルをもちいているが、多くはモンテカルロモデルではリスクニュートラルでキャリブレーションしている
- IMM承認を得るためには、Unilateral modelではリスク中立のデフォルト確率を使うべきである
- エクスポージャー自体は，CCRのEADを計算するのに使われるエクスポージャーモデルから計算されるべきである．
- エクスポージャーモデル自体は，バックテストが通っていて，リスク中立やヒストリカルキャリブレーションの選好性がないことが求められる
- 承認のプロセスの本質(何をクリアすれば承認されるか)が与えられれば，多くの銀行は資本規制に関わるCCRやCVAの計算をするのに，ヒストリカルキャリブレーションを用いる．
- 一方で，XVAのトレーディング部隊はリスク中立のモンテカルロモデルを用いて，プライスを出したり，リスク管理したり，CVAを計算したりする．

5th sentence
- 理論的には...


#### Histroical Interest Rate Calibration
1st sentence
- credit exposureモデルにおいて，金利の計算に使われる典型的なモデルがHull-Whiteモデルである
- $\theta(t)$:mean-reversion levelで，回帰先の水準，$\alpha(t)$:mean-reversionで回帰の強さ,$\sigma(t)$ がボラティリティ．
- ヒストリカルキャリブをする際の疑問点
    - ヒストリカルデータに全てのパラメータをキャリブレーションすべきか
    - $\theta(t)$　に関しては初期の期間構造にキャリブレーションすることによって，リスク中立でキャリブレーションされたパラメータを残すかどうか．(リスク中立モデルだと，初期の回帰先の水準はディスカウントファクターでキャリブレーションできる．)

2nd sentence
- リスク中立のドリフトの形は，16.2式のようになる
- その時点の初期の金利の期間構造にフィッティングしている
- $\theta(t)$ を得るためには瞬間的なforward rateが微分可能な滑らかな関数であることが必要である．(Hull-Whiteに特有？？)

3rd sentence
- volatilityパラメータは時系列データからキャリブレーションする
- 方法の一つとして,James and Webber(2000)に書かれている，general method of moments(GMM)がある
- キャリブレーションをするために，少しモデルを変形していく必要がある

__流れ__
- 変数変換
    - $x(t) = r(t) - \phi(t)$
    - $\phi(t)$ は$dx(t)$ がOU過程になるように選ばれている
    - OU過程は　$dx(t) = -\alpha(t) x(t) dt + \sigma(t) dW(t)$ なので
    - $( \theta(t) - \alpha(t) \phi(t)) dt - d\phi(t) = 0$　を満たすように$\phi(t)$が決まっている    
    - $\theta(t)$ がリスク中立の初期の金利構造でキャリブレーションされれば$r(t)$　の形は16.8式のようになる．

- GMMアプローチ
    - 16.7式と16.8式を離散化する．
    -

last sentence
- $\theta(t)$ が定数のときは，今の足元の金利でプライシングを行うということであり，モデル自体は将来の金利変動をモデル化していることにはなっていない
- mean reversion levelはキャリブレーション期間の選択によって値が変わりやすい．
- 二つのボラももちろん期間の長さの選択に敏感であるが，もし初めの金利構造にマッチしているのでれば，そこまで影響はない
- なのでキャリブレーションの期間の長さの選択は重要である．
- windowはおそらく，キャリブレーションの期間の長さのこと
- 長い期間のキャリブレーションはボラティリティの局所的な変化を弱らせる
    - まぶされてトレンドがでてこない
- 一方で，短い期間のキャリブレーションはそれらを強く反映させる．
    - トレンドが大きく反映される



#### Historical FX Calibration
本節で扱うモデル: 対数正規モデル  
$X(t)$ を為替レート，$\sigma_X(t)$ をボラティリティ，$W(t)$ をウィーナー過程とすると，対数正規モデルは次のように表される．
$$
dX(t) = \mu(t) X(t) dt + \sigma_X(t) X(t) dW(t)
$$

1st sentence
- ボラティリティのキャリブレーションをどうするかが初めに挙がる疑問である．
- もっとも単純な仮定はボラテリティを定数とすること
    - キャリブレーション期間を決めて，スポット為替レートから得られるログリターンの分散を取ることヒストリカルキャリブレーションできる．
    - 年率ボラティリティに直すために$N_{\text{trading}}$ をかける
    - キャリブレーションの期間の選択によって，現在から近い期間の値を反映させるか，遠くの期間の値を反映させるかがことなってくる．
    - マーケットのヒストリカルを用いているので，ボラティリティの振る舞いは反映している
    - 一方でヒストリカルキャリブレーションではボラのボラは反映されていない

2nd sentence
-

3rd sentence
- ドリフト項は長期のFXレートの振る舞いに関わってくるので，長期のFXレートを見る場合ドリフト項の選択は重要である．
- ドリフト項が定数であるとした場合
    - ログリータンの平均で得られる．
##### このアプローチの問題点
- クレジットリスクのシミュレーションの時にみられるように(リスクファクターの観測が市場のリスクファクターよりも長期間)，極端なFXの動きを反映することである
- 15年がなにかわからないが．．．
- キャリブレーション期間は1-3年に設定することが多く，中央銀行などが貨幣の価値を下げた結果として現れる，強いドリフト効果を見ることは不可能ではない．(あまりまぶされずに，直近のドリフト効果がみれる)
- ただ，あまりうまく行かない場合がほとんどである
    - 急なジャンプとかには対応できない
    - ドリフトが30年のキャリブレーションで$0.0001と推計されたとする
    - シミュレーション時のスポットは$1.57であるが
    - $1.98 to $1.37の変化は表現できない
    - $1.57を中心にモンテカルロでシミュレーションされてしまうので，極端なケースを表現することができない．
    - なので，ヒストリカルの期間構造をいれれば，期中の動きをある程度コントロールすることができる．