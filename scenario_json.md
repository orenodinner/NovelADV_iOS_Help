### シナリオテンプレート JSON 仕様書

#### 1. 概要
`NovelADV` が新規プロジェクトの土台として読み込む「シナリオテンプレート」を定義するJSONです。世界設定、文体、オープニング、キャラクター初期値、謎・伏線の初期リストなど、物語の方向性を決める要素を含みます。

#### 2. JSONフォーマット
```json
{
  "name": "テンプレート名",
  "settingPlace": "物語の主な舞台",
  "settingEra": "時代設定",
  "settingBackground": "世界観や背景ストーリー",
  "writingStyle": "AIが使う描写スタイル",
  "openingScene": "物語開始時に表示する導入文",
  "mysteryScale": 3,
  "mysteries": [
    {
      "content": "謎・伏線の概要",
      "truth": "真相（プレイヤーには秘匿）",
      "status": "unresolved",
      "resolutionPeriod": 8
    }
  ],
  "characters": [
    {
      "name": "キャラクター名",
      "gender": "性別・種別",
      "job": "職業/役割",
      "firstPerson": "一人称",
      "playerAlias": "主人公の呼び方",
      "personality": "性格・口調・価値観",
      "content": "背景や秘密",
      "relationshipWithPlayer": "主人公との初期関係",
      "recentEvents": "物語直前の出来事",
      "isPlayerCharacter": true
    }
  ]
}
```

#### 3. ルートオブジェクト フィールド詳細
| キー | 型 | 必須 | 説明・入力ヒント |
| :--- | :--- | :--- | :--- |
| `name` | String | 必須 | テンプレート名。シナリオのテーマが分かるタイトルにしてください。例: 「雨の探偵社」「塔の魔術師」 |
| `settingPlace` | String | 任意 | 主な舞台。情景が浮かぶ具体的な場所を推奨。例: 「常に霧が出る港町」「軌道エレベーター内部」 |
| `settingEra` | String | 任意 | 時代/テクノロジーレベル。例: 「近未来」「大正末期」「剣と魔法の時代」 |
| `settingBackground` | String | 任意 | 世界観や導入背景。プレイヤーが何をすべきかが分かるよう簡潔に。 |
| `writingStyle` | String | 任意 | AIの描写スタイル。例: 「ハードボイルドで簡潔」「三人称で叙情的」 |
| `openingScene` | String | 任意 | 最初に表示する導入文またはNPCの初回発話。 |
| `mysteryScale` | Number(1-5) | 任意 | 1=日常〜5=コズミックホラーのリアリティ/謎レベル。未指定なら既定値3。 |
| `mysteries` | Array<Object> | 任意 | 初期の謎・伏線リスト。`resolutionPeriod` が近づくと解決を促す指示が入ります。 |
| `characters` | Array<Object> | 任意 | 初期登場キャラクター。最低1人はPCにすることを推奨。 |

`mysteries` オブジェクト: `status` は `unresolved` または `resolved`。`truth` はプレイヤーには見せない真相テキストで、AIの裏指示に使われます。

#### 4. `characters` 配列オブジェクト詳細
| キー | 型 | 必須 | 説明・入力ヒント |
| :--- | :--- | :--- | :--- |
| `name` | String | 必須 | キャラクター名 |
| `gender` | String | 任意 | 性別/種別。例: 「男性」「女性」「中性」「AI」「妖精」 |
| `job` | String | 任意 | 役職や物語での役割 |
| `firstPerson` | String | 任意 | 一人称。口調の手がかりにします |
| `playerAlias` | String | 任意 | 主人公を呼ぶときの二人称 |
| `personality` | String | 任意 | 性格・口調・価値観・行動原理など。箇条書き推奨 |
| `content` | String | 任意 | 背景や秘密。AIが裏で保持する設定 |
| `relationshipWithPlayer` | String | 任意 | 物語開始時点での関係性。例: 「幼馴染」「初対面」 |
| `recentEvents` | String | 任意 | 直前に起きた出来事。導入のフックに活用 |
| `isPlayerCharacter` | Boolean | 必須 | 主人公なら `true`。PCは1人のみを推奨 |

#### 5. 具体的なJSON例
```json
{
  "name": "サイバーパンク探偵の事件簿",
  "settingPlace": "2077年、酸性雨が降る巨大都市『ネオ・シンジュク』",
  "settingEra": "近未来",
  "settingBackground": "電脳探偵として生計を立てるあなたに、巨大企業から行方不明になった娘捜索の依頼が届く。しかし依頼の裏には都市全体を揺るがす陰謀が潜んでいる。",
  "writingStyle": "乾いたハードボイルド調。スラングとメタファーを多用して描写する",
  "openingScene": "安物のジンを傾けていると、上等なスーツの男がドアを開けた。「君が腕利きのダイバーだと聞いた。娘を探してほしい。報酬は望むだけ払おう」",
  "mysteryScale": 4,
  "mysteries": [
    {
      "content": "依頼人の娘は何者に連れ去られたのか？",
      "truth": "企業内部の派閥争いで暗殺を企てられ、娘は自ら姿を消している",
      "status": "unresolved",
      "resolutionPeriod": 10
    }
  ],
  "characters": [
    {
      "name": "ジン・アーノルド",
      "gender": "男性",
      "job": "電脳探偵（ダイバー）",
      "firstPerson": "俺",
      "playerAlias": "",
      "personality": "皮肉屋だが義理堅い。仕事は手早く、無駄を嫌う。",
      "content": "かつて伝説的ハッカーだったが、仲間を失って引退した過去がある。",
      "relationshipWithPlayer": "",
      "recentEvents": "家賃滞納でオフィスを追い出されかけている",
      "isPlayerCharacter": true
    },
    {
      "name": "ユキ・エゾチカ",
      "gender": "女性",
      "job": "情報屋兼メカニック",
      "firstPerson": "アタシ",
      "playerAlias": "ジン",
      "personality": "明るくサバサバ。小気味よい軽口と現実的な助言を惜しまない。",
      "content": "主人公の過去を知る数少ない人物。借金持ちだが腕は確か。",
      "relationshipWithPlayer": "長年の仕事仲間で相棒",
      "recentEvents": "最新型のサイバー義手を買うため資金を探している",
      "isPlayerCharacter": false
    }
  ]
}
```
