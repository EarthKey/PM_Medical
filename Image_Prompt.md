# 「あなたが繰り返すミスのクセ診断」画像生成用プロンプト設計書（調剤・監査・確認業務編）

本診断サイトの結果ページにおいて、診断結果の「補助教材（NG/OK比較図）」として挿入する画像を生成するためのビジュアル設計書である。
画像生成は**ChatGPT（DALL-E 3）**のブラウザ版で実行することを前提とし、そのままコピペして使える高精度な英語プロンプトを定義している。

> [!IMPORTANT]
> **結果ページと教材画像の分離設計（Harvard Business Review風の実現）**
> - **HTMLで実装するもの**: タイプ名、キャッチコピー、スコア、レーダーチャート、振り返りメモ（localStorage保存）、印刷用レイアウト（PDF）、シェアボタン、行動改善チェックリスト。
> - **画像で生成するもの**: タイプ解説用の「NG/OK比較図」のみ。1タイプにつき「左右対比の1枚画像」とし、全6タイプ＝6枚の画像で完結させる（12枚ではなく6枚に集約し、運用・保守性を最大化する）。


## 1. ビジュアル共通仕様（トンマナ）

診断結果の「少し痛い指摘」をマイルドにしつつ、読者が「自分ごと」として親しみを持って受け入れられるよう、以下の仕様で統一する。

- **基本比率**: 横長 4:3（診断結果ページ、OGP画像、スライド転用に最適）
- **レイアウト**: 左右分割の2画面対比構成（**左半分にNGシーン、右半分にOKシーン**）
- **境界線**: 中央に薄い縦の境界線（A thin vertical divider）を配置
- **スタイル**: 手書き色鉛筆風（Colored pencil style, soft illustration, gentle hand-drawn texture, white background）
- **トーン**: 柔らかいパステル調、温かみのあるライティング（Soft pastel colors, warm lighting）
- **場所**: 薬局または病院薬剤部の調剤・監査スペース（Dispensing/auditing workspace in a pharmacy, clean white counter shelves with medicine boxes in the background）
- **主役**: 薬剤師1名（A single pharmacist, wearing a white medical scrub or lab coat）
- **対象物**: 処方箋（prescription）、薬袋（medicine bag）、薬剤（tablet sheets）、患者情報（patient details sheet）、監査画面（audit screen）、メモ（memo/sticky note）
- **テーマ**: 調剤・監査・確認業務で起こる「思考のクセ」（Cognitive biases and habits during dispensing, checking, and auditing tasks）
- **文字**: 最小限（左上に「NG」、右上に「OK」とだけシンプルに描画させる）

---

## 2. 画像プロンプト設計ステップ
1. **タイプ名を決める**: 診断するバイアスタイプ
2. **NG行動を1つ決める**: やりがちな業務上の失敗や見落とし（思考のクセ）
3. **OK行動を1つ決める**: 明日からの改善・確認行動
4. **場面を決める**: 調剤台、監査台、監査画面の前など
5. **登場人物を決める**: 薬剤師1名（白衣/スクラブ）の性別・外見
6. **表情を決める**: NG側の「焦り・思い込み・戸惑い」、OK側の「丁寧・納得・冷静」
7. **構図を決める**: 左右2分割（左NG・右OK）の4:3レイアウト、中央の仕切り線
8. **文字を入れるか決める**: 左上に「NG」、右上に「OK」のラベルのみ
9. **画像生成プロンプトに変換する**: DALL-E 3用の英語テキスト

---

## 3. タイプ別 左右対比プロンプト（全6枚）

---

### 🔥 No.1 ペースセッター型（スピード優先・流し読み型）
- **NG行動**: スピードを最優先し、処方箋の文字を流し読みして監査画面をしっかり確認せず完了ボタンを押そうとする。
- **OK行動**: 1ステップずつ処方箋と監査画面を指差し確認（指差し呼称）し、現物と画面を冷静に突合する。
- **登場人物**: 20代後半の女性薬剤師（スクラブ着用）
- **コピペ用プロンプト**:
  ```text
  A side-by-side split-screen illustration with an aspect ratio of 4:3, showing a comparison of dispensing tasks in a pharmacy. Hand-drawn colored pencil style, soft warm pastel colors, clean dispensing background. A single female pharmacist is the subject.
  - Left side (labeled "NG" at the top in simple text): The young female pharmacist looks stressed and rushed, briefly skimming a paper prescription while holding a tablet pack, her hand hovering over a computer audit screen to click confirm without looking closely at the details.
  - Right side (labeled "OK" at the top in simple text): The same pharmacist with a calm expression, using her finger to point at the prescription sheet and then the computer screen one by one to verify each detail carefully (point-and-call method).
  A thin vertical divider separates the two scenes. No other text.
  ```

---

### 🧭 No.2 コーチ型（放置・見守りすぎ型）
- **NG行動**: 後輩の調剤トレイに規格違いのミスがあるのを見ながら、横で「自分で気づくかな…」と何も介入せず黙って見守り（放置）続ける。
- **OK行動**: 違和感に気づいた時点で、「これ、規格を確認してみようか」と後輩のトレイを優しく指さして声をかける。
- **登場人物**: 30代後半の男性薬剤師（白衣着用）
- **コピペ用プロンプト**:
  ```text
  A side-by-side split-screen illustration with an aspect ratio of 4:3, comparing checking methods in a pharmacy. Hand-drawn colored pencil style, soft pastel tones. A single male pharmacist is the subject.
  - Left side (labeled "NG" at the top in simple text): The male pharmacist stands next to a messy dispensing tray with incorrect medicine boxes, looking at them silently with folded arms, observing and overthinking without stepping in to correct the error, letting the mistake pass.
  - Right side (labeled "OK" at the top in simple text): The same pharmacist smiles warmly, pointing gently at a specific medicine box on the tray to call attention to it and guide the other person's eyes to the detail.
  A thin vertical divider separates the two scenes. No other text.
  ```

---

### ⚡ No.3 強制型（思い込み・決めつけ型）
- **NG行動**: 「この医師の処方はいつもこうだから」と過去の記憶だけで決めつけ、処方箋に新しく書かれた規格変更を見落として調剤してしまう。
- **OK行動**: 先入観を捨て、目の前の処方箋の記載と医薬品添付文書（または監査画面）をニュートラルに照合する。
- **登場人物**: 眼鏡をかけた男性薬剤師（スクラブ着用）
- **コピペ用プロンプト**:
  ```text
  A side-by-side split-screen illustration with an aspect ratio of 4:3. Soft colored pencil drawing style, warm cozy lighting in a pharmacy setting. A single male pharmacist with glasses is the subject.
  - Left side (labeled "NG" at the top in simple text): The pharmacist confidently grabs a medicine bottle from a shelf based on memory, thinking "It must be the usual dosage," while a paper prescription sheet with a different dosage lies neglected on the desk.
  - Right side (labeled "OK" at the top in simple text): The same pharmacist with a neutral and objective face, carefully comparing the text on the prescription sheet directly with a drug reference document on a clipboard.
  A thin vertical divider separates the two scenes. No other text.
  ```

---

### 💛 No.4 関係重視型（疑義照会ためらい型）
- **NG行動**: 処方に明らかな疑問点があるが、忙しそうな医師の機嫌を損ねるのを恐れて電話（疑義照会）を躊躇し、そのまま監査を通そうとする。
- **OK行動**: 疑義確認の要点をメモに書き出して頭を整理し、冷静かつハキハキと電話をかけて確認する。
- **登場人物**: 20代の若い女性薬剤師（スクラブ着用）
- **コピペ用プロンプト**:
  ```text
  A side-by-side split-screen illustration with an aspect ratio of 4:3. Soft colored pencil style, warm pastel colors. A single young female pharmacist is the subject.
  - Left side (labeled "NG" at the top in simple text): The female pharmacist looks anxious and hesitant, staring at a telephone receiver in her hand, looking at a busy clinic logo or schedule, afraid of calling to double-check a suspicious prescription.
  - Right side (labeled "OK" at the top in simple text): The pharmacist looks determined and calm, looking at a neat checklist/sticky note she prepared, confidently speaking into the telephone to make a clear inquiry.
  A thin vertical divider separates the two scenes. No other text.
  ```

---

### 🔮 No.5 先見型（先読み・ビジョン先行型）
- **NG行動**: 「この患者は将来この治療へ移行するはず」と頭の中で治療ビジョンを先読みしすぎて、手元の「現在の処方箋」の数量間違いや規格ミスを見落とす。
- **OK行動**: 未来の予測と「今、目の前にある処方」を明確に区別し、手元の錠剤シートの数量を確実に数えて確認する。
- **登場人物**: 30代の男性薬剤師（白衣着用）
- **コピペ用プロンプト**:
  ```text
  A side-by-side split-screen illustration with an aspect ratio of 4:3. Hand-drawn colored pencil style, pharmacy setting. A single male pharmacist is the subject.
  - Left side (labeled "NG" at the top in simple text): The pharmacist looks up thoughtfully at a large medical diagram or poster on the wall showing a patient's future health roadmap, completely failing to notice that the drug packets on his counter are mismatched in quantity.
  - Right side (labeled "OK" at the top in simple text): The pharmacist focuses on the present, looking down at his desk and carefully counting the actual tablet sheets, matching the numbers exactly with the paper prescription.
  A thin vertical divider separates the two scenes. No other text.
  ```

---

### 🗳️ No.6 民主型（決断回避・判断先延ばし型）
- **NG行動**: イレギュラーな処方について周囲の同僚全員の意見を聞き回るだけで、自分で判断を下せず、未監査のまま作業を滞らせる。
- **OK行動**: 手順書（SOP）を確認し、最終判断を仰ぐべき責任者に直接処方箋を見せて速やかに解決する。
- **登場人物**: 30代の女性薬剤師（スクラブ着用）
- **コピペ用プロンプト**:
  ```text
  A side-by-side split-screen illustration with an aspect ratio of 4:3. Soft colored pencil style, gentle hand-drawn texture. A single female pharmacist is the subject.
  - Left side (labeled "NG" at the top in simple text): The female pharmacist looks overwhelmed and confused, holding a prescription sheet and looking around at multiple busy colleagues, unable to make a decision and letting the papers pile up.
  - Right side (labeled "OK" at the top in simple text): The same pharmacist holding the prescription, checking a Standard Operating Procedure (SOP) manual on a shelf, and directly presenting it to the chief pharmacist for a swift final decision.
  A thin vertical divider separates the two scenes. No other text.
  ```
