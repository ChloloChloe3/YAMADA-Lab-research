# 人工感情と探索・安全行動に関する文献調査

研究計画との対応・文献の優先順位・実験設計への反映

**調査・整理：工藤優花**  
**調査基準日：2026年10月8日**  
**形式・記述更新日：2026年10月22日**

本資料は、私の研究計画に関連する先行研究を分野横断で整理し、既存研究との重なり、研究課題、今後の精読・実験方針をまとめたものである。

本調査では、好奇心と脅威評価を履歴依存の内部状態として扱う研究を、人工感情、内発的動機づけ、安全強化学習、記憶と部分観測、人間による行動評価まで広げ、72件の関連文献を整理した。計画にある二つの近接研究に加え、既に履歴と減衰を持つ感情モデル、好奇心と恐怖の安全探索、状態追加と報酬変更の切り分けが研究されている。

本調査を通じて、私の研究計画では新規性の対象をさらに精密にすることが重要だと整理した。具体的には、同じ原観測と推定信号を用い、内部状態の持続性と接続経路が何を変えるかを切り分け、人の知覚との対応を評価する比較を中心候補として整理した。これは現時点での研究方針の候補であり、組合せ全体の先行例が存在しないとの証明ではない。

調査の起点は、私の研究計画資料 `Research_Presentation_CRN_EN(1).pptx` に記載した研究背景、先行研究、RQ1からRQ4、提案手法、実験計画である。修士段階のGridWorld検証を主対象とし、ARや都市デジタルツインへの拡張は背景文献として扱う。

## 1 調査範囲と整理方法

出版社、学会論文集、著者・所属機関の公開資料、arXiv、OpenReviewを用い、基礎研究から2026年10月8日までの近年研究を分野横断で確認した。本文の関連節を確認した文献と、抄録・書誌中心の文献を区別する。網羅性を保証するシステマティックレビューではなく、精読と再現対象を選ぶための調査である。

| **優先度**   | **精読の目的**                               | **精読後に整理する事項**                     |
|--------------|--------------------------------------------|------------------------------------------|
| S 最優先     | 計画と直接重なる研究、設計判断を変える文献 | 原式、実験条件、比較対象、本研究との差分 |
| A 基礎と比較 | 理論、強いbaseline、評価方法を固める       | 採用する方法と採用しない方法、その理由   |
| B 発展       | 周辺理論や博士段階への展開を見渡す         | 将来の接続先と第一段階での適用限界       |

各文献の「確認」は、本文＝関連する方法・結果・限界の節まで確認、抄録＝抄録と書誌を確認、索引＝出版社の検索索引と著者機関の書誌を確認、を意味する。本文確認は全文精読・証明の検算・再現完了を意味しない。「本研究との関係」と実験設計への反映事項には、私の解釈・判断を含む。

## 2 分野全体の見取り図

| **領域**            | **本調査で整理した主要な区別**                                          | **代表文献**                                                        |
|---------------------|-----------------------------------------------------------------|---------------------------------------------------------------------|
| 人工感情とappraisal | 評価の生成、履歴状態、行動への作用を分ける                      | Moerland 2018、Marinier 2008、Sequeira 2014、Zhang 2025             |
| 好奇心と情報探索    | 新規性、予測誤差、学習進捗、情報利得は異なる                    | Oudeyer 2007、ICM 2017、RND 2019、LPM 2026                          |
| 安全とリスク        | 危険予測、制約、tail risk、復帰可能性を分ける                   | Intrinsic Fear 2016、CPO 2017、Recovery RL 2021、ActSafe 2025       |
| 状態と記憶          | 感情履歴、安全予算、一般的なRNN記憶を比較する                   | DRQN 2015、Sauté 2022、Ni 2022、POPGym 2023                         |
| 人間の探索と感情    | 探索の量と情報探索、interestとcuriosity、恐怖とストレスを分ける | Silvia 2005、Wilson 2014、de Berker 2016、Ten 2021                  |
| 人間の行動評価      | 人間らしさ、慎重さ、意図の読み取り、信頼は別の変数              | Cautious Curiosity 2023、Navigates Like Me 2023、Dragan 2013        |
| 内部状態の代替理論  | 身体の安定、beliefの調整、appraisalを同一視しない               | Homeostatic RL 2014、Deeply Felt Affect 2021、Interoceptive AI 2026 |
| 多目的評価と統計    | 観測したfrontier、真のPareto集合、推定の不確かさを区別する      | Roijers 2013、Hayes 2022、Henderson 2018、Agarwal 2021              |

人工感情というキーワードだけで探すと、内発的動機づけ、安全状態の追加、危険記憶、モデル不確実性による探索制御を取りこぼす。機構と評価対象の両方から検索することが重要である。

## 3 本研究計画に近い研究と差分

| **文献**                | **既に扱っていること**                           | **本研究計画で確認する差分**                                               |
|-------------------------|--------------------------------------------------|------------------------------------------------------------------------|
| Marinier 2008 ［E02］   | 履歴と減衰を持つmood、感情だけとの比較           | 目標距離情報の交絡を取り除いた比較。好奇心と脅威の二変数を切り分ける。 |
| Okada 2025 ［X01］      | 予測誤差の時間変化によるcuriosityとfear          | 正式題名を引用。更新式と危険の定義を本文精読で照合する。               |
| Feariosity 2025 ［R01］ | 好奇心と恐怖、安全制約、経験再生                 | 感情の持続性と作用経路の重複を本文で確認する。                         |
| Sauté 2022 ［R04］      | 安全予算の追加状態とcost shapingのアブレーション | 安全予算とは異なるappraisal履歴の役割を、一般的記憶と分ける。          |
| Barthet 2022 ［E08］    | affect報酬と探索セル選択                         | セル選択と方策入力の状態追加を混同しない。                             |
| LPM 2026 ［C15］        | 学習進捗、ノイズ回避、MiniGrid Lava課題          | curiosityの生成原理を強い既存手法と比較する。                          |
| MICE 2025 ［R03］       | 危険経験の記憶と内発的cost                       | 危険記憶と、時間的に減衰する内部状態を比較する。                       |
| CC 2023 ［H01］         | curiosity報酬、Mario行動、人間の動画評定         | human-likenessとcuriosity・慎重さの知覚を分けて測る。                  |
| CPM RL 2025 ［E09］     | appraisalとRL、人間の感情判断の予測              | 物語人物の感情評価と、実際のagent行動評価を分ける。                    |

表に示した差分は、私の研究で検討する論点の候補である。抄録だけの文献に対して、特定の比較や人間評価が「ない」と断定していない。今後の精読では、FeariosityとOkada論文の原式、持続状態、各比較条件を優先して照合する。

## 4 本調査から得た研究計画への反映方針

### 4.1 新規性を比較する対象へ置く

Marinierではemotionとmood、Oudeyerでは履歴からの学習進捗、Sautéでは状態追加とcost shapingが既に比較されている。履歴状態や2×2の形式だけを新規性にしない。共通推定信号を用いた持続性・接続経路・未見環境・知覚の対応を新規性候補として絞る。 ［E02、C02、R04］

### 4.2 情報経路と記憶を分ける

同じ推定器を用いても、報酬経路と方策入力経路では情報の到達先が異なる。「同じ原観測、同じ推定器、同じ経験予算」と記述し、瞬時の評価値を直接入力する条件と、持続状態にして入力する条件を比較する。可能なら同程度の記憶容量のGRU対照も置く。 ［X05、X06］

### 4.3 感情強度の操作を定義する

報酬の重み変更は最適化目的を変える。一方、入力特徴の倍率変更はネットワークが打ち消せる。state条件の重み走査は何を操作するかを明示し、必要なら方策固定後の内部状態への介入を補助実験にする。減衰率を変えると記憶長だけでなく振幅やclip到達頻度も変わり得るため、それらを記録する。

### 4.4 未知とノイズと危険を分離する

安全で未知、安全で確率的、危険だが予測可能、危険で不確実という条件を分ける。failure probabilityは対象行動、予測時間幅、失敗事象を定義する。学習進捗でノイズを抑えることと、脅威モデルで危険を避けることを別に検証する。 ［R11、C13、C15］

### 4.5 評価中の更新と状態リセットを定義する

未見地図では方策を凍結し、推定器を更新するオンライン探索と、推定器も凍結する評価を分ける。実際の予測改善から学習進捗を算出する方式では、凍結すると信号が変わるため、計算方法と評価の意味を明記する。内部状態と経験記憶をエピソード間でリセットするかも決める。

### 4.6 安全指標の分母と目的を固定する

固定ステップ予算でcoverageを測り、事故数、事故を含むエピソード率、環境ステップ当たりの事故を併記する。動かないことで安全に見える条件や、死亡で探索時間が短くなる条件を区別する。CVaRは損失変数とtail水準を定義する。重み探索は検証地図で行い、未見地図で最終評価する。 ［R08、R10、X12］

### 4.7 行動からの知覚と感情表示の効果を分ける

同じ見た目・速度・動画長で手法名を伏せ、複数seedと地図から刺激を選ぶ。curiosityと慎重さの具体的項目、自由記述、条件識別を測る。行動と評定の対応を主な検証対象とし、内部状態の表示が理解を助けるかは別実験とする。 ［H02、H03、H04］

### 4.8 統計と調整予算を揃える

条件間の比較は単一seedや代表動画だけで行わず、seed・地図・参加者・刺激の反復を扱う。信頼区間を示し、評定では混合効果モデル等を検討する。性能比較のチューニング予算を揃え、4条件の平均値だけの相関から対応を断定しない。 ［H12、H13］

修士段階では、追加する比較を、瞬時評価と履歴状態の比較、未知・ノイズ・危険を分けた環境、評価中の更新規則の明示、近接手法を1から2個選んだ比較に絞る方針とする。

### 現時点での新規性の整理

既存の好奇心・安全強化学習・感情モデルを踏まえ、学習進捗と失敗予測から生成する履歴依存状態を共通化する。その上で、報酬経路、方策観測経路、両経路への接続が、探索と安全の関係、未見環境への適応、人による行動の解釈に与える差を、情報経路と記憶の交絡を明示して比較する。

以上を、現時点での研究目的の候補として整理した。最終的な新規性の主張は、近接文献の本文照合と実験結果によって確定する。

## 5 精読・再現の優先順位と今後の調査計画

| **順** | **文献**                      | **精読によって確定する事項**                         |
|--------|-------------------------------|----------------------------------------------|
| 1      | Moerland 2018 ［E01］         | 領域全体の地図と、感情の生成源・作用先を把握 |
| 2      | Marinier 2008 ［E02］         | 持続状態の原式と情報量の交絡を確認           |
| 3      | Okada 2025 ［X01］            | 二つの評価の原式・統合・安全の定義を確認     |
| 4      | Feariosity 2025 ［R01］       | 好奇心と恐怖をどう結合し、何と比べたか確認   |
| 5      | Sauté 2022 ［R04］            | 状態と報酬変更の切り分けを確認               |
| 6      | Oudeyer 2007 ［C02］          | 学習進捗の履歴推定とノイズの扱いを確認       |
| 7      | LPM 2026 ［C15］              | 最新の学習進捗baselineとGridWorld接点を確認  |
| 8      | Curiosity-Critic 2026 ［C16］ | 有限データの偽の学習進捗と比較方法を確認     |
| 9      | Ni 2022 ［X05］               | 通常の記憶baselineを固める                   |
| 10     | CC 2023 ［H01］               | 報酬から行動、人間の印象までの評価を確認     |
| 11     | Milani 2023 ［H02］           | 人間の判断根拠と交絡の記録方法を確認         |
| 12     | Agarwal 2021 ［H13］          | seedと地図の不確かさを評価する方法を確認     |

続く調査では、ActSafe、MICE、Intrinsic Fear、Depeweg、ICM・RND・Disagreementを精読し、実装比較の候補を絞る。Silvia、Ten、Erdemliは人工感情の命名と心理学的根拠を、Dragan・Gray・Godspeedは人間評価の構成概念を整理するために読む。

| **時期の目安** | **調査すること**                | **具体的な成果**                                 |
|----------------|---------------------------------|--------------------------------------------------|
| 第1週          | 最も近い原著を精読する          | 重複点と差分の表。新規性候補を1段落で書く。      |
| 第2週          | curiosityとthreat推定を照合する | 原式、ノイズ条件、失敗定義、更新規則を決める。   |
| 第3週          | baselineと記憶比較を選ぶ        | 再現対象を絞り、観測・容量・予算の比較表を作る。 |
| 第4週          | 人間評価と統計計画を読む        | 項目案、動画抽出法、反復単位、主要指標を決める。 |

今後の調査では、各論文の原観測、追加情報、内部状態とリセット、更新式、作用先、学習予算、危険の定義、未見環境、人間評価、再現コードを同じ書式で抜き出す。この比較欄の充実を調査の進捗指標とする。

### 継続検索のキーワード

感情と履歴 appraisal reinforcement learning、emotion mood dynamics、persistent affective state、emotion state augmentation

好奇心 learning progress intrinsic motivation、prediction error noisy TV、epistemic aleatoric exploration、information gain curiosity

安全と状態 safe curiosity fear、failure prediction intrinsic fear、safety state augmentation cost shaping、memory intrinsic cost

比較と知覚 recurrent RL POMDP baseline、legibility human-like navigation、perceived curiosity cautiousness、RL statistical evaluation

近接文献の参考文献を後ろ向きに確認し、その後の引用論文を前向きに追う。AIIDE、ACII、AAMAS、ICML、ICLR、NeurIPS、HRI、CHI、IEEE Transactions on Affective ComputingとRA-Lを横断する。感情認識や共感対話だけのLLM研究は、現在の機構との接点がある場合に追加する。

## 6 注釈付き文献一覧 72件

IDは前半の表と本文参照に対応する。各項目に正式題名、年、掲載先、原典リンク、概要、本研究との関係、適用限界、確認レベルを示す。長い著者一覧は第一著者ほかで省略する。

### 6.1 人工感情とappraisal

#### E01 Emotion in reinforcement learning agents and robots: a survey

Thomas M. Moerland; Joost Broekens; Catholijn M. Jonker (2018) Machine Learning 107(2), 443–480  
優先度 S 確認 本文

**概要** 感情の誘発源とRLへの作用を体系化し、報酬変更・状態変更・メタ学習・行動選択を区別する、この研究領域の入口となる総説。

**本研究との関係** 計画のreward/stateの2×2比較は、この総説の機能分類に直接対応する。本研究の基礎文献として位置づけ、原著実証研究とは分けて扱う。

**適用限界** 2017年までの文献が中心。感情導入による性能向上だけでは心理学的妥当性は示せない。

[原典 https://doi.org/10.1007/s10994-017-5666-0](https://doi.org/10.1007/s10994-017-5666-0)

#### E02 Emotion-Driven Reinforcement Learning

Robert P. Marinier III; John E. Laird (2008) Proceedings of the 30th Annual Meeting of the Cognitive Science Society, 115–120  
優先度 S 確認 本文

**概要** Soarでappraisalと減衰するmoodを統合し、feelingを内発報酬に使用。迷路課題でemotionのみより学習初期とばらつきが改善。

**本研究との関係** moodはmoving history of emotionで、現在emotionへ引かれneutralへ減衰する。持続内部状態とrewardへの接続は計画に極めて近い。emotion-only対emotion+mood比較もある。

**適用限界** 目標までの距離の知識を感情条件だけが使用する交絡を著者自身が認める。履歴感情だけの新規性は主張できない。

[原典 https://escholarship.org/uc/item/9jk839mw](https://escholarship.org/uc/item/9jk839mw)

#### E03 Learning by appraising: an emotion-based approach to intrinsic reward design

Pedro Sequeira; Francisco S. Melo; Ana Paiva (2014) Adaptive Behavior 22(5), 330–349  
優先度 S 確認 抄録と書誌

**概要** 相互作用履歴を評価する四つのappraisalを報酬特徴に変換し、重みを最適化。部分観測の採餌課題で通常の目標報酬型RLを上回る。

**本研究との関係** appraisal由来の内発報酬はすでに直接的先行研究がある。2011 ACII論文は前身。計画では状態入力との因果分離や同一観測下の比較を重視する。

**適用限界** 本文は今回未読。総説は目標距離heuristicによるbaselineとの情報量差を指摘している。

[原典 https://doi.org/10.1177/1059712314543837](https://doi.org/10.1177/1059712314543837)

#### E04 EMA: A process model of appraisal dynamics

Stacy Marsella; Jonathan Gratch (2009) Cognitive Systems Research 10(1), 70–90  
優先度 A 確認 抄録と書誌

**概要** 自動的appraisalと知覚・推論の更新を区別して、速い感情反応と熟考後の変化を説明する。自然な情動場面を計算モデルで例示する。

**本研究との関係** 計画のgを単なる刺激反応とせず、目標・解釈・coping能力の評価として定義する理論的基礎。時系列の感情動態を考える際の理論的基礎として位置づける。

**適用限界** この論文の中心はプロセスモデル。通常のdeep RLとの性能比較や2×2アブレーションを実証した論文ではない。

[原典 https://www.stacymarsella.org/publications/abstracts/MarsellaCSR09-abstract.html](https://www.stacymarsella.org/publications/abstracts/MarsellaCSR09-abstract.html)

#### E05 Modeling appraisal in theory of mind reasoning

Mei Si; Stacy C. Marsella; David V. Pynadath (2010) Autonomous Agents and Multi-Agent Systems 20, 14–31  
優先度 A 確認 抄録と書誌

**概要** POMDPの意思決定・信念更新から五つのappraisalを構成。自己と他者についての再帰的信念により社会的感情を三つの場面で例示する。

**本研究との関係** 長期関係へ拡張すると、脅威や安全性の評価は物理的結果だけでなく他者の意図・信念にも依存する。appraisalの数式化と部分観測の先行例。

**適用限界** 今回確認は抄録のみ。感情信号の生成と、その感情によるpolicy改善は別の研究課題として区別する。

[原典 https://doi.org/10.1007/s10458-009-9093-x](https://doi.org/10.1007/s10458-009-9093-x)

#### E06 A reinforcement learning model of joy, distress, hope and fear

Joost Broekens; Elmer Jacobs; Catholijn M. Jonker (2015) Connection Science 27(3), 215–233  
優先度 S 確認 抄録と書誌

**概要** joy/distressをTD誤差、hope/fearを予期される利得・損失に対応づけ、学習とともに生じる馴化・消去などの感情動態を検討する。

**本研究との関係** threat/fearを現在の負報酬と同一視せず、予測された損失として設計するために重要。RL信号を感情と命名する前に心理学的動態を検証する姿勢が参考。

**適用限界** 著者は学習性能改善それ自体を主目的としていない。感情生成の妥当性と感情による制御効果を混同しない。

[原典 https://doi.org/10.1080/09540091.2015.1031081](https://doi.org/10.1080/09540091.2015.1031081)

#### E07 Combating Reinforcement Learning's Sisyphean Curse with Intrinsic Fear

Zachary C. Lipton et al. (2016) arXiv:1611.01211 (revised 2018; checked source is preprint)  
優先度 S 確認 本文

**概要** 近い将来の破局確率を予測するfearモデルでDQN報酬を修正し、破局の再発と忘却を抑える。玩具課題・Cartpole・Atariで比較する。

**本研究との関係** fear由来reward shapingと安全探索の直接的な先行例の一つ。予測モデルF(s)は持続するe_tとは異なるので、同じfearという名称でも計算機構を区別する。

**適用限界** 安全保証そのものではない。Seaquestでは収益が改善しても破局率が同程度。fear radiusと係数の設計が重要。

[原典 https://arxiv.org/abs/1611.01211](https://arxiv.org/abs/1611.01211)

#### E08 Play with Emotion: Affect-Driven Reinforcement Learning

Matthew Barthet et al. (2022) 10th International Conference on Affective Computing and Intelligent Interaction (ACII)  
優先度 S 確認 本文

**概要** Go-Blendで人間のarousalを用いた報酬と探索セル選択を別々に操作し、レースゲームで感情系列の再現と探索・得点の改善を示す。

**本研究との関係** 感情に基づくrewardと探索state selectionを比較するため、計画の作用位置比較と近い。ただしstate selectionはpolicyへe_tを追加するstate augmentationではない。

**適用限界** 単一レース課題・3 runs。arousalは人間の注釈から予測し、遷移appraisalから生成する自律的感情ではない。arousal最大化ではoffroad増加などが起きる。

[原典 https://arxiv.org/abs/2208.12622](https://arxiv.org/abs/2208.12622)

#### E09 Modeling Cognitive-Affective Processes With Appraisal and Reinforcement Learning

Jiayi Zhang; Joost Broekens; Jussi P. P. Jokinen (2025) IEEE Transactions on Affective Computing 16(2), 771–782 (online 2024)  
優先度 S 確認 プレプリント本文と掲載版書誌

**概要** CPMのnovelty・goal relevance・conduciveness・powerをRL計算で定式化し、物語課題に対する人間の感情判断を複数実験で予測する。

**本研究との関係** appraisal→感情の解釈可能性と人間評価を結びつけた近年の重要研究。fear/anxiety等をcontrol/powerとsuddennessで区別する設計が参考になる。

**適用限界** 全文確認は2023年arXiv v2で、掲載版との全差分は未確認。人間が物語の主人公を評価する設定で、agentの実際の探索安全性能比較ではない。

[原典 https://doi.org/10.1109/TAFFC.2024.3470555](https://doi.org/10.1109/TAFFC.2024.3470555)

#### E10 Homeostatic reinforcement learning for integrating reward collection and physiological stability

Mehdi Keramati; Boris Gutkin (2014) eLife 3, e04811  
優先度 S 確認 本文

**概要** 身体内部の不足を減らす報酬を定義し、報酬最大化と生理的安定性の対応を証明。予期的反応・満足・極端な逸脱回避をシミュレーションする。

**本研究との関係** 履歴を持つ内部状態とreward/stateの接続を論じる基礎文献として位置づける。身体的homeostasisとappraisal由来の好奇心・脅威は、内部状態という共通点を持つが同一概念ではない。

**適用限界** 主に生理的必要と動物行動の規範モデル。感情ラベル・主観経験・人間に知覚される自然さを直接実証したものではない。

[原典 https://doi.org/10.7554/eLife.04811](https://doi.org/10.7554/eLife.04811)

#### E11 Emotional Valence and the Free-Energy Principle

Mateus Joffily; Giorgio Coricelli (2013) PLOS Computational Biology 9(6), e1003094  
優先度 A 確認 本文

**概要** free energyの時間変化をvalenceとみなし、その一階・二階変化から感情動態を構成。感情による学習率調整で非定常環境への適応を例示する。

**本研究との関係** 感情の作用場所はreward/state以外にも学習率・不確実性推定にある。予測誤差そのものと、その減少率の区別を整理する基礎文献とする。

**適用限界** 行動RLの2×2比較ではない。free-energy数式を採用するなら予測誤差との同一視に必要な仮定を確認する。

[原典 https://doi.org/10.1371/journal.pcbi.1003094](https://doi.org/10.1371/journal.pcbi.1003094)

#### E12 Deeply Felt Affect: The Emergence of Valence in Deep Active Inference

Casper Hesp et al. (2021) Neural Computation 33(2), 398–446  
優先度 A 確認 抄録と書誌

**概要** 階層active inferenceでvalenceを行動モデルへの信頼から推論する内部状態として構成し、T迷路と文脈反転で適応的confidence調整を例示する。

**本研究との関係** 持続する感情状態を、単なる報酬の別名でなくbelief-about-beliefとして扱う代替理論。非定常環境と内部感情動態の関係を比較する。

**適用限界** 今回確認は著者機関掲載の詳しい抄録。simulationは顔面的妥当性の初段階で、人間の主観感情・神経活動へfitした実証ではない。

[原典 https://doi.org/10.1162/neco_a_01341](https://doi.org/10.1162/neco_a_01341)

#### E13 Drive competition underlies effective allostatic orchestration

Oscar Guerrero Rosado et al. (2022) Frontiers in Robotics and AI 9, 1052998  
優先度 A 確認 本文

**概要** 内部needsの競合を神経集団の相互抑制とattractor dynamicsで実装し、開放空間を動くげっ歯類の移動傾向と環境変化への自己調整を再現する。

**本研究との関係** curiosity/threatという競合する内部状態が探索を制御する計画に関連。RLを経由しない内部状態による直接制御との比較候補になる。

**適用限界** この原著の主モデルはattractor controlで、標準RLではない。二つのdriveをそのまま好奇心・不安の心理的同一物と見なさない。

[原典 https://doi.org/10.3389/frobt.2022.1052998](https://doi.org/10.3389/frobt.2022.1052998)

#### E14 Life-inspired interoceptive artificial intelligence for autonomous and adaptive agents

Sungwoo Lee et al. (2026) Nature Machine Intelligence 8, 1335–1346  
優先度 A 確認 抄録と書誌

**概要** 内外の状態変数を分け、内部状態の動態と調整から目標・学習・行動を生むinteroceptive AIを提案する、最新の研究展望・理論整理。

**本研究との関係** 内部状態を普遍的contextとして学習へ使う構想に近く、研究の広い位置づけに役立つ。掲載は2026年、前身arXivは2023年。

**適用限界** Perspectiveであり、新しいアルゴリズムの優位性を統制実験で証明した原著実証とは区別する。今回確認は著者機関の抄録と書誌。

[原典 https://doi.org/10.1038/s42256-026-01296-8](https://doi.org/10.1038/s42256-026-01296-8)

#### E15 What is interesting? Exploring the appraisal structure of interest

Paul J. Silvia (2005) Emotion 5(1), 89–102  
優先度 S 確認 抄録と書誌

**概要** 四つの実験で、novelty/complexityと理解できるというcoping potentialがinterestを予測し、楽しさとは異なる構造を持つことを支持する。

**本研究との関係** 好奇心を単なる新規性・予測誤差に還元しない心理学的根拠。新規で難しくても理解可能ならinterestを生むというg設計の候補になる。

**適用限界** interestとepistemic curiosityを同義としない。この論文から脅威や不安の対称的メカニズムまで実証されたとは言えない。

[原典 https://doi.org/10.1037/1528-3542.5.1.89](https://doi.org/10.1037/1528-3542.5.1.89)

#### E16 An Integrative Appraisal Model of Epistemic Curiosity

Asli Erdemli; Catherine Audrin; David Sander (2025) Affective Science 6, 714–725  
優先度 S 確認 本文

**概要** 情報ギャップ・感情・報酬予期をappraisalで統合し、高関連性でも対処能力が低い場合は好奇心より不安と情報回避が生じるというモデルを提案する。

**本研究との関係** 計画のcuriosity/threat軸の心理的根拠に極めて近い。gにnoveltyだけでなくrelevance・coping potentialを組み込む根拠と検証可能な対立予測を与える。

**適用限界** 理論総説であり、本論文の新規実験が分岐仮説を実証したわけではない。epistemic curiosityから物理的危険下の探索への適用は追加検証が必要。

[原典 https://doi.org/10.1007/s42761-025-00328-7](https://doi.org/10.1007/s42761-025-00328-7)

### 6.2 好奇心と学習進捗

#### C01 Curious model-building control systems

Jürgen Schmidhuber (1991) International Joint Conference on Neural Networks (IJCNN), Vol. 2, pp. 1458–1463  
優先度 S 確認 抄録と書誌

**概要** 世界モデルの予測信頼性がどれだけ改善するかを、Q学習を用いた4ネットワーク構成で最大化した初期研究。非決定的環境で実験した。

**本研究との関係** curiosityを予測誤差の大きさではなく学習進捗として定義する系譜の出発点。learning progressそのものを新規性と主張することは難しい。

**適用限界** 小規模な初期モデルであり、現代的な高次元環境や、脅威評価・感情状態の因果的役割の検証ではない。

[原典 https://people.idsia.ch/~juergen/curioussingapore/curioussingapore.html](https://people.idsia.ch/~juergen/curioussingapore/curioussingapore.html)

#### C02 Intrinsic Motivation Systems for Autonomous Mental Development

Pierre-Yves Oudeyer; Frédéric Kaplan; Verena V. Hafner (2007) IEEE Transactions on Evolutionary Computation, 11(2), 265–286  
優先度 S 確認 本文

**概要** Intelligent Adaptive Curiosityは状況空間を領域に分割し、各領域の予測誤差の履歴を平滑化して学習進捗を推定する。容易すぎる／学習不能な活動を避ける自律的な発達系列をロボット実験で示した。

**本研究との関係** 履歴を持つlearning progressの内部変数、平滑化、複数の動機を組み合わせる議論が計画に近い。瞬間的LPと履歴LPの比較の理論的根拠となる。

**適用限界** 領域分割・平滑化・表現に依存する。単一経験の前後差は確率的変動に敏感と本文でも指摘。人間の発達をそのまま再現するモデルとは主張していない。

[原典 https://adapt.informatik.hu-berlin.de/pub/papers/ims.pdf](https://adapt.informatik.hu-berlin.de/pub/papers/ims.pdf)

#### C03 VIME: Variational Information Maximizing Exploration

Rein Houthooft et al. (2016) Advances in Neural Information Processing Systems (NeurIPS/NIPS) 29  
優先度 A 確認 抄録と書誌

**概要** ベイズニューラルネットの動力学モデルを更新した際の事前・事後のKL変化を探索報酬とし、環境ダイナミクスに関する情報利得を最大化する。

**本研究との関係** 予測誤差、learning progress、情報利得を区別する重要な比較対象。何についての不確実性を減らすかを明示できる。

**適用限界** 変分推論による近似に依存し、実装・計算コストが高い。情報利得の報酬化であり脅威の内部状態との統合を直接扱わない。

[原典 https://proceedings.neurips.cc/paper/2016/hash/abd815286ba1007abfbb8415b83ae2cf-Abstract.html](https://proceedings.neurips.cc/paper/2016/hash/abd815286ba1007abfbb8415b83ae2cf-Abstract.html)

#### C04 Curiosity-driven Exploration by Self-supervised Prediction

Deepak Pathak et al. (2017) ICML, PMLR 70:2778–2787  
優先度 S 確認 抄録と書誌

**概要** 逆ダイナミクスモデルで学習した特徴空間で、次状態の予測誤差を内発的報酬にするICM。VizDoomやMarioで疎報酬探索、無報酬探索、未知レベルへの転移を検証した。

**本研究との関係** 標準的なprediction-error curiosityとして必須baseline。同じ表現・同じ予測器で報酬だけをLPに差し替える比較が因果的に明確。

**適用限界** 制御に関係しない変動を抑える設計だが、あらゆる観測ノイズや行動依存ノイズを排除する保証ではない。LPではなく誤差の絶対値。

[原典 https://proceedings.mlr.press/v70/pathak17a.html](https://proceedings.mlr.press/v70/pathak17a.html)

#### C05 Large-Scale Study of Curiosity-Driven Learning

Yuri Burda et al. (2019) ICLR 2019 (arXiv initial submission 2018)  
優先度 A 確認 抄録と書誌

**概要** 54環境で外発的報酬を使わない予測誤差ベース探索を評価。ランダム特徴と学習特徴の差、ゲームの外発的目的との一致、確率的環境での失敗を示した。

**本研究との関係** 学習器の予測対象・特徴表現が探索行動を大きく変える。noisy-TV条件と未知マップでの汎化を実験設計に含める根拠。

**適用限界** 探索の広さや外発的得点の向上は、感情状態の存在・機能の証拠とは異なる。好奇心の目標と課題目標の一致は環境依存。

[原典 https://arxiv.org/abs/1808.04355](https://arxiv.org/abs/1808.04355)

#### C06 Exploration by Random Network Distillation

Yuri Burda et al. (2019) ICLR 2019 (arXiv initial submission 2018)  
優先度 S 確認 本文

**概要** 固定ランダムネットの出力を学習する予測器の誤差を新規性報酬にするRND。次状態予測を行わず、低い追加コストで困難なAtari探索を改善した。

**本研究との関係** 強い低コストbaseline。LPの効果が単なる新規性報酬で説明できないかを確かめる。観測入力RNDと真の座標入力RNDを混同しない。

**適用限界** ターゲット関数は決定的でも、ノイズにより毎回異なる観測が入ると新規性が続き得る。RNDがnoisy-TVに一般に免疫とは言えない。

[原典 https://arxiv.org/abs/1810.12894](https://arxiv.org/abs/1810.12894)

#### C07 Self-Supervised Exploration via Disagreement

Deepak Pathak; Dhiraj Gandhi; Abhinav Gupta (2019) ICML, PMLR 97:5062–5071  
優先度 S 確認 抄録と書誌

**概要** 複数の動力学予測モデルの不一致を探索信号とし、確率的Atari、MuJoCo、Unity、実ロボットで評価。予測誤差の大きさから、知識不足による不一致へ移行した。

**本研究との関係** LPに対して別原理でノイズを避ける強いbaseline。認識的な不確実性と環境固有の確率性の違いを押さえる。

**適用限界** ensemble不一致も厳密なベイズ事後ではなく、表現、容量、学習相関、十分なデータ量に依存する。計算量を合わせた比較が必要。

[原典 https://proceedings.mlr.press/v97/pathak19a.html](https://proceedings.mlr.press/v97/pathak19a.html)

#### C08 RIDE: Rewarding Impact-Driven Exploration for Procedurally-Generated Environments

Roberta Raileanu; Tim Rocktäschel (2020) ICLR 2020  
優先度 A 確認 本文

**概要** 学習された状態表現の変化量を、遷移先状態のエピソード内訪問数の平方根で割った内発的報酬を用いる。MiniGridの手続き生成環境でICMやRND等と比較し、制御可能な対象への相互作用を促進した。

**本研究との関係** GridWorld/MiniGrid実験に直接参考になる。予測誤差やLP以外の制御可能性・影響に基づく探索を知ることで、好奇心の意味を広げられる。

**適用限界** 感情履歴を内部状態に追加する研究ではない。表現を方策損失で更新すると報酬を人工的に増やせるため、表現とpolicyの学習を切り分ける。

[原典 https://arxiv.org/abs/2002.12292](https://arxiv.org/abs/2002.12292)

#### C09 Never Give Up: Learning Directed Exploration Strategies

Adrià Puigdomènech Badia et al. (2020) ICLR 2020  
優先度 B 確認 抄録と書誌

**概要** 逆ダイナミクス表現と近傍エピソード記憶で新規性を計算し、探索重視から活用重視までの複数方策をUVFAで同時学習する。

**本研究との関係** 履歴を保持すること自体は一般的な探索機構でも実現可能。内部感情状態の優位性を示すなら、記憶を持つ非感情baselineとの比較が必要だと整理した。

**適用限界** 計算規模が大きく小規模GridWorldにそのまま導入する必要はない。情動を想定せずとも履歴と探索係数調整で行動変化が生まれる。

[原典 https://arxiv.org/abs/2002.06038](https://arxiv.org/abs/2002.06038)

#### C10 Agent57: Outperforming the Atari Human Benchmark

Adrià Puigdomènech Badia et al. (2020) ICML, PMLR 119:507–517  
優先度 B 確認 抄録と書誌

**概要** 探索と活用の程度が異なる方策群を学習し、訓練中に優先方策を適応的に選ぶことで、57のAtariゲームすべてで標準的な人間基準を超えた。

**本研究との関係** 固定の好奇心・脅威重みだけでなく、動的な探索制御で達成できる効果を考える対照研究。感情機構とmeta-controllerの違いを明示する。

**適用限界** 大規模分散エージェントで計算資源が大きい。内部状態の履歴が情動機能を持つかを切り分ける実験ではない。

[原典 https://proceedings.mlr.press/v119/badia20a.html](https://proceedings.mlr.press/v119/badia20a.html)

#### C11 Planning to Explore via Self-Supervised World Models

Ramanan Sekar et al. (2020) ICML, PMLR 119:8583–8592  
優先度 A 確認 抄録と書誌

**概要** Plan2Exploreは課題報酬なしで世界モデルを学習し、モデル内のplanningで将来の新規性を求める。その後、複数の下流制御課題にzero/few-shot適応する。

**本研究との関係** その場の好奇心・危険だけでなく、将来の学習価値と危険を予測する方向を知るための重要な世界モデル研究。長期展開の比較基準。

**適用限界** 小規模な第一段階の全baselineとしては実装が重い。計画・世界モデルの品質の改善と、感情状態の効果を混同しない。

[原典 https://proceedings.mlr.press/v119/sekar20a.html](https://proceedings.mlr.press/v119/sekar20a.html)

#### C12 Humans monitor learning progress in curiosity-driven exploration

Alexandr Ten et al. (2021) Nature Communications 12, 5972  
優先度 S 確認 本文

**概要** 自由に学習活動を選択できる人間実験と計算モデルで、選択には習熟度に加えて学習進捗の成分が必要と示した。難しすぎる活動の回避と、習得可能な活動への挑戦を説明する。

**本研究との関係** curiosityをLPとして扱う心理学的根拠。単純な中難度選好や新規性とLPを区別する設計、時間配分・活動切替の評価に役立つ。

**適用限界** 課題選択にLPが関与する証拠であり、LPが好奇心の唯一の原因との証明ではない。脅威・不安との統合や人工エージェントの主観的経験を検証していない。

[原典 https://www.nature.com/articles/s41467-021-26196-w](https://www.nature.com/articles/s41467-021-26196-w)

#### C13 How to Stay Curious while avoiding Noisy TVs using Aleatoric Uncertainty Estimation

Augustine Mavor-Parker et al. (2022) ICML, PMLR 162:15220–15240  
優先度 A 確認 抄録と書誌

**概要** Aleatoric Mapping Agentsは次状態の平均と偶然的不確実性を別々に予測し、予測不能な遷移への探索報酬を減らす。行動が引き起こす確率的罠を回避した。

**本研究との関係** 単に観測だけがランダムなnoisy-TVに加え、行動依存ノイズも評価条件に含める根拠。LPの効果が明示的なノイズ推定より優れるかを比較できる。

**適用限界** 不確実性予測の精度と学習量に依存する。従来の免疫とされる手法も行動依存ノイズには陥り得るため、絶対的ノイズ排除は主張しない。

[原典 https://proceedings.mlr.press/v162/mavor-parker22a.html](https://proceedings.mlr.press/v162/mavor-parker22a.html)

#### C14 Intrinsic Rewards for Exploration Without Harm From Observational Noise: A Simulation Study Based on the Free Energy Principle

Theodore Jerome Tinker; Kenji Doya; Jun Tani (2024) Neural Computation 36(9), 1854–1885  
優先度 A 確認 抄録と書誌

**概要** 潜在状態の予測事前分布と観測後分布のKLをhidden state curiosityとし、予測誤差curiosity・方策entropyとの組合せを迷路で比較。潜在状態への情報利得が観測ノイズの罠に頑健だった。

**本研究との関係** 観測予測誤差、パラメータ情報利得、潜在状態情報利得を区別する近年の参考例。複数の探索報酬成分のアブレーションが計画に近い。

**適用限界** 迷路シミュレーションでの結果。潜在モデルの仕様と事後推定に依存し、一般環境の安全保証や情動の機能証明ではない。

[原典 https://arxiv.org/abs/2405.07473](https://arxiv.org/abs/2405.07473)

#### C15 Beyond Noisy-TVs: Noise-Robust Exploration Via Learning Progress Monitoring

Zhibo Hou; Zhiyu An; Wan Du (2026) ICLR 2026 (arXiv initial submission September 2025; v2 April 2026)  
優先度 S 確認 本文

**概要** LPMは動力学予測器と前回の期待予測誤差を学ぶ誤差モデルを用い、誤差そのものではなく改善を探索報酬にする。理論、MNIST、MiniWorld、Atari等でノイズ頑健性を検証した。

**本研究との関係** 計画に最も近い最新の査読済み比較対象。Appendix BではMiniGrid Lava Crossingも評価し、探索と致命的危険が同居する点も近い。LPだけでは新規性にならず、脅威履歴状態とreward/state/both比較で差分を示す必要がある。

**適用限界** IGとの理論関係には尤度・期待誤差・モデル適合等の仮定がある。Lava CrossingではICMとLPMが同程度。有限データの単純な誤差差分全般に無条件のノイズ排除保証を与えるものではない。

[原典 https://arxiv.org/abs/2509.25438](https://arxiv.org/abs/2509.25438)

#### C16 Curiosity-Critic: Cumulative Prediction Error Improvement as a Tractable Intrinsic Reward for World Model Training

Vin Bhaskara; Haicheng Wang (2026) ICML 2026 Workshop on Epistemic Intelligence in Machine Learning (workshop, not main-conference paper); arXiv v3 June 2026  
優先度 S 確認 本文

**概要** 世界モデルの累積予測誤差改善を、現在の誤差から学習した漸近的誤差baselineを引く代理報酬にする。確率的GridWorldでRND、訪問数、単一步LP等と比較した。

**本研究との関係** 研究計画のGridWorldとLPに非常に近い最新文献。単一更新の前後差は純ノイズでもspurious rewardを生み得ること、RNDは真の座標入力とノイズ観測入力で挙動が異なることを直接示す。

**適用限界** 評価は制御されたGridWorldに限られる。有限容量・有限時間ではbaselineが偶然的不確実性だけでなく、そのモデルで削減できない認識的誤差も吸収する。高次元環境・安全・感情状態は未検証。

[原典 https://arxiv.org/abs/2604.18701](https://arxiv.org/abs/2604.18701)

### 6.3 安全探索とリスク

#### R01 "Feariosity"-Guided Reinforcement Learning for Safe and Efficient Autonomous End-to-End Navigation

Dong Hu et al. (2025) IEEE Robotics and Automation Letters, 10(8), 7723–7730  
優先度 S 確認 抄録と書誌

**概要** fearとcuriosityを統合するFeariosityモデルに基づき、潜在的危険を評価するpolicy constraintと、threat/unknown levelで利用確率を変える経験再生を提案。シミュレーションと実機の自律走行で評価。

**本研究との関係** 『好奇心と脅威評価を組み合わせ安全探索する』という着想の直接的な先行研究の一つ。名称や2感情併用を新規性にせず、履歴状態・時間持続・条件を揃えた比較の差を本文で確認する必要がある。

**適用限界** 本調査では著者所属大学の論文抄録を確認。IEEE全文を読めていないため、具体的な感情更新式・再帰状態の有無・比較条件の重複は未確定。

[原典 https://doi.org/10.1109/LRA.2025.3577523](https://doi.org/10.1109/LRA.2025.3577523)

#### R02 ActSafe: Active Exploration with Safety Constraints for Reinforcement Learning

Yarden As et al. (2025) ICLR 2025  
優先度 S 確認 本文

**概要** 確率的world modelのepistemic uncertaintyを用い、安全制約に対して悲観的な方策集合内で、不確実性の高い軌道を楽観的に探索する。GPでの仮定付き保証と、ensemble/RSSMを用いる実用版を区別する。

**本研究との関係** 未知だから探索する好奇心と、未知だから警戒する脅威評価の使い分けを数学的に整理する比較軸。uncertainty-only exploration、安全制約なし、両方という対照の設計に有用。

**適用限界** 理論にはLipschitz性、校正されたモデル、非空の初期安全方策集合などが必要。視覚制御の実用版ではwarm-upがあり、全条件でzero violationsを保証した結果ではない。感情状態のモデルではない。

[原典 https://openreview.net/forum?id=aKRADWBJ1I](https://openreview.net/forum?id=aKRADWBJ1I)

#### R03 Controlling Underestimation Bias in Constrained Reinforcement Learning for Safe Exploration

Shiqing Gao et al. (2025) ICML 2025, PMLR 267:18290–18316  
優先度 S 確認 本文

**概要** Memory-driven Intrinsic Cost Estimation (MICE)。経験したunsafe statesをflashbulb memoryに保存し、記憶内の高cost領域への近さをpseudo-countとしてintrinsic costにする。cost criticの過小評価を補正し探索中の違反を抑える。

**本研究との関係** 危険経験の履歴を利用し、以後の探索を抑制する先行例。記憶利用自体ではなく、現在のaffective stateの時間的持続・情報圧縮・適応がdanger memory/intrinsic costに対して何を加えるかを明確化する。

**適用限界** unsafe状態の記憶は、方策へ入力する持続的な感情状態と同じではない。cost criticのbias correctionが中心。ICMLの出版年は2025であり、arXiv公開2026を研究発表年と誤記しない。

[原典 https://proceedings.mlr.press/v267/gao25b.html](https://proceedings.mlr.press/v267/gao25b.html)

#### R04 Saute RL: Almost Surely Safe Reinforcement Learning Using State Augmentation

Aivar Sootla et al. (2022) ICML 2022, PMLR 162:20423–20443  
優先度 S 確認 本文

**概要** 残りのsafety budgetを追加状態として持たせ、budget超過時のcost shapingを組み合わせSafety Augmented MDPを構成。本文ではstate augmentationとcost shapingを外すablationも行い、budgetを変えた汎化を評価。

**本研究との関係** 『安全関連の履歴をstateへ追加する』『stateとreward/costを分離して比較する』両方に近い。感情状態の比較には、単なる残り安全予算stateを同じ入力次元で加える対照が必要。

**適用限界** 理論上のalmost-sure制約と、有限penalty・関数近似・有限学習での実証を区別する。状態は残り予算であり、好奇心や脅威appraisalそのものではない。

[原典 https://proceedings.mlr.press/v162/sootla22a.html](https://proceedings.mlr.press/v162/sootla22a.html)

#### R05 Recovery RL: Safe Reinforcement Learning with Learned Recovery Zones

Brijen Thananjeyan et al. (2021) IEEE Robotics and Automation Letters  
優先度 S 確認 本文

**概要** offlineの制約違反データでsafety criticを学習し、将来の違反危険が高いときにtask policyからrecovery policyへ切り替える。タスク向上と安全復帰を別方策へ分け、複数のシミュレーションと視覚ロボット制御で評価。

**本研究との関係** 計画のlearned failure probabilityには直接先行例がある。failure predictorをstateに渡すだけの対照と、predictorからrecovery/action gatingする対照を置くと感情状態の追加効果を評価しやすい。

**適用限界** safety criticはpolicy依存の割引将来違反値であり、任意のH-step failure probabilityと自動的に同一にはならない。offline危険データと安全復帰可能性が必要で、推定誤差下の無条件保証ではない。

[原典 https://arxiv.org/abs/2010.15920](https://arxiv.org/abs/2010.15920)

#### R06 Constrained Policy Optimization

Joshua Achiam et al. (2017) ICML 2017, PMLR 70:22–31  
優先度 A 確認 抄録と書誌

**概要** CMDPにおけるreward最大化とexpected cumulative cost制約を扱う方策最適化。trust regionと方策間の性能差のboundにより、更新ごとのnear-constraint satisfactionを目指す。

**本研究との関係** hazard penaltyを報酬へ混ぜる場合と、cost budgetを明示する場合は異なる。安全性能を比較する際にCPOまたはLagrangian系を同じcost定義・budgetで加える基礎文献。

**適用限界** 制約は期待累積costに対するもので、各episode・各stepで違反しない保証と同一ではない。本調査では出版元抄録を確認し、証明・実装を精読していない。

[原典 https://proceedings.mlr.press/v70/achiam17a.html](https://proceedings.mlr.press/v70/achiam17a.html)

#### R07 A Lyapunov-based Approach to Safe Reinforcement Learning

Yinlam Chow et al. (2018) NeurIPS 2018  
優先度 A 確認 抄録と書誌

**概要** 期待累積cost制約を持つCMDPで、Lyapunov関数から局所線形制約を構成し、安全を満たす方策更新へ動的計画法やRLを変換する。

**本研究との関係** 『脅威状態で危険が減った』という経験結果と、仮定・制約付きの安全性保証の差を整理する。hazard回避を感情報酬だけへ任せる設計との比較分類に必要。

**適用限界** 特定CMDPの仮定と期待cost制約に基づく保証。局所観測POMDPへそのまま適用できるとは限らない。抄録確認のみ。

[原典 https://papers.neurips.cc/paper_files/paper/2018/hash/4fe5149039b52765bde64beb9f674940-Abstract.html](https://papers.neurips.cc/paper_files/paper/2018/hash/4fe5149039b52765bde64beb9f674940-Abstract.html)

#### R08 Risk-Sensitive and Robust Decision-Making: a CVaR Optimization Approach

Yinlam Chow et al. (2015) NeurIPS 2015  
優先度 A 確認 抄録と書誌

**概要** 期待値だけでなくCVaRを目的とするMDPを定式化し、一定の誤差budgetでのworst-caseモデル誤差との関係を示す。CVaR向けvalue iterationと収束解析を提示。

**本研究との関係** 平均hazard率では低頻度の重大failureを見落とす。episode costの上側tailのCVaRまたはworst-case指標を加え、好奇心・脅威状態が重大failureを減らすか比較するための基礎。

**適用限界** CVaRのtailの定義・confidence level・costかreturnかを明記する必要がある。CVaR最適化は絶対に違反しないhard safetyと同一ではない。抄録確認のみ。

[原典 https://papers.nips.cc/paper_files/paper/2015/hash/64223ccf70bbb65a3a4aceac37e21016-Abstract.html](https://papers.nips.cc/paper_files/paper/2015/hash/64223ccf70bbb65a3a4aceac37e21016-Abstract.html)

#### R09 Safe Exploration for Optimization with Gaussian Processes

Yanan Sui et al. (2015) ICML 2015, PMLR 37:997–1005  
優先度 A 確認 抄録と書誌

**概要** GPの信頼区間と初期安全集合から、安全thresholdを満たす探索集合を拡張し、到達可能な安全集合内の最適化を行うSafeOptを提案。

**本研究との関係** 不確実性が高い対象を無条件に避けるのではなく、安全と判断できる領域から未知を学び安全集合を広げる原理が重要。coverageは全mapだけでなくsafely reachable regionを分母にした評価も検討できる。

**適用限界** 直接にはbandit/black-box optimizationであり、局所観測の逐次移動・状態履歴を扱うRLとは違う。GP正則性と安全seedの条件付き。出版元抄録確認のみ。

[原典 https://proceedings.mlr.press/v37/sui15.html](https://proceedings.mlr.press/v37/sui15.html)

#### R10 Safe Exploration in Finite Markov Decision Processes with Gaussian Processes

Matteo Turchetta et al. (2016) NeurIPS 2016  
優先度 A 確認 抄録と書誌

**概要** 未知の安全制約をGPで推定し、safely reachableなMDP領域を探索するSafeMDP。reachabilityに加え、安全な退出経路を確保し、unsafeな行き止まりを避ける。roverの未知地形map探索で評価。

**本研究との関係** 探索coverageとhazard回避という評価対象が計画に近い。単なるhazard侵入数に加え、復帰可能性・dead-end進入・安全到達領域coverageを区別するために読む。

**適用限界** GP正則性などの仮定下のMDPであり、任意のPOMDPや学習した感情状態に同じ保証が移るわけではない。出版元抄録確認のみ。

[原典 https://papers.nips.cc/paper_files/paper/2016/hash/9a49a25d845a483fae4be7e341368e36-Abstract.html](https://papers.nips.cc/paper_files/paper/2016/hash/9a49a25d845a483fae4be7e341368e36-Abstract.html)

#### R11 Decomposition of Uncertainty in Bayesian Deep Learning for Efficient and Risk-sensitive Learning

Stefan Depeweg et al. (2018) ICML 2018, PMLR 80:1184–1193  
優先度 S 確認 本文

**概要** 潜在変数を持つBayesian neural networkにより予測のaleatoricとepistemic uncertaintyを分解し、active learningとrisk-sensitive model-based RLに用いる。model-bias回避とnoise回避を別に重み付けする。

**本研究との関係** threat=failure probability+uncertaintyという設計は、不確実性の種類を分離する必要がある。未知で学習可能な安全領域、既知の危険、予測不能だが無害なnoise領域を別条件にして評価する根拠。

**適用限界** Bayesianモデルでの分解方法の論文。ensemble disagreementはそのまま校正済み確率ではない。aleatoric uncertainty自体をdangerと同義にしない。

[原典 https://proceedings.mlr.press/v80/depeweg18a.html](https://proceedings.mlr.press/v80/depeweg18a.html)

#### R12 Benchmarking Safe Exploration in Deep Reinforcement Learning

Alex Ray et al. (2019) Technical report / arXiv:1910.01708  
優先度 A 確認 抄録と書誌

**概要** safe explorationの共通定式化としてconstrained RLを提案し、Safety Gym環境と複数のconstrained deep RLのbaselineを提示する。

**本研究との関係** 学習中の違反と学習後の方策costを分け、rewardと安全costを別指標として追跡する標準的な評価枠組みを参照する。GridWorldから連続制御へ発展する際の橋渡し。

**適用限界** Safety Gymでの性能は現実の無条件な安全保証ではない。今回確認したのは著者機関の公開抄録。

[原典 https://arxiv.org/abs/1910.01708](https://arxiv.org/abs/1910.01708)

#### R13 Safety Gymnasium: A Unified Safe Reinforcement Learning Benchmark

Jiaming Ji et al. (2023) NeurIPS 2023, Datasets and Benchmarks Track  
優先度 A 確認 抄録と書誌

**概要** 単一/複数agent、ベクトル/vision-only入力を含む安全RL環境と、16手法を収録するSafe Policy Optimizationライブラリを提供。

**本研究との関係** 独自GridWorldでの因果比較が確認できた後、既存benchmarkでも効果があるかを評価する候補。既存安全RLとの再現可能な比較を組みやすい。

**適用限界** 現在の計画に全benchmarkを追加する必要はなく、局所観測とpersistent stateの検証を保てるtaskを選ぶ。著者名はNeurIPS公式の現行表記Josef Daiを使用。抄録確認のみ。

[原典 https://papers.nips.cc/paper/2023/hash/3c557a3d6a48cc99444f85e924c66753-Abstract-Datasets_and_Benchmarks.html](https://papers.nips.cc/paper/2023/hash/3c557a3d6a48cc99444f85e924c66753-Abstract-Datasets_and_Benchmarks.html)

#### R14 SHAPO: Sharpness-Aware Policy Optimization for Safe Exploration

Kaustubh Mani et al. (2026) ICLR 2026  
優先度 B 確認 本文

**概要** actorのparameter perturbation感度をepistemic uncertaintyのproxyとし、摂動先で勾配を評価する悲観的な方策更新を提案。稀なunsafe actionを重視し、Safety Gym/MuJoCoで安全と効率のPareto frontierを評価。

**本研究との関係** 安全改善が内部状態に由来するのか、単に学習updateを保守的にすることで達成できるのかを考える最新対照。平均違反だけでなくepisode costのheavy tailにも注目する。

**適用限界** 感度proxyをそのまま校正済みuncertaintyやfailure probabilityと解釈しない。感情状態の提案ではなくactor updateの変更。証明の検算と全実験精読は未実施。

[原典 https://proceedings.iclr.cc/paper_files/paper/2026/hash/5cfbaa614adaf59bffc697cb0844143b-Abstract-Conference.html](https://proceedings.iclr.cc/paper_files/paper/2026/hash/5cfbaa614adaf59bffc697cb0844143b-Abstract-Conference.html)

#### R15 Sampling-Based Safe Reinforcement Learning

Luca Vignola et al. (2026) arXiv preprint, arXiv:2605.19469  
優先度 B 確認 本文

**概要** 複数のsampled dynamicsについて同時に安全制約を満たす方策を選ぶSBSRL。epistemic uncertaintyに対する制約で十分な情報収集を要求し、明示的exploration reward bonusを使わず探索を誘導する。GPの仮定付き保証と実機評価を提示。

**本研究との関係** rewardに好奇心を足す以外にも、安全と情報収集を制約として同時に扱う選択肢がある。reward/state/bothという配置比較だけでなく、探索制約という別の実装群を見渡すための最新文献。

**適用限界** 今回確認した公開版はpreprint。GP理論とneural ensembleの実用版を区別。本文は有限horizon episode・resetの必要性、期待累積cost制約の限界を明記している。

[原典 https://arxiv.org/abs/2605.19469](https://arxiv.org/abs/2605.19469)

### 6.4 人間による行動評価と統計

#### H01 Cautious Curiosity: A Novel Approach to a Human-Like Gameplay Agent

Chujin Zhou; Tiago Machado; Casper Harteveld (2023) AIIDE 19(1), 370–379  
優先度 必読・直接類似 確認 本文

**概要** ICMの予測誤差に逆V型の内発報酬を与えるMarioエージェントを開発。100人の動画評価で比較AIより人間らしく見えると報告した。

**本研究との関係** 内発報酬、行動、人間の印象を結ぶ直接的な類似研究。危険への慎重さを独立操作する計画との差を検討する。

**適用限界** cautiousは危険コストや恐怖状態ではなく未知すぎる対象への報酬低下。効果量ε²=.0335は弱く、人間との差が非有意でも等価性は示さない。

[原典 https://doi.org/10.1609/aiide.v19i1.27533](https://doi.org/10.1609/aiide.v19i1.27533)

#### H02 Navigates Like Me: Understanding How People Evaluate Human-Like AI in Video Games

Stephanie Milani et al. (2023) CHI ’23, 18 pages  
優先度 必読・直接類似 確認 本文

**概要** 3D移動AIを動画の対比較、自由記述、確信度で評価。報酬整形したAIは著者定義の人間らしさテストを通過し、判断手掛かりも分析した。

**本研究との関係** 印象評定に加えて理由を集める根拠。滑らかさ、環境への反応、目的性、速度などの交絡と教示の明確化を検討する。

**適用限界** 現実の人間の移動と人間がゲームを操作した移動が異なる解釈を生んだ。特定の第三者視点ナビゲーションからの一般化に限界。

[原典 https://doi.org/10.1145/3544548.3581348](https://doi.org/10.1145/3544548.3581348)

#### H03 Legibility and Predictability of Robot Motion

Anca D. Dragan; Kenton C. T. Lee; Siddhartha S. Srinivasa (2013) HRI ’13, 301–308  
優先度 必読・知覚評価 確認 本文

**概要** 軌跡から目的を読み取れるlegibilityと、既知の目的に対して期待される動きに一致するpredictabilityを区別し、両者が対立する例を検証した。

**本研究との関係** 好奇心や慎重さを行動から読み取れることと、次の動きを予測できることを別々に測る評価設計の理論的根拠となる。

**適用限界** ロボットの目標推定が対象。GridWorldの情動状態知覚への適用は本研究計画で今後検証する拡張であり、既存結果から直接保証されない。

[原典 https://doi.org/10.1109/HRI.2013.6483603](https://doi.org/10.1109/HRI.2013.6483603)

#### H04 Dimensions of Mind Perception

Heather M. Gray; Kurt Gray; Daniel M. Wegner (2007) Science 315(5812), 619  
優先度 必読・構成概念 確認 本文

**概要** 人間や非人間の心の知覚を比較し、計画や自己制御などのAgencyと、恐怖や苦痛を感じる能力などのExperienceという2次元を示した。

**本研究との関係** 慎重な方策、恐怖を感じているように見えること、意識の帰属を分ける。行動制御と感情の知覚を一つの尺度にまとめない。

**適用限界** 知覚される心の次元を扱う研究であり、AIが実際に感情や意識を持つことを示すものではない。

[原典 https://doi.org/10.1126/science.1134475](https://doi.org/10.1126/science.1134475)

#### H05 On Seeing Human: A Three-Factor Theory of Anthropomorphism

Nicholas Epley; Adam Waytz; John T. Cacioppo (2007) Psychological Review 114(4), 864–886  
優先度 高・知覚の理論 確認 抄録と書誌

**概要** 擬人化を、人間に関する知識の利用しやすさ、相手の行動を理解したい動機、社会的なつながりを求める動機という3要因から説明する。

**本研究との関係** 観察者の性向や事前説明が印象を変える可能性を整理する。条件名を見せず、教示を揃え、参加者側の差も検討する。

**適用限界** 擬人化の理論枠組みであり、好奇心や慎重さの特定尺度、RLエージェントへの効果を直接検証した研究ではない。

[原典 https://doi.org/10.1037/0033-295X.114.4.864](https://doi.org/10.1037/0033-295X.114.4.864)

#### H06 Measurement Instruments for the Anthropomorphism, Animacy, Likeability, Perceived Intelligence, and Perceived Safety of Robots

Christoph Bartneck et al. (2009) International Journal of Social Robotics 1(1), 71–81  
優先度 高・評価尺度 確認 本文

**概要** ロボットの擬人化、生命感、好感、知能、安全性の知覚を測るGodspeed質問紙を提案し、複数の実証研究による信頼性と妥当性の指標を示した。

**本研究との関係** 人間らしさなどを補助評価する尺度の候補。好奇心と慎重さの主尺度を別途定義する必要性を明確にする。

**適用限界** 好奇心、慎重さ、信頼の直接尺度ではない。GridWorldへの表現変更や項目改変後に原尺度の妥当性をそのまま主張できない。

[原典 https://doi.org/10.1007/s12369-008-0001-3](https://doi.org/10.1007/s12369-008-0001-3)

#### H07 Trust in Automation: Designing for Appropriate Reliance

John D. Lee; Katrina A. See (2004) Human Factors 46(1), 50–80  
優先度 高・信頼の理論 確認 抄録と書誌

**概要** 自動化への信頼と依存の関係を整理し、システムの能力や利用文脈に合った適切な依存を支援するための概念モデルと設計の観点を示す。

**本研究との関係** 信頼の最大化を目的にせず、好感、安心感、信頼、委任を区別する。信頼を副次評価にする際の仮説設定に用いる。

**適用限界** 信頼と依存は同一ではない。受動的な動画評定だけでは、能力に対して適切に依存できるかまで評価できない。

[原典 https://doi.org/10.1518/hfes.46.1.50_30392](https://doi.org/10.1518/hfes.46.1.50_30392)

#### H08 Trust in Automation: Integrating Empirical Evidence on Factors That Influence Trust

Kevin Anthony Hoff; Masooda Bashir (2015) Human Factors 57(3), 407–434  
優先度 中・体系的レビュー 確認 抄録と書誌

**概要** 101論文127研究を統合し、自動化への信頼の変動を個人の性向、状況、経験から学習された信頼という3層に整理した体系的レビュー。

**本研究との関係** 一度の観察による印象と、成功や失敗を繰り返し経験して形成される信頼を区別する。後続の長期評価への設計指針になる。

**適用限界** レビュー対象は2002年から2013年。単純な動画観察課題と、目的達成のために自動化と相互作用する課題では適用範囲が異なる。

[原典 https://doi.org/10.1177/0018720814547570](https://doi.org/10.1177/0018720814547570)

#### H09 Foundations for an Empirically Determined Scale of Trust in Automated Systems

Jiun-Yin Jian; Ann M. Bisantz; Colin G. Drury (2000) International Journal of Cognitive Ergonomics 4(1), 53–71  
優先度 中・信頼尺度 確認 抄録と書誌

**概要** 語の抽出、質問紙、対比較という3段階の実験により、信頼と不信や対象の異なる信頼の共通性を調べ、自動化への信頼尺度の基盤を作った。

**本研究との関係** 信頼を副次指標として測る場合の尺度候補。項目の適用範囲を確認し、印象と実際の依存行動を分ける。

**適用限界** 動画視聴だけで実際の委任に関する信頼を測る際には適用上のずれが残る。検索の同名誤表示を避け、DOI末尾_04を用いる。

[原典 https://doi.org/10.1207/S15327566IJCE0401_04](https://doi.org/10.1207/S15327566IJCE0401_04)

#### H10 The Mind in the Machine: Anthropomorphism Increases Trust in an Autonomous Vehicle

Adam Waytz; Joy Heafner; Nicholas Epley (2014) Journal of Experimental Social Psychology 52, 113–117  
優先度 中・信頼と擬人化 確認 本文

**概要** 100人の運転シミュレータ実験で同じ自動運転機能に名前、性別、声を付加。擬人化条件で総合および行動的な信頼指標が高くなった。

**本研究との関係** 行動以外の表示や名前も信頼に影響する。好奇心と慎重さの比較では外見、名前、音声、説明文を統一する必要がある。

**適用限界** 擬人化対自動運転のみの条件で自己報告信頼の差は非有意(p=.14)。人間らしさの向上が全ての信頼尺度を高めるとは言えない。

[原典 https://doi.org/10.1016/j.jesp.2014.01.005](https://doi.org/10.1016/j.jesp.2014.01.005)

#### H11 An Experimental Study of Apparent Behavior

Fritz Heider; Marianne Simmel (1944) The American Journal of Psychology 57(2), 243–259  
優先度 中・古典的基礎 確認 本文

**概要** 幾何学図形が動く映像を観察した人々が、図形に人格、意図、恐怖などを帰属する様子を調べ、動きや場面の構成が解釈に関与することを示した。

**本研究との関係** 単純な表示でも行動から感情や意図を読む評価は成立しうる。感情の存在を先に教示せず、帰属の誘導を抑える設計の根拠となる。

**適用限界** 古典的な限定的参加者集団と特定映像の研究。一般的なRL方策や現代のAI知識を持つ参加者への結果を直接保証しない。

[原典 https://www.jstor.org/stable/1416950](https://www.jstor.org/stable/1416950)

#### H12 Deep Reinforcement Learning That Matters

Peter Henderson et al. (2018) AAAI-18, 3207–3214  
優先度 高・再現性と評価方法 確認 本文

**概要** 学習seed、ハイパーパラメータ、実装、環境の変動が深層RLの結果比較に及ぼす影響を調べ、有意性と実験報告の標準化の必要性を示した。

**本研究との関係** 各条件1体や選んだ代表動画だけで結論を出さず、複数seedと複数環境で客観指標と知覚指標の安定性を検証する。

**適用限界** 主に連続制御の方策勾配法が対象。必要なseed数や効果量は本課題の分散と計算予算に応じて設計する必要がある。

[原典 https://doi.org/10.1609/aaai.v32i1.11694](https://doi.org/10.1609/aaai.v32i1.11694)

#### H13 Deep Reinforcement Learning at the Edge of the Statistical Precipice

Rishabh Agarwal et al. (2021) NeurIPS 34  
優先度 高・統計評価 確認 本文

**概要** 少数の学習runの平均や中央値だけではRLの比較結論が不安定になることを示し、信頼区間、性能プロフィール、中央50%の平均（IQM）とrliableを提案した。

**本研究との関係** 客観指標はseed間の不確かさを報告し、複数マップの集約も単一平均順位だけで判断しない。再現可能な比較の方法を学ぶ。

**適用限界** 複数タスクの性能集約が主対象。参加者と動画の反復評定は別の統計モデルが必要で、rliableだけでは扱えない。

[原典 https://papers.neurips.cc/paper_files/paper/2021/hash/f514cec81cb148559cf475e7426eed5e-Abstract.html](https://papers.neurips.cc/paper_files/paper/2021/hash/f514cec81cb148559cf475e7426eed5e-Abstract.html)

### 6.5 報酬理論 記憶 人間の探索 多目的評価

#### X01 Realization of Efficient Exploration by Self-Generating Evaluation Considering Curiosity and Fear Indices Based on Prediction Error

Kazusato Okada; Kentarou Kurashige (2025) Applied Sciences 15(22), 12023  
優先度 S 確認 索引と書誌

**概要** センサ入力を評価して内発的報酬を生成し、予測誤差の時間変化からcuriosityとfearを計算する方法を提案。

**本研究との関係** 計画に挙げた直接的先行研究。発表中のTwo Measures Curiosity and Fearは説明用の見出しで、正式な論文題名ではない。引用には本項の正式題名を用いる。

**適用限界** 本項は著者機関の書誌と出版社の索引・抄録断片に基づく。更新式、脅威の意味、人間評価や配置比較の実施範囲は本文精読で確定する。予測不能性と物理的危険を同義にしない。

[原典 https://doi.org/10.3390/app152212023](https://doi.org/10.3390/app152212023)

#### X02 Policy Invariance Under Reward Transformations: Theory and Application to Reward Shaping

Andrew Y. Ng; Daishi Harada; Stuart Russell (1999) ICML 1999  
優先度 A 確認 抄録と書誌

**概要** 元の最適方策を保存する報酬変換の条件を示し、ポテンシャル差によるreward shapingを定式化する。

**本研究との関係** 感情由来の報酬で目的自体を変える条件と、学習を促進しながら元の目的を保つ参照条件を分ける基礎。

**適用限界** 一般の感情報酬へ最適方策保存の結論は移らない。状態の定義、割引率、終端ポテンシャルを確認する。本項の内容は著者公開の書誌・論文抄録中心。

[原典 https://people.eecs.berkeley.edu/~pabbeel/cs287-fa09/readings/NgHaradaRussell-shaping-ICML1999.pdf](https://people.eecs.berkeley.edu/~pabbeel/cs287-fa09/readings/NgHaradaRussell-shaping-ICML1999.pdf)

#### X03 Dynamic Potential-Based Reward Shaping

Sam Devlin; Daniel Kudenko (2012) AAMAS 2012  
優先度 A 確認 本文

**概要** 時間とともに変化するポテンシャルを、訪問時点の値の差として扱い、方策不変性を維持する拡張を証明・実験する。

**本研究との関係** 推定器をオンライン更新する感情報酬では、静的ポテンシャルの議論だけでなく時間依存の扱いが必要。

**適用限界** 任意の非定常な感情重みを加えてよいという意味ではない。履歴状態・学習器更新と原論文の仮定を照合する。

[原典 https://www.ifaamas.org/Proceedings/aamas2012/papers/2C_3.pdf](https://www.ifaamas.org/Proceedings/aamas2012/papers/2C_3.pdf)

#### X04 Deep Recurrent Q-Learning for Partially Observable MDPs

Matthew Hausknecht; Peter Stone (2015) AAAI Fall Symposium on Sequential Decision Making for Intelligent Agents  
優先度 A 確認 抄録と書誌

**概要** DQNに再帰的ネットワークを導入し、現在の観測だけでは不十分な課題で、過去情報を方策へ利用する。

**本研究との関係** 内部感情状態の履歴が、一般的な記憶機構と比べて何を加えるかを調べる基礎比較。局所観測のGridWorldは部分観測性を明示する。

**適用限界** 記憶の導入が常に優位とは限らない。入力系列、隠れ状態のリセット、容量・計算量・訓練方法を揃える。

[原典 https://arxiv.org/abs/1507.06527](https://arxiv.org/abs/1507.06527)

#### X05 Recurrent Model-Free RL Can Be a Strong Baseline for Many POMDPs

Tianwei Ni; Benjamin Eysenbach; Ruslan Salakhutdinov (2022) ICML 2022, PMLR 162:16691–16723  
優先度 S 確認 抄録と書誌

**概要** 設計とハイパーパラメータを調整した再帰型model-free RLが、複数の部分観測課題で専用手法に匹敵・上回ることを示す。

**本研究との関係** 感情状態ありを記憶なしMLPだけと比較すると、履歴の恩恵を感情の恩恵と解釈しかねない。強い非感情の記憶baselineが必要。

**適用限界** 論文の結果は対象ベンチマークでの比較。任意のPOMDPで最良という意味ではない。最低限のGRU対照の設計を検討する。

[原典 https://proceedings.mlr.press/v162/ni22a.html](https://proceedings.mlr.press/v162/ni22a.html)

#### X06 POPGym: Benchmarking Partially Observable Reinforcement Learning

Steven Morad et al. (2023) ICLR 2023  
優先度 A 確認 本文

**概要** 多様な部分観測課題と記憶モデルを比較する。ナビゲーション課題だけでは記憶性能の優劣が見えにくいことも指摘する。

**本研究との関係** 履歴状態の評価に、本当に履歴が必要な場面を入れる根拠。再遭遇、隠れた危険、過去の失敗を記憶しなければ解けない地図が候補。

**適用限界** 多数の課題を第一段階へ追加する必要はない。局所観測にしただけで記憶効果が検出できるとは限らない。

[原典 https://arxiv.org/abs/2303.01859](https://arxiv.org/abs/2303.01859)

#### X07 Humans Use Directed and Random Exploration to Solve the Explore–Exploit Dilemma

Robert C. Wilson et al. (2014) Journal of Experimental Psychology General 143(6), 2074–2081  
優先度 A 確認 本文

**概要** 人間の探索を、情報を求める方向づけられた探索と、選択のランダム性による探索へ分け、意思決定の残り時間によって両者が変わることを示す。

**本研究との関係** coverageだけでは、未知を知ろうとする行動と単なる行動ノイズを区別できない。情報獲得、再訪、活動切替も観察する。

**適用限界** 人間のbandit課題の結果をGridWorldへ転用する際は仮説として扱う。好奇心の単一機構を証明した論文ではない。

[原典 https://pmc.ncbi.nlm.nih.gov/articles/PMC5635655/](https://pmc.ncbi.nlm.nih.gov/articles/PMC5635655/)

#### X08 Deconstructing the human algorithms for exploration

Samuel J. Gershman (2018) Cognition 173, 34–42  
優先度 B 確認 抄録と書誌

**概要** 不確実性に基づく方向づけられた探索とランダム探索を分解し、両者を含むモデルで人間の選択を説明する。

**本研究との関係** 観察者が感じる好奇心と、実際の情報探索アルゴリズムの働きを区別する。探索指標を複数用意する背景となる。

**適用限界** banditの選択モデルであり、感情状態の実装や安全性を直接検証していない。

[原典 https://gershmanlab.com/pubs/Gershman18.pdf](https://gershmanlab.com/pubs/Gershman18.pdf)

#### X09 Computations of uncertainty mediate acute stress responses in humans

Archy O. de Berker et al. (2016) Nature Communications 7, 10996  
優先度 A 確認 本文

**概要** 確率的な脅威予測課題で、学習モデルから推定した不確実性と主観・生理的ストレスの動態の対応を示す。

**本研究との関係** 脅威評価を失敗確率だけでなく不確実性と関連づける心理学的根拠。脅威が存在する文脈での不確実性という条件を保持する。

**適用限界** ストレスと不安・恐怖は同一ではない。無害な観測ノイズすべてが脅威になると解釈してはいけない。

[原典 https://www.nature.com/articles/ncomms10996](https://www.nature.com/articles/ncomms10996)

#### X10 Motivationally selective risk judgments: Do fear and curiosity boost the boons or the banes?

Jon K. Maner; Mary A. Gerend (2007) Organizational Behavior and Human Decision Processes 103(2), 256–267  
優先度 B 確認 抄録と書誌

**概要** 接近・回避に関連する動機や感情が、選択の正・負の結果の評価と選択的に関わるかを調べる。

**本研究との関係** 好奇心と恐怖を併用する心理学的背景として読む。リスクの知覚と、実際に生じるリスクを分ける。

**適用限界** 本調査では抄録・書誌中心。人工エージェントに同じ心理機構が存在することを示す研究ではない。

[原典 https://doi.org/10.1016/j.obhdp.2006.08.002](https://doi.org/10.1016/j.obhdp.2006.08.002)

#### X11 A Survey of Multi-Objective Sequential Decision-Making

Diederik M. Roijers et al. (2013) Journal of Artificial Intelligence Research 48, 67–113  
優先度 B 確認 抄録と書誌

**概要** 複数目的の逐次意思決定を、スカラー化や必要な方策集合の違いによって分類する。Pareto frontと凸包の違いを整理する。

**本研究との関係** 探索と安全の重み走査で得られる集合を、真のPareto frontと自動的に呼ばないための基礎。

**適用限界** 総説であり感情状態の原著実証ではない。単純な線形重み和だけでは非凸なfrontの全体を回収できない場合がある。

[原典 https://www.cs.ox.ac.uk/people/shimon.whiteson/pubs/roijersjair13.pdf](https://www.cs.ox.ac.uk/people/shimon.whiteson/pubs/roijersjair13.pdf)

#### X12 A practical guide to multi-objective reinforcement learning and planning

Conor F. Hayes et al. (2022) Autonomous Agents and Multi-Agent Systems 36, 26  
優先度 A 確認 本文

**概要** 目的のスカラー化、方策選択、評価指標、ベンチマークなど、複数目的RLを実際に研究するための設計判断を整理する。

**本研究との関係** 同じ安全水準での探索、同じ探索水準での安全、hypervolumeの参照点を定義する際に読む。重み探索予算も比較条件に含める。

**適用限界** ガイド・総説として扱う。目的の単位・向き・尺度が違うと、重みや集約指標の解釈が変わる。

[原典 https://doi.org/10.1007/s10458-022-09552-y](https://doi.org/10.1007/s10458-022-09552-y)
