<<<<<<< HEAD
# NovelADV シナリオテンプレート JSON仕様書

## 1. ファイル形式概要
*   **ファイル拡張子**: `.json` または `.noveladv_scenario`
*   **文字コード**: UTF-8
*   **データ構造**: 単一のルートオブジェクト（`ScenarioTemplate`）

## 2. ルートオブジェクト構造
JSONのルート（一番外側）は以下のキーを持つオブジェクトです。

| キー名 | 型 | 必須 | 説明 |
| :--- | :--- | :--- | :--- |
| `name` | String | **YES** | **シナリオテンプレート名**。<br>アプリ内での識別子として使用されます。既存のテンプレートと同じ名前の場合、上書き確認が表示されます。 |
| `settingPlace` | String | No | **場所**。<br>物語の主な舞台（例：「新宿の雑居ビル」「魔法学校の寮」）。 |
| `settingEra` | String | No | **時代**。<br>時代背景（例：「現代日本」「西暦3000年」「中世ファンタジー風」）。 |
| `settingBackground` | String | No | **背景ストーリー**。<br>世界観の深い設定や、物語開始以前の経緯。 |
| `writingStyle` | String | No | **文体・AIへの指示**。<br>AIの描写スタイルやナレーションの口調（例：「ハードボイルド調で」「三人称視点で客観的に」）。 |
| `mysteryGenerationTrend`| String | No | **謎・伏線の傾向**。<br>AIが自動生成する謎のジャンル指定（例：「人間関係のトラブルを中心に」「SF的ガジェットの謎」）。 |
| `openingScene` | String | No | **オープニングシーン**。<br>ゲーム開始時にAIが最初に出力する描写テキスト。 |
| `mysteryScale` | Integer | No | **謎のリアリティレベル**。<br>1〜5の整数で指定します（詳細は後述）。省略時は `2` (Grounded) が適用されます。 |
| `characters` | Array | No | **登場人物リスト**。<br>キャラクターオブジェクトの配列（詳細は後述）。 |

### 2.1 mysteryScale (謎のリアリティレベル) の値
| 値 | レベル名称 | 説明 |
| :--- | :--- | :--- |
| `1` | Mundane | **日常・ラブコメ**。超常現象なし、平和的。 |
| `2` | Grounded | **本格ミステリー・現実**。物理法則遵守、論理的解決。 |
| `3` | Ambiguous | **都市伝説・微ファンタジー**。解釈の余地がある不思議、高度な科学。 |
| `4` | Supernatural | **伝奇・ハイファンタジー**。魔法や異能が実在し、謎の核になる。 |
| `5` | Eldritch | **コズミックホラー・シュール**。論理崩壊、不条理。 |

## 3. Characters (登場人物) オブジェクト構造
`characters` 配列の中に含める各キャラクターの定義です。

| キー名 | 型 | 必須 | 説明 |
| :--- | :--- | :--- | :--- |
| `name` | String | **YES** | **キャラクター名**。 |
| `gender` | String | No | **性別**。 |
| `job` | String | No | **職業・役割**（例：「探偵」「王女」）。 |
| `personality` | String | No | **性格・特徴**。<br>AIがロールプレイする際の指針となる性格描写。 |
| `content` | String | No | **自由記述・背景**。<br>生い立ちや目的などの詳細情報。 |
| `firstPerson` | String | No | **一人称**（例：「私」「俺」「ボク」）。 |
| `playerAlias` | String | No | **主人公の呼び方**（例：「あなた」「先輩」「お兄ちゃん」）。 |
| `relationshipWithPlayer`| String | No | **プレイヤーとの関係**。<br>（動的情報）初期状態の関係性。 |
| `recentEvents` | String | No | **最近の出来事**。<br>（動的情報）物語開始時点での状況。 |
| `isPlayerCharacter` | Boolean| No | **主人公フラグ**。<br>`true` の場合、このキャラがプレイヤーの分身として設定されます。 |

## 4. JSONサンプル

以下をコピーして `.json` ファイルとして保存するか、「テキストからインポート」機能に貼り付けて使用してください。
=======
### シナリオテンプレート JSON 仕様書

#### 1. 概要
`NovelADV` が新規プロジェクトの土台として読み込む「シナリオテンプレート」を定義するJSONです。世界設定、文体、オープニング、キャラクター初期値、謎・伏線の初期リストなど、物語の方向性を決める要素を含みます。
>>>>>>> 9d18c3286d1b5ba5622fdfd7b2cc8eb4095925ab

```json
{
<<<<<<< HEAD
  "name": "洋館ミステリー",
  "settingPlace": "嵐の孤島にある古い洋館",
  "settingEra": "1920年代、イギリス",
  "settingBackground": "富豪が遺した遺産を巡り、親族たちが集められた。外は嵐で連絡手段は絶たれている。",
  "writingStyle": "アガサ・クリスティ風の古典的なミステリー小説のトーン。三人称視点で、重厚な雰囲気を描写してください。",
  "mysteryGenerationTrend": "密室トリック、アリバイ崩し、隠された血縁関係",
  "openingScene": "激しい雷鳴が轟き、館の照明が一瞬明滅した。大広間に集まった人々の顔に不安の色が浮かぶ。「…さて、皆さんに集まっていただいたのは他でもありません」弁護士が重い口を開いた。",
  "mysteryScale": 2,
  "characters": [
    {
      "name": "アーサー・ヘイスティングス",
      "gender": "男性",
      "job": "私立探偵",
      "firstPerson": "私",
      "playerAlias": "君",
      "personality": "冷静沈着で論理的。パイプを嗜む紳士。",
      "content": "かつてロンドン警視庁に協力していた名探偵。招待状を受け取りこの島へ来た。",
      "isPlayerCharacter": true
    },
    {
      "name": "エレノア・ヴァンガード",
      "gender": "女性",
      "job": "富豪の長女",
      "firstPerson": "わたくし",
      "playerAlias": "探偵様",
      "personality": "高慢だが、どこか怯えている様子。",
      "content": "遺産相続の第一候補。妹たちとは仲が悪い。",
      "relationshipWithPlayer": "探偵としての腕を見定めている。",
      "recentEvents": "昨晩、何者かに部屋を覗かれたと主張している。",
      "isPlayerCharacter": false
    },
    {
      "name": "セバスチャン",
      "gender": "男性",
      "job": "執事",
      "firstPerson": "私（わたくし）",
      "playerAlias": "アーサー様",
      "personality": "忠実で無口。館の秘密を何か知っているようだ。",
      "content": "長年この屋敷に仕えている老執事。",
=======
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
>>>>>>> 9d18c3286d1b5ba5622fdfd7b2cc8eb4095925ab
      "isPlayerCharacter": false
    }
  ]
}
```
<<<<<<< HEAD

## 5. インポート時の注意点

1.  **無料プランの制限**:
    *   `characters` 配列に **2名以上** のキャラクターが含まれている場合、無料プランのユーザーはインポートに失敗します（Premiumへの加入が必要です）。
2.  **重複時の挙動**:
    *   アプリ内に既に同じ `name` のテンプレートが存在する場合、ダイアログが表示され「上書き」するかどうかを選択できます。
3.  **IDについて**:
    *   JSON内に `id` (UUID) や `createdAt` (Date) を含めることも可能ですが、必須ではありません。含まれていない場合、インポート時にアプリ側で自動生成されます。共有目的の場合は含めないことを推奨します。
=======
>>>>>>> 9d18c3286d1b5ba5622fdfd7b2cc8eb4095925ab
