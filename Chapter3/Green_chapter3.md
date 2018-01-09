# 3.1 CVA and DVA: credit and debit valuation adjustment models
## 3.1 introduction
- Value adjustmentの定義

  $$
  \begin{equation}
  \hat{V} = V + U
  \end{equation}
  $$

  $\hat{V}$ は価格調整された価値, $V$ は価格調整まえの価値, $U$ が価格調整を表している. value adjustmentとしてCVAのみの計算だとすると, $U = \text{CVA}$ である.

- CVAの計算について
  - 取引レベルではなく,カウンターパーティーごとに行われる.
  - CVAの計算はnettingして行われる.
  - もし, nettingなしで, ここの取引ごとにCVAを出すと, CVA額を見積もりすぎる可能性がある.


- CVAと市場リスク管理との違い
  - 市場は資産クラス毎(商品毎)に管理されるが, CVAはカウンターパーティー毎で, かつ全ての商品を取り扱っているので, CVAデスクの方が市場リスク管理よりも複雑である.


- CVAの2つのモデル
  - unilateral modelとbilateral model
    - unilateralはcounter partyの信用リスクのみ考慮に入れる.
    - bilateralはcounter partyの信用リスクに加えて, 自社の信用リスクも考慮に入れたモデル. したがって, 自社のvalue adjustmentをDVA(debt value adjustment)とすると, 定義において
      $$
      U = \text{CVA} + \text{DVA}
      $$
      である. CVAはコストであり, DVAはベネフィットである. DVAはいわばカウンターパーティから見たときのCVAに相当するもので,相手から見たらコストとなるものは, 自社にとってはベネフィットである. CVAは勝ちポジションだとコストになるので, 相手が勝ちポジションということは, 相手のコストになり, つまりそれは自社のベネフィットとなる. コストはpositive exposureを用い, ベネフィットはnegative exposureを用いる.

## 3.1.1 Close-out and CVA

デフォルト時には損害賠償を請求することができ, SDA契約を結んで入ればその契約に基づき請求額が決定する. close-out額はEADに大きく影響するものであり, したがってCVAそのものに関わるため, 重要な取り決め事項である. 以下がclose-outの分類である.

- Risk-free close-out
  - もっとも単純なケースでcounter partの信用リスクを考慮しないもの。
- Risky close-out
  - すべてのvalue adjustmentを考慮に入れたデフォルト直前のポートフォリオのclose-outg額として定義されるもの. モデルが色々あって, 主にBurgard and Kajaerniによるもの．
- Replacement cost: DVA-only
  - CVA額は無視して，DVA額をclose-out額にするもの．
- Replacement coas: Funding costs
  - fundingコストを含めるもの(ポジションの再構築とかの話？)

Greenの本ではrisk-free close-outのみを考える．理由は，その他のclose-outについてはCVAの計算が複雑になってしまうためである．
