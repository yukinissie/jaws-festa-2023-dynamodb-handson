# はじめに

この資料は JAWS FESTA 2023 Kyushu で行われるハンズオンために書かれました。

イベントページは[こちら](https://jft2023.jaws-ug.jp/)。

手を動かしながら Amazon DynamoDB の基本を学ぶことができます。

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

# 1. 座学編[30]（xx:xx〜xx:xx）

## 1-1. Amazon DynamoDB の基本

Amazon DynamoDB(以下、DynamoDB) は高速で予測可能なパフォーマンスやシームレスなスケーラビリティを提供するフルマネージドでサーバーレスの key-value NoSQL データベースサービスです。

### 1-1-1. DynamoDB の利点

以下のような利点があります。

- 分散データベースの運用やスケーリングにかかる管理負荷を軽減
- ハードウェアのプロビジョニング、セットアップと設定、レプリケーション、ソフトウェアのパッチ適用、クラスタのスケーリングなどを心配する必要がなくなる

### 1-1-2. DynamoDB の特徴

DynamoDB では以下のような特徴があります。

- 任意の量のデータを格納および取得し、任意のレベルのリクエストトラフィックに対応できるデータベーステーブルの作成
- ダウンタイムやパフォーマンスの低下なしに、テーブルのスループット容量をスケールアップまたはスケールダウン
- AWS Management Console を使用した、リソースの使用率とパフォーマンスメトリクスの監視
- 他にもたくさんの特徴があります
  - 詳細：AWS 公式サイト「[Amazon DynamoDB の特徴](https://aws.amazon.com/jp/dynamodb/features/)」

### 1-1-3. DynamoDB の機能

DynamoDB では以下のような機能が提供されています。

- オンデマンドバックアップ機能
  - 完全なバックアップを作成できる
  - 詳細：AWS 公式ドキュメント「[DynamoDB のオンデマンドバックアップおよび復元の使用](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/BackupRestore.html)」
- ポイントインタイムリカバリ機能
  - リアルタイムでバックアップし任意の時点にテーブルを復元できる
  - 詳細：AWS 公式ドキュメント「[ポイントインタイムリカバリ: 仕組み](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/PointInTimeRecovery_Howitworks.html)」
- 期限切れの項目をテーブルから自動的に削除する機能
  - 詳細：AWS 公式ドキュメント 「[DynamoDB の有効期限 (TTL) を使用して項目を期限切れにする](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/TTL.html)」

### 1-1-4. DynamoDB の高い可用性と耐久性

- 一貫性のある高速なパフォーマンスを維持しながら、スループットとストレージ要件を処理するために十分な数のサーバーにテーブルのデータとトラフィックを自動的に分散する
- すべてのデータはソリッドステートディスク(SSD)に保存され、AWS リージョン内の複数の [アベイラビリティーゾーン（AZ）](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/using-regions-availability-zones.html) に自動的にレプリケートされ、ビルトインの高可用性とデータの耐久性を提供する
- グローバルテーブルを使用すると、AWS リージョン間で DynamoDB のテーブルを同期させることが可能
  - 詳細：AWS 公式ドキュメント「[グローバルテーブル – DynamoDB の複数リージョンレプリケーション](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/GlobalTables.html)」

### 1-1-5. ユースケース

以下のような１秒間に数百万回のリクエストを処理する必要がある業界で使われています。

- アドテック(広告)
- 小売り
- ソフトウェアとインターネット
- ゲーム
- メディアとエンターテイメント
- 銀行と金融

詳細は AWS 公式サイト「[Amazon DynamoDB](https://aws.amazon.com/jp/dynamodb/)」のユースケースセクションをご覧ください。

### 1-1-6. 料金

DynamoDB の課金対象は大きく分けて以下の 2 つです。

1. DynamoDB テーブル内のデータの読み取り、書き込み、保存
2. 有効化したオプション機能の使用

さらに 1. には「オンデマンド」と「プロビジョニング」という 2 種類のキャパシティモードがあり、それぞれのモードにおけるテーブルの読み書き処理について別個の請求オプションがあります。

詳しくは AWS 公式サイト「[Amazon DynamoDB 料金](https://aws.amazon.com/jp/dynamodb/pricing/)」をご覧ください。

#### 無料利用枠（無期限無料）

Amazon DynamoDB には無期限の無料利用枠があります。

### 1-1-7. 公式ドキュメント

安心安全 AWS 公式ドキュメントのリンクはこちらです ↓

- https://docs.aws.amazon.com/ja_jp/dynamodb/

例えば以下のようなものが載っています。

- [「DynamoDB の使用開始」](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GettingStartedDynamoDB.html)
- [「DynamoDB へのアクセス」](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/AccessingDynamoDB.html)
- [「Programming with DynamoDB」](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Programming.html)

今回のハンズオンは公式ドキュメントの内容を元に作成しています。

### 1-1-8. 学習リソース

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

#### テーブル名

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

#### 状態

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

#### 削除保護

削除保護はテーブルの削除を防ぐために使用される機能です。

- 削除保護を有効にすると、その間はテーブルを削除することができなくなる

# 休憩[10]（xx:xx〜xx:xx）

# 2. 実習編[60]（xx:xx〜xx:xx）

## 2-1. DynamoDB サービストップページの開き方[5]

1. AWS コンソールにログインして、ヘッダーにある検索窓をクリックします。

![image](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/5155dba0-136a-42ea-8c43-ddedd9e54f14.png)

---

2. 検索窓に「DynamoDB」と入力します。
3. 検索結果の中から「DynamoDB」をクリックします。

![image-1](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/a5fe077b-5b2b-4222-b810-205f87bd3181.png)

---

4. DynamoDB サービスのトップページが開きます。

![image-5](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/42734ab1-804c-4de0-81e9-313d4682ff70.png)

トップページには座学編で説明した内容が書かれています。

### 2-2-1. 【余談】AWS サービスのブックマークの仕方[5]

1. 検索窓にブックマークしたい AWS サービス名（例では「DynamoDB」）を入力します。
2. 検索結果横の星マークをクリックします。
3. ブックマークしたい AWS サービスがブックマークバーに追加されます。

![image-4](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/4a3eb7b1-285f-4d22-aa14-c0cde46963dd.png)

## 2-3. テーブルの作成

では早速、テーブルを作成していきましょう！

### 2-3-1. テーブル一覧を表示する

1. DynamoDB サービスページの左にあるメニュー内の「テーブル」をクリックします。

![2-3-1-1](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/be8a4ac5-1acf-46aa-a6cd-416a7c8942fc.png)

---

2. そうすることでテーブル一覧を表示することができます。

![2-3-1-2](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/c9cb7f9b-7e9b-4141-a0dd-830c9c89ba80.png)

### 2-3-2. テーブルを作成する (1/5)

書棚を管理するためのテーブルを作成していきます。

1. 「テーブルの作成」をクリックします。

![2-3-2-1](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/60aa7d51-2a77-4870-892e-a05e896beb9d.png)

### 2-3-2. テーブルを作成する (2/5)

以下の内容を入力します。

1. 「テーブル名」に「`Books`」と入力します。
2. 「主キー」に「`ISBN`」と入力します。
3. 「ソートキー」に「`Title`」と入力します。

> ISBN（アイエスビーエヌ）は、International Standard Book Number の略称（頭字語）。図書（書籍）および資料の識別用に設けられた国際規格コード（番号システム）の一種
> 引用：Wikipedia「[ISBN](https://ja.wikipedia.org/wiki/ISBN)」

### 2-3-2. テーブルを作成する (3/5)

![image-10](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/88cfedd9-0760-4079-9717-5ab72ec187c7.png)

### 2-3-2. テーブルを作成する (4/5)

1. 他の設定を変更せずに一番下までスクロールします。
2. タグセクションの「新しいタグの追加」をクリックします。
3. 「キー」に「`Group`」と入力します。
4. 「値」に「`jft2023-dynamodb-handson`」と入力します。
5. 「テーブルの作成」をクリックします。

### 2-3-2. テーブルを作成する (5/5)

![2-3-2-3](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/10c6632d-503b-410b-9c09-16c80876238d.png)

### 2-3-3. テーブルの作成状況を確認する[1]

「テーブルの作成」をクリックするとテーブル一覧が表示され、自動的に作成処理が開始されます。テーブルの作成にはしばらく時間がかかりますが、テーブルが作成中かどうかの状態などを一覧から確認できます。通常、1 分程度で完了します。

![image-3](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/27c0421e-2722-4584-b302-e46e349db551.png)

### 2-3-4. テーブルの作成完了を確認する[1]

作成が完了すると以下のような画面になります。

![2-3-2-4](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/4a3423bd-edc5-463f-b3ff-94021088a2b9.png)

テーブルを作成できました！🎉

## 2-5-1. 項目の作成[5]

それでは最初の項目を追加してみましょう。

1. 先ほど作成したテーブルの名前をクリックします。

![image-6](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/84d20499-ce3b-4b1a-8f84-b0960a9edaad.png)

---

2. 「テーブルアイテムの探索」をクリックします。

![image-7](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/4a15153e-e913-46e4-98bd-d0b0b6a4837d.png)

---

3. 下にスクロールして、「項目を作成」をクリックします。

![image-8](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/2511a3e8-aebd-41ac-a32f-a6c87245917e.png)

---

4. 属性名と値を埋めていきます。内容は以下の通りです。
   1. 「`ISBN`」に「`978-1234567890`」と入力します。
   2. 「`Title`」に「`Sample Book 1`」と入力します。
5. 「新しい属性の追加」を押して、以下の内容を入力します。
   1. 文字列を追加して属性名に「`Author`」、値に「`John Doe`」と入力します。
   2. 数値を追加して属性名に「`PublicationYear`」値に「`2022`」と入力します。
6. 「項目を作成」をクリックします。

---

![image-11](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/52032dc6-81ed-4028-aef2-d66fe6d66d35.png)

---

項目が追加されました！🎉

![image-12](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/1d215b1f-94ec-4abc-a6e9-0a9f7315fb17.png)

参考：https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/getting-started-step-2.html

---

もう 1 つ項目を追加してみましょう。

1. 「項目を作成」をクリックします。

![image-13](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/345a7095-c5f9-438a-970a-c5e9941a34d8.png)

---

先ほどはフォームに入力しましたが、今度は DynamoDB JSON を入力してみます。

2. 「JSON ビュー」をクリックします。

![image-14](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/c5d06bc3-235e-4d49-9897-97c71a756b98.png)

---

3. 以下をコピーします。

```json
{
  "ISBN": { "S": "978-0987654321" },
  "Title": { "S": "Sample Book 2" },
  "Author": { "S": "Jane Smith" },
  "PublicationYear": { "N": "2023" }
}
```

---

4. 「JSON ビュー」に貼り付けます。
5. 「項目を作成」をクリックします。

![image-15](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/144d8b68-cc74-4bd6-baa3-644d2c5bc907.png)

### 【余談】JSON でも項目を作成できる[5]

DynamoDB では、JSON を使用して項目を作成することもできます。

JSON ビューにした際に「DynamoDB JSON の表示」トグルをクリックしてオフにすると、生の JSON を編集することができます。例えば以下のような JSON を入力して項目を作成することができます。

```json
{
  "ISBN": { "S": "978-1111222233" },
  "Title": { "S": "Sample Book 3" },
  "Author": { "S": "Alice Brown" },
  "PublicationYear": { "N": "2020" }
}
```

余裕があれば試してみてください。

---

![image-16](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/1202a314-8049-4f0a-b066-214e8b471e12.png)

## 2-5-2. 項目の検索[5]

様々な方法で項目を検索してみましょう。

### スキャン

全ての項目のデータ属性を返します。1 回のスキャンで最大 1 MB のデータを返すことができます。

実は項目作成後に見た「返された項目」はの内容はスキャンの結果です。

![image-17](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/9b4210bd-b69e-42da-96ee-ca78182d3de0.png)

### クエリ

テーブルまたはインデックス内の項目をクエリします。パーティションキーやソートキーを指定して検索することができます。

今回は ISBN が「`978-1234567890`」の項目を検索してみましょう。

1.  「クエリ」を選択します。
2.  「`ISBN`」に「`978-1234567890`」と入力します。
3.  「実行する」をクリックします。

![image-18](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/55d22abf-5b45-47ec-91cd-f2fa4f89aa6b.png)

---

クエリできました！🎉

![image-19](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/6f04520e-c55f-4df3-a6fa-06092f743d52.png)

### フィルタ

フィルター機能も試してみましょう。クエリと違い、フィルタはスキャンやクエリの後に行うことができます。

1. スキャンを選択します。
2. フィルターを以下の通りに設定します。
   1. 属性名を「`Title`」に
   2. タイプを「`文字列`」に
   3. 条件を「`次と等しい：`」に
   4. 値を「`Sample Book 2`」に
3. 「実行する」をクリックします。

---

![image-20](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/506669b5-2b34-4f41-ae42-58304fa05ae6.png)

---

フィルタできました！🎉

![image-21](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/8d5495b8-c48b-44ea-bf6c-55be5b84abfa.png)

## 2-5-3. 項目の操作[5]

項目の操作をやってみましょう。

### 編集

任意の項目を編集してみます。

1. パーティションキーの値をクリックします。

![image-22](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/8938aaf9-7e23-40c5-ab27-3a1eed1137f9.png)

---

2. 「`PublicationYear`」を「`2023`」に変更します。
3. 「Save and close」をクリックします。

![image-23](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/f5ad372a-af4e-4113-bbc8-6feb89b72c0c.png)

---

編集できました！🎉

![image-24](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/69917e41-3991-4ce9-b6ea-7df8aaae46be.png)

### 複製

次に項目を複製してみます。

1. 任意の項目を選択します。
2. 「アクション」メニューから「項目の複製」をクリックします。

![image-25](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/f8f17048-7f26-42c8-8eba-3290f969a506.png)

---

見慣れてきたフォームが表示されます。プライマリキーであるパーティションキーとソートキーの複合キーは一意である必要があるので変更する必要があります。

3. 「`ISBN`」を「`978-1234567891`」に変更します。
4. 「`Title`」を「`Sample Book 1 Copy`」に変更します。
5. 「項目を作成」をクリックします。

---

![image-26](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/3dc79454-c6ab-41cc-9763-3b88539d9782.png)

---

複製できました！🎉

![image-27](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/bebadabb-3f49-4211-91fc-bf7e8b9c1c08.png)

### 削除

最後に項目を削除してみます。

1. 任意の項目を選択します。
2. 「項目を削除」をクリックします。

![image-28](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/5f0568d7-b6d8-42bd-b526-4106780b1849.png)

---

3. 「削除」をクリックします。

![image-29](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/52203266-c547-46dd-b396-e9e5e5f6d22f.png)

---

削除できました！🎉

![image-30](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/a81f662b-66ac-4d1d-937a-a3a56179022a.png)

### CSV ダウンロード

テーブルアイテムを CSV ダウンロードしてみましょう。

- 選択した項目をダウンロード
  - ダウンロードしたい項目にチェックボックスをつけます
  - 「アクション」を押下して「選択した項目を CSV にダウンロード」を押します。
  - 選択した項目のみダウンロードされます。

---

![⑤](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/1dd4789d-9264-4a4a-a4e8-016c93181604.png)

---

- 検索した結果をダウンロード
  - 「項目のスキャンまたはクエリ」にて次のように設定して「実行」を押して検索します。
    - 「クエリ」
    - パーティションキー「978-1234567890」
  - 返された項目にてチェックボックスをつけずに
    「アクション」を押下して「結果を CSV ダウンロードする」
  - 検索された結果がダウンロードされます。

---

![⑥](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/f3b75cbf-0f04-42fc-8c3d-4e487b6d6e9b.png)

## インデックスの追加

ここではグローバルセカンダリインデックスの追加とその動きを見ていきましょう。

1. `インデックス`タブを開く
   ![[9005502645341738] スクリーンショット 2023-10-07 1.23.07](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/1fa98e49-fcdf-48e7-8bec-4e7946f4bbdb.png)
1. `インデックスの作成`をクリックする
   ![[9005502645148844] スクリーンショット 2023-10-07 1.26.17](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/484e9933-30c9-445f-afbf-0e5201e20bda.png)
1. インデックスの詳細に必要な値を入力する
   - パーティションキー: `Title`
   - インデックス名: `Title-All-Index`
   - ![[9005502642510468] スクリーンショット 2023-10-07 2.10.16](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/1f8024a2-d8b7-4325-972f-a12292438888.png)
1. インデックスキャパシティーはデフォルト値のまま
   ![[9005502644969926] スクリーンショット 2023-10-07 1.29.16](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/1e0f1e54-52a1-42d7-a736-96cca1f33a30.png)
1. 属性の射影もデフォルト値のまま
   ![[9005502644904375] スクリーンショット 2023-10-07 1.30.02](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/492b3248-a112-4268-af42-c5aa543f07c1.png)
1. `インデックスの作成`をクリックする
   ![[9005502644562107] スクリーンショット 2023-10-07 1.36.06](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/7c050d20-1562-4b85-8c13-8146959e3641.png)
1. 状態が`アクティブ`になるまで待つ
   ![[9005502644391946] スクリーンショット 2023-10-07 1.38.54](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/21f13b53-6cc8-4110-aa9d-ed90bc558444.png)
   ![[9005502643873292] スクリーンショット 2023-10-07 1.47.40](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/2f78d726-a1bc-45b9-96c9-2cf73324c001.png)
1. Item を追加する
   - ISBN: `97848840230926`
   - Title: `海の底`
   - Author: `有川浩`
1. Item を追加する
   - ISBN: `9784043898022`
   - Title: `海の底`
   - Author: `有川浩`
1. クエリでインデックスを指定して検索する
   - クエリ
   - テーブルまたはインデックスを選択: `インデックス - Title-All-Index`
   - Title (パーティションキー): `海の底`
   - ![[9005502642996970] スクリーンショット 2023-10-07 2.02.07](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/1822a73f-df6f-489d-a751-93cfe40d4fbd.png)

2 件、タイトルで検索ができました。
グローバルセカンダリインデックスは、パーティションキーを指定して一意に決まらない唯一のインデックスなのです。

## バックアップ

テーブルのバックアップ操作をやってみましょう。

### バックアップの作成

バックアップのタブを選択します。

![①](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/a92ae976-6d8e-4059-84c7-b663e43ed20b.png)

1. バックアップの作成を選択します。
2. オンデマンドバックアップを作成を選択します。
   1. ソーステーブルに「Books」
   2. バックアップ名に「Books-2023-10-7-jaws-festa」
3. 「バックアップの作成」をクリックします。

---

## ![②](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/e716d9e6-bfc9-460a-84e0-c533e8f8bd0d.png)

バックアップできました！🎉

### バックアップの復元

1. 「Books-2023-10-7-jaws-festa」のチェックボックスを選択します。
2. 「復元」をクリックします。
3. 「セカンダリインデックス」は「テーブル全体の復元」を選択します。
4. 「復元先 AWS リージョン」は「同じリージョン (東京)」を選択します。
5. 「保管中の暗号化の設定」は「Amazon DynamoDB が所有」を選択します。
6. 「復元」をクリックします。

---

![③](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/20c9e526-d253-47df-aea8-ff7dff11e28e.png)

---

テーブルの復元にはしばらく時間がかかりますが、テーブルが復元中かどうかの状態などを一覧から確認できます。今回のデータ量だと、5~10 分程度で完了します。

復元出来ました！🎉

![④](https://mimemo.s3-ap-northeast-1.amazonaws.com/attachment/78920e3b-02a8-4c47-a46c-d909cc0d9c8f.png)

## 2-6. お片付け[15]

# 3. 終わりに[5]
