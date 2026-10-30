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
