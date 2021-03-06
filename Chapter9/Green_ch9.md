# Funding Costs: Funding Valuation Adjustment(FVA)
## Explaining funding costs
1.3.5, 1.4.1節でFVAについて少し触れたが，この章ではより詳しくFVAについて説明．
- 主に無担保のデリバティブ取引を例にとって，FVAを説明．
- その他，initial marginなどもFVAの対象になるが，それはchapter 10で説明．

この章の主な目的
- FVA(調達に関わるコストやベネフィット)が存在することを理解する
- FVAの定義式がCVAの定義式を導出した場合と一貫していることの理解．

FVAのmodelは何が適切であるか(どう言う文脈で定義すれば良いか)
- valuationの種類(valuationの目的)に関係する.
- trading(pricing), accounting, regulatoryの3つがある．
- この章ではtrading valuation modelでのFVAを考える．（通常これ？）
- FVAをモデル化した時のaccountingとregulatoryへの影響についてはChap. 11で議論

### 9.1.1 what is FVA
一般的になされるFVAの説明の例があり，それらは以下の4つ．
- effective loans and deposits
- cost(benefit) of collateral on market risk hedges
- no repo market for derivatives
- cost(benefit) of not having a CSA

#### Effective loans and deposits: ローンや預金のデリバティブ版を考えることで，FVAのコストやベネフィットを理解する

デリバ取引のファンディングを最も理解するのに良い例  
それぞれの対応関係は
- ローン : funding cost
- 預金 : funding benefit

##### どういうことか
まずローンとはについて考える
ローンのプライス:顧客にチャージする部分は大きく分けて2つ
1. 銀行の資金貸し出しに対するコスト（調達コスト）
1. 顧客のクレジットスプレッドに上乗せ

>1について: (顧客にお金を貸し出すためのお金を)市場から借りてきたり、ほかの銀行から借りてきたりするときのコスト．

>2について: 貸し出した顧客はデフォルトリスクがあるので，格付けに応じて金利水準を決める．

逆に預金は
1. お金を貸し出すので，funding benefitとなる(調達に関わって利益を得られる)

##### Figureで比較:デリバのエクスポージャーの例  
- Fig. 9.1: in the moneyの取引の図
- Fig. 9.3: out of the moneyの取引の図
- $100mの想定元本で5%の固定金利をもらう(9.1)で，1%の固定金利をもらう(9.3)

Fig. 9.2と9.4はローンと預金のエクスポージャー(元本のスケールはデリバの図と合わせている)

##### 図からわかること
- in the moneyのエクスポージャーはローンのエクスポージャーと似ている．
- ローンと同じように相手が勝ちポジションなので，資金を支払う調達コストがかかったり，クレジットスプレッドを上乗せすべき
- out of the moneyの場合は預金のエクスポージャーと類似
- 預金と同じように相手が負けポジションなので，調達コストなどは考えなくて良い．

##### 注意点
- 厳密にはデリバ自体はEPEもENEもあるのでcostもbenefitも両方ある

#### マーケットリスクのヘッジに対する担保のコスト

##### 言いたいことのまとめ
- CSA契約が非対称だと、funding cost(benefit)の考え方が生まれる

##### どういうことか
- 想定すること：back-to-backの取引を考える  
- この場合双方にクレジットリスク、ファンディングコスト、資本などがなければ完全にエクスポージャーは打ち消しあい、リスクヘッジされる.
- CSA契約非対称を考える前に対称を考える

##### CSA契約ありの場合
仮定:
1. 双方同じCSA契約
1. すぐに担保の差し出し
1. No MTA and Threshold

取引の際の担保のやりとりの例  
- 取引相手が勝っているとき、取引相手が自行に担保を差し出す
- 同時に、反対取引は自行の勝ちポジションになるので、CSA契約が全く同じ場合、同じ担保額をインターバンクに差し出す
- リハイポが認められているなら、差し出された額そのものをインターバンクに差し出せば良い.
- この場合ファンディングコストはないことがわかる

##### CSA契約ない場合
仮定
1. 反対取引を行うインターバンクCとはCSAはある
2. 事業法人Aとの取引相手とはCSA契約がない

取引例  
- Aのポジョンが勝っているとき(Bは負けポジション)でも、Bに担保は差し出さなくて良い．
- 一方でヘッジの反対取引はBから見て勝ちポジョンとなっているので、担保を差し出す必要がある．
- この場合、市場からそのための資金を調達しなければいけなくなる．
- リハイポできない場合funding costがかかる．

##### 注意点
- 余剰担保の部分はリハイポできるなら、担保として再利用できるので、funding benefitとなる

#####

##### No repo market for derivative

> レポ取引:債券などを一定の条件付で買い戻したり、売りつけたりする取引
債券を貸し出す代わりに現金をもらい、ある一定期間後に、その逆の取引を行う。主に資産運用の目的で行う。債券の貸し手は受け取った現金に対して金利を払う。調達コストがレポレートになる。(担保金利-債券貸借率)

債権のレポ取引 = 担保付きローンの一種とみなせる
- ある合意した時点で、合意した額を返却する取引

資金調達をしたい場合(債券を買いたい時)
- レポ取引で自分の持っている債券を貸して，資金を調達する

債券を借りたい場合
- 目的：担保に使いたい
- 逆のレポ取引を行い，債券を借りる．

##### 言いたいこと
- レポ取引を行うことでいつでも債券を借りたり貸したりできる
- 債券をもっていれば，fundingコストはかからない．

一方でデリバティブには、レポ取引に相当するものがない
- デリバティブの貸し借りでfundingできない
- レポマーケットがあればFVAをゼロにすることができる(9.4.1でやる) ??
- 理想的にはrepo取引のデリバ版があればよいけど，そんな市場はできなさそうである．
- 債券市場がレポ取引できるのは，十分な流動性のある資産であるから．
  - すぐに貸手に対して借りてが見つかったり，その逆であることが必要な市場

##### 言いたいこと
- デリバ取引にはレポ市場がないので，funding costがかかる

##### CSA契約がないことによるコスト(ベネフィット)

##### つらつらと言うだけ
CSA契約は調達コストとカウンターパーティリスクを軽減している

- リハイポできれば、FVAは無くなる
- ということは、無担保デリバのFVAはCSAを結んでいないことによるコストとみなせる（CSAにリハイポOKと書いていれば）
- つまるところ、CSA契約は調達コストとカウンターパーティリスクを軽減している
- ただ、事法に対してはCSA契約は結ばないので，ビジネスをやる上では，銀行のfundingコストが乗るのは避けられない

調達コストの一般的な原理
1. リハイポできない場合に、担保資金を調達しなければいけない時
2.
