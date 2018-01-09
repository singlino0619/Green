## 6.1 Credit mitigants
クレジットリスクを軽減する方法について，具体的にCVAモデルにどのように組み込まれるのかを学ぶ．
クレジットリスクの軽減は4つあり，
- 一括清算(close out netting)
- 中途解約条項(break clauses)
- CSA担保(collateral)
- 不動産等(non-financial security)

## 6.2 Close out netting
一括清算の方法はクレジットリスク軽減の方法の中でももっとも重要であり，もっともシンプルなものである．
CVAやDVAのモデルのなかに簡単に組み込むことができる(ある条件をのぞけば).
#### unilateral CVAについて
$$
\text{CVA}(t) = E\left[ (1-R)(V(\tau))^{+} | \mathcal{F}_{t}\right]
$$
の式で与えられ，$\tau$はデフォルト時刻，$V_t$ポートフォリオベースの取引の一括清算の値をあらわす．
すなわち，
$$
V(t) = \sum_{i=1}^{n}V_{i}(t)
$$
であり，添え字$i$が(信用リスクを加味していない)取引を表している．
一括清算がありの場合となしの場合のCVAはそれぞれ，
$$
\text{CVA}^{\text{netted}}(t) = E\Big[ (1-R)\text{max}\Big( \sum_{i=1}^{n} V^{i}(\tau), 0 \Big) |
\mathcal{F}_{t} \Big],
$$
$$
\text{CVA}^{\text{non-netted}}(t) = E\Big[ (1-R) \sum_{i=1}^{n} \text{max} (V^{i}(\tau), 0) |
\mathcal{F}_{t} \Big]
$$
である．一括清算してもよい取引は決まっており，これをnetting setと呼ぶ．netting set間の一括清算は
認められていない．netting setのCVAは, $j$の添え字netting setの番号とすると($j=1,...,m$),
$$
\text{CVA}^{\text{netting set}}(t) = E\Big[ (1-R) \sum_{j=1}^{m} \Big( \sum_{i=1}^{n_{j}} \text{max} (V^{ij}(\tau), 0)
\Big) | \mathcal{F}_{t} \Big]
$$
である．
#### bilateral CVAについて
unilateralと同じように考えればよい．
unilateralの場合と異なる点で重要な点は，nettingを
行ったからといって必ずしも信用リスクを軽減するわけではないということである．
BCVAの場合，当行負けポジションの分もプラスのCVAとして計算をしてしまうので，BCVAの場合，nettingをしても
軽減されないことがある．
