> 🚧 只今誠意作成中です、しばらくお待ちください。。🚧

TODO：最後に画像を配置する。また、適切な見出し番号と所要時間を付け直す。

# はじめに

この資料は JAWS FESTA 2023 Kyushu で行われるハンズオンために書かれました。

イベントページは[こちら](https://jft2023.jaws-ug.jp/)。

手を動かしながら Amazon DynamoDB の基本を学ぶことができます。

この資料のマスタは[GitHub](https://github.com/yukinissie/jaws-festa-2023-dynamodb-handson/blob/main/README.md)にあります。

# 自己紹介

- ニッシー ☆ === 西勇樹（Nishi Yuki）
- 株式会社ユーザベースに今年新卒入社しました。
- ソーシャル経済メディア「NewsPicks」の Web 版を作っています。
- 日本酒が好きです。

---

- SNS リンク
  - 𝕏 (Twitter)：https://twitter.com/yukinissie
  - Facebook：https://www.facebook.com/yukinissie
  - GitHub：https://github.com/yukinissie

---

@[TOC](目次)

# 1. 座学編[30]

## 1-1. Amazon DynamoDB の基本[5]

Amazon DynamoDB(以下、DynamoDB) は高速で予測可能なパフォーマンスやシームレスなスケーラビリティを提供するフルマネージドでサーバーレスの key-value NoSQL データベースサービスです。

### 1-1-1. DynamoDB の利点[5]

以下のような利点があります。

- 分散データベースの運用やスケーリングにかかる管理負荷を軽減
- ハードウェアのプロビジョニング、セットアップと設定、レプリケーション、ソフトウェアのパッチ適用、クラスタのスケーリングなどを心配する必要がなくなる

### 1-1-2. DynamoDB の特徴[5]

DynamoDB では以下のような特徴があります。

- 任意の量のデータを格納および取得し、任意のレベルのリクエストトラフィックに対応できるデータベーステーブルの作成
- ダウンタイムやパフォーマンスの低下なしに、テーブルのスループット容量をスケールアップまたはスケールダウン
- AWS Management Console を使用した、リソースの使用率とパフォーマンスメトリクスの監視
- 他にもたくさんの特徴があります
  - 詳細：AWS 公式サイト「[Amazon DynamoDB の特徴](https://aws.amazon.com/jp/dynamodb/features/)」

### 1-1-3. DynamoDB の機能[5]

DynamoDB では以下のような機能が提供されています。

- オンデマンドバックアップ機能
  - 完全なバックアップを作成できる
  - 詳細：AWS 公式ドキュメント「[DynamoDB のオンデマンドバックアップおよび復元の使用](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/BackupRestore.html)」
- ポイントインタイムリカバリ機能
  - リアルタイムでバックアップし任意の時点にテーブルを復元できる
  - 詳細：AWS 公式ドキュメント「[ポイントインタイムリカバリ: 仕組み](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/PointInTimeRecovery_Howitworks.html)」
- 期限切れの項目をテーブルから自動的に削除する機能
  - 詳細：AWS 公式ドキュメント 「[DynamoDB の有効期限 (TTL) を使用して項目を期限切れにする](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/TTL.html)」

### 1-1-4. DynamoDB の高い可用性と耐久性[5]

- 一貫性のある高速なパフォーマンスを維持しながら、スループットとストレージ要件を処理するために十分な数のサーバーにテーブルのデータとトラフィックを自動的に分散する
- すべてのデータはソリッドステートディスク(SSD)に保存され、AWS リージョン内の複数の [アベイラビリティーゾーン（AZ）](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/using-regions-availability-zones.html) に自動的にレプリケートされ、ビルトインの高可用性とデータの耐久性を提供する
- グローバルテーブルを使用すると、AWS リージョン間で DynamoDB のテーブルを同期させることが可能
  - 詳細：AWS 公式ドキュメント「[グローバルテーブル – DynamoDB の複数リージョンレプリケーション](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/GlobalTables.html)」

### 1-1-5. ユースケース[5]

以下のような１秒間に数百万回のリクエストを処理する必要がある業界で使われています。

- アドテック(広告)
- 小売り
- ソフトウェアとインターネット
- ゲーム
- メディアとエンターテイメント
- 銀行と金融

詳細は AWS 公式サイト「[Amazon DynamoDB](https://aws.amazon.com/jp/dynamodb/)」のユースケースセクションをご覧ください。

### 1-1-6. 料金 [5] 🚧

DynamoDB の課金対象は大きく分けて以下の 2 つです。

1. DynamoDB テーブル内のデータの読み取り、書き込み、保存
2. 有効化したオプション機能の使用

さらに 1. には「オンデマンド」と「プロビジョニング」という 2 種類のキャパシティモードがあり、それぞれのモードにおけるテーブルの読み書き処理について別個の請求オプションがあります。

#### 無料利用枠（無期限無料）

### 1-1-7. 公式ドキュメント[5]

安心安全 AWS 公式ドキュメントのリンクはこちら ↓

- https://docs.aws.amazon.com/ja_jp/dynamodb/

例えば以下のようなものが載っています。

- [「DynamoDB の使用開始」](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GettingStartedDynamoDB.html)
- [「DynamoDB へのアクセス」](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/AccessingDynamoDB.html)
- [「Programming with DynamoDB」](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Programming.html)

今回のハンズオンは公式ドキュメントの内容を元に作成しています。

### 1-1-8. 学習リソース[5]

- [公式チュートリアル](https://aws.amazon.com/jp/dynamodb/getting-started/?nc1=h_ls)
- [API リファレンス](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/APIReference/Welcome.html)
  - AWS CLI もしくは AWS SDK から DynamoDB を操作する際に参照する
- [よくある質問](https://aws.amazon.com/jp/dynamodb/faqs/)
- [フォーラム](https://repost.aws/tags/TAljkKQ0MDQJCjDdxSeDQBJw?forumID=131)
  - DynamoDB に関する質問や issue（技術的課題）を投稿することができる
- [公式ブログ](https://aws.amazon.com/jp/blogs/database/tag/dynamodb/)

## 1-2. DynamoDB の基本用語

### 1-2-1. テーブル・項目・属性

- テーブル（Table）
  - DynamoDB はデータをテーブルに保存する
  - テーブルは複数の項目の集合
- 項目（Item）
  - 各テーブルにはゼロ以上の項目が含まれている
  - 項目は他のすべての項目間で一意に識別可能な属性の集合
  - 他のデータベースでいうところの「行（レコード）」に似ている
  - テーブルに保存できる項目数に制限はない

---

- 属性（Attribute）
  - 各項目は 1 つ以上の属性で構成される
  - 属性は基盤となるデータ要素であり、それ以上分割する必要がないものである
  - 他のデータベースでいうところの「列（フィールド）」に似ている
  - プライマリキー以外はスキーマレス
  - 属性のほとんどは 1 つの値のみを持つことができる
    - 例：文字列、数値
  - 一部の項目には、ネストされた属性 (アドレス) がある
    - ネストの深さが最大 32 レベルの属性をサポート

### 1-2-2. 属性の詳細 (1/2)

属性は、基盤となるデータ要素であり、それ以上分割する必要がないものです。

- 命名規則あり
  - 1 文字以上の長さ、64 KB 未満のサイズにする必要あり
  - できるだけ短くすることがベストプラクティス
  - 属性名がストレージとスループットの使用量の測定に含まれるため、属性名を短くすることで消費される読み取りリクエストユニットを減らすことができる
  - 以下は例外で、これらの属性名は 255 文字以下である必要がある
    - セカンダリインデックスのパーティションキー名
    - セカンダリインデックスのソートキー名
    - ユーザー指定の射影された属性の名前 (ローカルセカンダリインデックスにのみ適用)
  - 参考：AWS 公式ドキュメント「[Amazon DynamoDB でサポートされるデータ型と命名規則](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/HowItWorks.NamingRulesDataTypes.html)」

### 1-2-2. 属性の詳細 (2/2)

- データ型
  - スカラー型
    - 数値
    - 文字列
    - バイナリ(base64 エンコードされたデータ)
    - ブール
    - null
  - ドキュメント型
    - リスト
    - マップ
  - セット型
    - 文字セット
    - 数値セット
    - バイナリセット

参考：AWS 公式ドキュメント「[Amazon DynamoDB のコアコンポーネント](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/HowItWorks.CoreComponents.html)」

### 1-2-3. 項目の詳細

項目は、他のすべての項目間で一意に識別可能な属性の集合です。

- 各テーブルにゼロ以上の項目が含まれている
- 他のすべての項目間で一意に識別可能な属性のグループである
- 多くの点で他のデータベースシステムの行、レコード、またはタプルに似ている
- テーブルに保存できる項目数に制限はなし

参考：AWS 公式ドキュメント「[Amazon DynamoDB のコアコンポーネント](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/HowItWorks.CoreComponents.html)」

### 1-2-4. テーブルの詳細

テーブルの重要な用語は以下の通りです。

- テーブル名
- 状態
- プライマリキー
- セカンダリインデックス
- 読み取り/書き込みキャパシティモード
- テーブルクラス
- 削除保護

それぞれの用語について説明していきます。

#### テーブル名[1.5]

その名の通りテーブルの名前です。

- 命名規則あり
  - すべての名前は UTF-8 を使用してエンコードする必要があり
  - 大文字と小文字が区別される
  - テーブル名とインデックス名の長さは 3 ～ 255 文字
  - 次の文字が使える
    - `a-z`
    - `A-Z`
    - `0-9`
    - `_` (下線)
    - `-` (ダッシュ)
    - `.`（ドット）
- 現在の AWS アカウントとリージョン内で一意である必要がある
  - 例 1）米国東部 (バージニア北部) に People テーブルを作成した場合、米国東部 (バージニア北部) に追加で同名の People テーブルを作成することはできない
  - 例 2）米国東部 (バージニア北部) に People テーブルを作成し、欧州 (アイルランド) に別の People テーブルを作成できるが、これらの 2 つのテーブルは全くの別物である

詳細については、AWS 公式ドキュメント「[Amazon DynamoDB でサポートされるデータ型と命名規則](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/HowItWorks.NamingRulesDataTypes.html)」を参照してください。

#### 状態[1]

現在のテーブルの状態について知ることができます。AWS SDK for Java V2 では以下のような状態が定義されています。（一部抜粋）

- ACTIVE
- ARCHIVED
- ARCHIVING
- CREATING
- DELETING
- UPDATING

#### プライマリキー

テーブルの項目を一意に識別するために使用される属性または属性のセットです。

DynamoDB は 2 種類の異なるプライマリキーをサポートします。

1. パーティションキーのみ
2. パーティションキーとソートキーの組み合わせ

プライマリキー属性はスカラー値である必要があり、許可される唯一のデータ型は、文字列、数値、またはバイナリです。

参考：AWS 公式ドキュメント「[Amazon DynamoDB のコアコンポーネント](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/HowItWorks.CoreComponents.html)」

##### パーティションキー

1 つの属性で構成されたシンプルなプライマリキーです。

- DynamoDB はデータをパーティションと呼ばれる物理ストレージに保存する
- パーティションキーを利用して生成したハッシュ値によって、データはパーティションに分散配置される
- パーティションは、AWS リージョン内の複数のアベイラビリティーゾーン間で自動的にレプリケート（複製）される
- パーティション管理は DynamoDB によって完全に処理される
- パーティションを管理者が管理する必要はない

##### ソートキー

同じパーティションキー値を持つすべての項目をソートしてまとめて保管するための複合プライマリキーです。

- 同じパーティションキーを持つ他の項目とソートキーの昇順で項目が保存される
- テーブルから項目を読み込むには、パーティションのキーバリューとソートキーのキーバリューを指定する必要がある
- 目的の項目に同じパーティションキーバリューがある場合、単一のオペレーション (`Query`) でテーブルから複数の項目を読み取ることができる
- パーティションキーとソートキーが存在するテーブルでは、同じパーティションのキーバリューが複数の項目に割り当てられることがある
- ソートキー値は複数の項目で異なる必要がある

#### セカンダリインデックス

- テーブルに 1 つ以上のセカンダリインデックスを作成できる
- セカンダリインデックスでは、プライマリキーに対するクエリに加えて、代替キーを使用して、テーブル内のデータのクエリを行うことができる
- インデックスの使用は必須ではありませんが、インデックスを使用すると、データのクエリを行う際にアプリケーションの柔軟性が高まる
- テーブルにグローバルセカンダリインデックスを作成すると、テーブルから行う場合とほぼ同じ方法でインデックスからデータを読み取ることができる

#### 2 つのセカンダリインデックス

DynamoDB では、次の 2 種類のインデックスをサポートしています。

- グローバルセカンダリインデックス
  - パーティションキーおよびソートキーを持つインデックス
  - テーブルのものとは異なる場合がある
- ローカルセカンダリインデックス
  - パーティションキーはテーブルと同じ
  - ソートキーが異なるインデックスである

#### 読み取り/書き込みキャパシティモード

テーブルで読み込みおよび書き込みを処理するためのキャパシティモードについて説明します。

- 2 つのキャパシティモードがある
  - オンデマンドモード
  - プロビジョニングモード (デフォルト、無料利用枠の対象)
- 読み取りおよび書き込みスループットの課金方法と容量の管理方法を制御する
- 参考：AWS 公式ドキュメント「[読み取り/書き込みキャパシティモード](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/HowItWorks.ReadWriteCapacityMode.html)」

##### オンデマンドモード (1/2)

オンデマンドキャパシティモードの特徴は以下の通りです。

- キャパシティプランなしで 1 秒あたりに数千ものリクエストを処理できる
- 読み取りおよび書き込みリクエストごとの支払い料金が用意されている
- 使用した分だけ課金される

##### オンデマンドモード (2/2)

オンデマンドキャパシティモードは以下のような場合に適しています。

- 不明なワークロードを含む新しいテーブルを作成する場合
- アプリケーションのトラフィックが予測不可能な場合
- わかりやすい従量課金制の支払いを希望する場合

- 参考：AWS 公式ドキュメント「[読み取り/書き込みキャパシティモード](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/HowItWorks.ReadWriteCapacityMode.html)」

##### プロビジョニングモード (1/2)

プロビジョニングキャパシティモードの特徴は以下の通りです。

- アプリケーションに必要な 1 秒あたりの読み込みと書き込みの回数を事前に指定する
- Auto Scaling を使用すると、トラフィックの変更に応じて、テーブルのプロビジョンドキャパシティーを自動的に調整できる

##### プロビジョニングモード (2/2)

プロビジョニングキャパシティモードは以下のような場合に適しています。

- アプリケーションのトラフィックが予測可能な場合
- トラフィックが一定した、または徐々に増加するアプリケーションを実行する場合
- キャパシティーの要件を予測してコストを管理できる場合

- 参考：AWS 公式ドキュメント「[読み取り/書き込みキャパシティモード](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/HowItWorks.ReadWriteCapacityMode.html)」

##### キャパシティユニット (1/2)

プロビジョニングモードのテーブルでは、読み取りキャパシティユニット (RCU) と書き込みキャパシティユニット (WCU) の観点でスループットキャパシティを指定できます。

- 1 読み込みキャパシティユニットは最大サイズが 4 KB までのサイズの項目について
  - 1 秒あたり 1 回の強力な整合性のある読み込みができる
  - 1 秒あたり 2 回の結果整合性のある読み込みができる
- トランザクションの読み込みリクエストでは、4 KB までの項目を 1 秒あたりに 1 回読み込むのに読み込みキャパシティユニットが 2 個必要である
- 4 KB より大きい項目を読み込む必要がある場合は追加の読み込みキャパシティユニットを消費する必要がある
- 必要な読み込みキャパシティユニットの最大数は、項目のサイズと、結果整合性のある読み込みまたは強力な整合性のある読み込みが必要かどうかによって異なる
- 詳細：AWS 公式ドキュメント「[読み込みでのキャパシティユニットの消費](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/ProvisionedThroughput.html#ItemSizeCalculations.Reads)」

##### キャパシティユニット (2/2)

- 1 書き込みキャパシティユニットは、最大サイズが 1 KB の項目について
  - 1 秒あたり 1 回の書き込みができる
- 1 KB より大きい項目を書き込む必要がある場合は追加の書き込みキャパシティユニットを消費する必要がある
- トランザクションの書き込みリクエストでは、1 KB までの項目を 1 秒あたり 1 回書き込むのに書き込みキャパシティユニットが 2 個必要である
- 必要な書き込みキャパシティーユニットの合計数は、項目サイズに応じて異なる
- 詳細：AWS 公式ドキュメント「[書き込みでのキャパシティユニットの消費](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/ProvisionedThroughput.html#ItemSizeCalculations.Writes)」

参考：AWS 公式ドキュメント「[読み取り/書き込みキャパシティモード](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/HowItWorks.ReadWriteCapacityMode.html)」

#### テーブルクラス (1/2)

コストの最適化に役立つように設計された 2 つのテーブルクラスが用意されています。

- DynamoDB 標準テーブルクラス（デフォルト）
  - 大半のワークロードで推奨
- DynamoDB Standard-Infrequent Access (DynamoDB 標準-IA) テーブルクラス
  - ストレージが主要なコストとなるテーブル用に最適化
  - アクセス頻度の低いデータを格納するテーブル
    - アプリケーションログ
    - 古いソーシャルメディアの投稿
    - e コマースの注文履歴
    - 過去のゲーム実績

#### テーブルクラス (2/2)

テーブルクラスに関する料金の詳細については、「[Amazon DynamoDB の料金表](http://aws.amazon.com/dynamodb/pricing/on-demand/)」を参照してください。

参考：AWS 公式ドキュメント「[テーブルクラス](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/HowItWorks.TableClasses.html)」

#### 削除保護[1]

削除保護はテーブルの削除を防ぐために使用される機能です。

- 削除保護を有効にすると、その間はテーブルを削除することができなくなる

# 2. 実習編[60]

## 2-1. DynamoDB サービストップページの開き方[5]

1. AWS コンソールにログインして、ヘッダーにある検索窓をクリックします。

![Alt text](image.png)

---

2. 検索窓に「DynamoDB」と入力します。
3. 検索結果の中から「DynamoDB」をクリックします。

![Alt text](image-1.png)

---

4. DynamoDB サービスのトップページが開きます。

![Alt text](image-5.png)

トップページには座学編で説明した内容が書かれています。

### 2-2-1. 【余談】AWS サービスのブックマークの仕方[5]

1. 検索窓にブックマークしたい AWS サービス名（例では「DynamoDB」）を入力します。
2. 検索結果横の星マークをクリックします。
3. ブックマークしたい AWS サービスがブックマークバーに追加されます。

![Alt text](image-4.png)

## 2-3. テーブルの作成[15]

では早速、テーブルを作成していきましょう！

### 2-3-1. テーブル一覧を表示する[1]

1. DynamoDB サービスページの左にあるメニュー内の「テーブル」をクリックします。

![Alt text](2-3-1-1.png)

---

2. そうすることでテーブル一覧を表示することができます。

![Alt text](2-3-1-2.png)

### 2-3-2. テーブルを作成する[10]

1. 「テーブルの作成」をクリックします。

![Alt text](2-3-2-1.png)

---

2. 「テーブル名」に「`jft2023`」と入力します。
3. 「主キー」に「`id`」と入力します。

![Alt text](2-3-2-2.png)

---

4. 他の設定を変更せずに一番下までスクロールします。
5. タグセクションの「新しいタグの追加」をクリックします。
6. 「キー」に「`Group`」と入力します。
7. 「値」に「`jft2023-dynamodb-handson`」と入力します。
8. 「テーブルの作成」をクリックします。

---

![Alt text](2-3-2-3.png)

### 2-3-3. テーブルの作成状況を確認する[1]

「テーブルの作成」をクリックするとテーブル一覧が表示され、自動的に作成処理が開始されます。テーブルの作成にはしばらく時間がかかりますが、テーブルが作成中かどうかの状態などを一覧から確認できます。通常、1 分程度で完了します。

![Alt text](image-3.png)

### 2-3-4. テーブルの作成完了を確認する[1]

作成が完了すると以下のような画面になります。

![Alt text](2-3-2-4.png)

テーブルを作成できました！🎉

## 2-5. 項目の探索[15]

### 2-5-1. 項目の作成[5]

<TBD>

```
- 属性について
  - 名前
  - 値
  - タイプ
```

参考：https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/getting-started-step-2.html

### 2-5-2. 項目の検索[5]

＜ TBD ＞

参考：https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/getting-started-step-3.html
https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/SQLtoNoSQL.ReadData.html
https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/SQLtoNoSQL.ReadData.SingleItem.html
https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/SQLtoNoSQL.ReadData.Query.html
https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/SQLtoNoSQL.ReadData.Scan.html

#### スキャン

#### クエリ

#### フィルタ

### 2-5-3. 項目の操作[5]

#### 編集

#### 複製

#### 削除

#### CSV ダウンロード

- 選択した項目をダウンロード
- 検索した結果をダウンロード

## インデックスの追加

## グローバルテーブルの作成

## バックアップ

## エクスポートおよびストリームの作成

## 追加の設定

## 2-6. お片付け[15]

# 3. 終わりに[5]

---

# その他用語集

## 予約語と特殊文字

DynamoDB には予約語と特殊文字があります。

- 予約語の例： `INSERT` や `DELETE`
  - 詳細は：「[DynamoDB の予約語](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/ReservedWords.html)」
- 特殊文字の例： `#` （ハッシュ）や `:` （コロン）
- 命名目的でこれらの予約語と特殊文字を使用することができるが、非推奨
  - 式でこれらの名前を使用するたびに、プレースホルダー変数を定義する必要がある
  - 詳細は：「[DynamoDB の式の属性名](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/Expressions.ExpressionAttributeNames.html)」
  - ドキュメントによっては予約語を「使用しないでください」と書かれている

## DynamoDB テーブルのデータモデリング

設計の話
<TBD>

https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/data-modeling.html
