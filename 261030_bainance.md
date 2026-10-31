# Binance

[grok]

```
Binanceのハッカー、私が見てきた中でもトップクラスに頭いい動きをしたかも

まずTetherが$1.5B分のUSDTを凍結
続けてCircleも$800M分のUSDCを凍結
これで資金は詰んだと誰もが思ってた

でもハッカーはそれも想定済みだったらしい
盗んだUSDTをウォレットに置かずAaveに預けて、それを担保にETHを借りてそのまま消えた

Tetherが凍結できるのはUSDTだけ
すでに借りられたETHは凍結できない

結果、Aaveに残ったのは凍結された担保、ハッカーの手元には自由に動かせるETH
プロトコル側が回収できなければ、借りたETHを返す必要すらないかも

2社が$2B超を一瞬で凍結したのに、DeFiの仕組みを理解してた1人がその両方をすり抜けたかもしれない
冷静に考えるとヤバすぎる、、、
```

```
The Binance hacker might have just pulled off one of the smartest moves I’ve seen in crypto.

First, Tether froze $1.5 billion in USDT.

Then Circle froze another $800 million in USDC.

At that point, it looked like the hacker’s money was trapped.

But apparently, he had already planned for that.

Instead of holding the stolen USDT in a wallet, he allegedly deposited it into Aave and used it as collateral to borrow ETH.

Then he walked away.

That’s where the story gets crazy.

Tether can freeze the USDT sitting in the wallet.

But it can’t freeze the ETH he already borrowed.

So now Aave is left holding frozen collateral, while the hacker is sitting on liquid ETH.

And unless the protocol can recover it somehow, he may not even need to pay the loan back.

Two companies froze billions of dollars in seconds.

But someone who understood how to use DeFi may have found a way around both of them.

Pretty insane when you think about it.
```

- このポストは2026年10月29-30日のBinance大規模流出事件（推定数十億ドル規模）を分析し、ハッカーがTetherの1.5B USDT凍結とCircleの800M USDC凍結を事前に想定した動きを評価している。
- ハッカーは盗んだUSDTをAaveに預け入れて担保とし、凍結不能なETHを借りて逃亡したため、Tetherの凍結対象外となりAaveには凍結担保だけが残る形になった。
- DeFiプロトコルの仕組みを活用したこの戦略は、ステーブルコイン発行者の中央集権的制御の限界を露呈し、迅速な資産移動の難しさを示す事例となった。


```
同じようなポストはあるか？
```

はい、たくさんあります。元の@akina_koinjpさんのポストは、英語圏でかなりバズった投稿のほぼ直訳・要約版です。

### 最も似ている人気ポスト（元ネタに近いもの）

**@cryptoblaney** の投稿（約9500いいね超）  
内容がほぼ同じで、「smartest moves I’ve seen in crypto」と表現し、Tetherの1.5B USDT凍結 → Circleの800M USDC凍結 → ハッカーが事前にAaveにUSDTを預けてETHを借りて逃げた、という流れを詳しく書いています。  
→ https://x.com/cryptoblaney/status/2115964568342261955

この投稿が広く引用・コピーされていて、以下のような類似投稿が多数出ています：

- @heyHilal_ ：「one wallet linked to the Binance outflows moved about $60M in USDT into Aave and borrowed 19,762 WETH」と具体的な数字を挙げたもの  
  → https://x.com/heyHilal_/status/2116022796438352212

- @8figureceo ：「the binance hacker found the gap」として同じポイントを簡潔にまとめたもの  
  → https://x.com/8figureceo/status/2115967462709801466

- @agentmavericksi ：オンチェーンデータに基づき「60M USDT on Aave V3 and borrowed 19,762 ETH」と報告したもの  
  → https://x.com/agentmavericksi/status/2116006940086042919

- @Mr_Chonky ：「He’s never paying it back. Doesn’t need to.」と結論を強調したもの  
  → https://x.com/Mr_Chonky/status/2115934804902584550

### 日本語の類似ポスト

- @bigwave96475815 ：Aaveを「管理者なしの自動暗号資産質屋」と説明し、凍結前にETHに換えたと指摘したもの  
  → https://x.com/bigwave96475815/status/2116021408094703640

- @WakiyamaP ：Aaveの市場凍結について触れたもの  
  → https://x.com/WakiyamaP/status/2115994960269050328

- @Advance_start ：Aave側のリスク（預け手に損失が出ない理由）を詳しく解説したもの  
  → https://x.com/Advance_start/status/2115987811111506144

全体的に「ハッカーが凍結を想定してAaveを使った賢い動き」という観点の投稿が英語・日本語ともにかなり出回っています。特に@cryptoblaneyの投稿が起点となって拡散している印象です。

もっと特定の角度（例：日本語だけ、詳細なオンチェーン分析だけなど）で探したい場合は教えてください。

---

```
Aaveの凍結メカニズムを詳しく
```

**Aaveの「凍結（Freeze）」メカニズム**について、今回のBinance事件での対応を踏まえて詳しく説明します。

### 1. Freeze（凍結）とPause（一時停止）の違い
Aaveには緊急時のリスク管理ツールとして主に2つの状態があります。

| 機能                  | 新規供給（預け入れ） | 新規借入 | 引き出し | 返済 | 清算     | 備考                                         |
|-----------------------|----------------------|----------|----------|------|----------|----------------------------------------------|
| **Freeze（凍結）**    | ×                    | ×        | ○        | ○    | ○        | 今回使われたもの。既存ポジションの管理は可能 |
| **Pause（一時停止）** | ×                    | ×        | ×        | ×    | 制限あり | より強力。ほぼ全アクションを止める           |

- **Freeze**は「新規の供給・借入を止める」が、既存ユーザーの**引き出し・返済・清算は継続**させる比較的ソフトな対策です。
- 凍結中は新しい担保を追加できないため、ヘルスファクター（健全性指標）を上げる方法は「返済」のみになります。

今回のBinance事件では、**Freezeを選択**し、Pauseは使っていません。

### 2. 誰が・どのようにFreezeを実行するか
- **実行権限**：主に**Aave Guardian**（コミュニティ選出のマルチシグ）が持っています。Emergency Admin役割を通じて、迅速に実行可能です。
- V3では特定のリザーブ（資産）単位で細かくFreeze可能。
- V4ではさらにHub/Spoke単位など、より粒度の高い制御が可能です。
- Guardianは**Freezeを解除（Unfreeze）することも可能**です。一方、供給・借入キャップの大幅削減などはフルガバナンス投票が必要で、復旧に数日かかることがあります。

今回の流れ（LlamaRisk公式報告より）：
- 事件報告から約10分以内にAave Labs、TokenLogic、Certoraと合同の緊急対応（war room）を実施。
- 「ハッカーが盗んだ資産を任意の上場資産にスワップして担保に使う可能性がある」ため、**特定資産だけでなく広範囲をFreeze**する方針を決定。
- Guardianマルチシグが署名・実行（最初のFreezeは21:42 UTC頃から開始）。
- 結果：Aave V3で16ネットワーク・175リザーブ、V4で4ネットワーク・117リザーブをFreeze。
- Horizon RWA市場など、権限付き資産のみの市場は対象外としました。

### 3. Freezeの効果と影響
**直接的な効果**
- ハッカーを含む誰も、新たに資産を預けたり借りたりできなくなる。
- 既存ポジションは維持され、通常の清算ルールが適用される。

**今回のハッカーのポジションについて**
- ハッカーはFreeze前（約40分前）に60M USDTを供給し、約19,762 WETH（当時約4,460万ドル）を借りた。
- このポジションは**超過担保状態**（担保約5,990万ドル vs 負債約4,380万ドル）で、Aaveの供給者に直接的なリスクはないと報告されています。
- ETH価格が約4%上昇すれば清算対象になる可能性があります。

**副次的な影響**
- 新規供給が止まるため、既存の供給者が引き出すと**利用率（Utilization）が上昇**しやすい。
- 利用率が高まると借入金利が急上昇することがあるため、今回はRisk Stewardsが一時的にSlope2（高利用率時の金利傾き）を引き下げる調整を提案・実施しています。
- 長期化すると流動性や利用者体験に影響するため、状況が落ち着き次第、段階的にUnfreezeする方針です。

### 4. なぜこの仕組みが存在するのか
Aaveは完全に分散型ですが、**プロトコル全体の健全性を守るための緊急回路遮断器**としてこれらの機能を用意しています。  
個人のポジションを強制的に動かすことはできず（ユーザーは自己保管）、あくまで「市場全体の新規活動を制限する」レベルに留まっています。

公式の詳細報告はこちらです：  
[Binance Hot Wallet Exploit: Aave's Response (LlamaRisk)](https://governance.aave.com/t/binance-hot-wallet-exploit-aaves-response/25954)

さらに技術的なコントラクトレベルの詳細や、V2/V3/V4の違い、過去のFreeze事例など知りたい部分があれば教えてください。

---

```
過去に同じような事件があれば、簡単な説明でいいですから列挙してください。
```

過去に**似たようなパターン**（盗んだ／問題のある資産をDeFiレンディングに担保として預け、凍結・回収されにくい資産を借りて逃げる）の主な事例を簡単に列挙します。

### 1. **Kelp DAO / rsETH エクスプロイト（2026年4月）** ※最も類似
- 攻撃者がKelp DAOのLayerZeroブリッジを悪用し、裏付けのないrsETHを約11.65万枚（約2.92億ドル）ミント・盗取。
- 即座にそのrsETHをAave（およびCompound、Euler）に担保として預け、本物のWETH/ETHを約2億ドル以上借り出した。
- Aave側に最大約1.2〜2.3億ドル規模の不良債権（bad debt）が発生。
- Aaveは関連市場を緊急Freezeし、その後大規模な資金流出（約124億ドル規模）を招いた。
- 「問題のある担保を使ってクリーンなETHを借りて逃げる」という点で、今回のBinance事件と非常に近いプレイブック。

### 2. **その他の関連・類似事例**
- **複数の小〜中規模DeFiエクスプロイト**で、攻撃者がAaveのフラッシュローンや担保機能を悪用して資金を移動・洗浄したケースは複数ある（例: 2023年のSturdy Financeなど）。ただし規模や「ステーブルコイン凍結回避」の意図は今回ほど明確ではない。
- 過去の大規模CEXハッキング（例: Bybit 2025年など）でも、盗んだ資産をDEXやDeFiに流して洗浄する動きはあったが、Aaveに大量のステーブルを担保預けてETHを借りるという明確な「凍結すり抜け」戦術は、Kelp DAO事件が最も近い先行事例。

今回のBinance事件のような「発行体によるステーブルコイン凍結を前提に、事前にAaveでETHに変換する」戦術は、大規模なものは比較的新しく、**Kelp DAO事件が直接の先例**として挙げられます。

さらに詳しい特定の事件について知りたい場合は教えてください。

---

- この投稿は、TRM Labsの報告を基に、北朝鮮のハッカー集団TraderTraitorがBinanceから約63.6億ドルの暗号通貨を盗んだ史上最大の窃盗事件を報じている。
- 10のブロックチェーン上で20分以内に資金が移動し、Bybitの2025年ハックの4倍規模で、Tetherなどにより約27億ドルが凍結されたが、24億ドルは依然として追跡困難。
- BinanceはDevOpsエンジニアのノートPC経由の侵害を認め、SAFU基金で損失を補填する方針を示しており、北朝鮮の過去のハック手法と一致する特徴が見られる。



