---
title: 2022 Year in Review
publishDate: 2022-12-30
description: "2022 Year in Review"
---
## Work

GitHub API v4から自分の出したPR一覧を取得して確認してみました^[[GitHub の GraphQL API Explorer を使って自分の活動の振り返りをする - mookjp.io](https://blog.mookjp.io/blog-ja/github-graphql-explorer/)]。
今年仕事で取り組んだ内容は下記になります。

- MySQL8バージョンアップのアプリケーション側の対応
- 管理画面VersionUp対応
- フリーキーテストを直す
- CakePHP4.2のFixture対応
- バッチのユニットテストの開発体験をちょっとだけ良くする対応
    - [vierge-noire/cakephp-fixture-factories: CakePHP Fixture Factories](https://github.com/vierge-noire/cakephp-fixture-factories)を導入
    - DIコンテナを導入
- デプロイ頻度、PRのリードタイムの計測基盤開発
- PHP8.1対応
- テストカバレッジ計測対応
- Datadog導入のアプリケーション側対応
    - APMとログの連携
    - version追跡の対応
    - ログフォーマットのjson化対応
- コンテナのイメージサイズ削減対応

こうして見るとかなりいろいろなことをやってきたことが分かります。

マージされたPRの一覧からは読み取れない仕事もあって、開発生産性計測やDatadog関連では社内技術基盤のカスタマーサクセスっぽいムーブが多かったです。

## Output

### Speaking

3つのイベントに参加して、計4つのセッションでトークしました。

- [開発組織の生産性を可視化する State of DevOpsとFour Keysとは / deep dive into State of DevOps - Speaker Deck](https://speakerdeck.com/isanasan/deep-dive-into-state-of-devops)
- [「LeanとDevOpsの科学」を実践して LancersのDevOps的取り組みとこれから / Lancers' DevOps efforts and the future - Speaker Deck](https://speakerdeck.com/isanasan/lancers-devops-efforts-and-the-future)
- [今あらためて考える PHPに型定義をする理由 / why use type hint and static analyse at php - Speaker Deck](https://speakerdeck.com/isanasan/why-use-type-hint-and-static-analyse-at-php)
- [開発組織の生産性を可視化するState of DevOpsとFour Keysとは(増補改訂版) / Introduction to State of DevOps and Four Keys for Visualizing Productivity in Development Organizations expanded and revised edition - Speaker Deck](https://speakerdeck.com/isanasan/introduction-to-state-of-devops-and-four-keys-for-visualizing-productivity-in-development-organizations-expanded-and-revised-edition)

Four Keys関連のトークが中心でした。特にPHP Con 2022での発表は評判が良くて嬉しかったです。

### Writing

zennに9記事投稿しました。
よく読まれた記事はこのあたり

- [Pull requestの理想的なサイズとその理由](https://zenn.dev/isana/articles/ideal-size-of-pull-request-and-why)
- [24のケイパビリティがいつのまにか27のケイパビリティになっていた件](https://zenn.dev/isana/articles/24capability-update-27capability)
- [Rectorの独自ルールを作成する方法(2022年版)](https://zenn.dev/isana/articles/rector-tutorial-2022)

週一で聞いたポッドキャストのまとめを書こうとした時期もありましたが早々に挫折しました。
ポッドキャストは`ながら聞き`が多いのでメモを取れないんですよね。

## Learning

### Books

今年読んだ本のうち特に良かったのは以下の3冊です。

- [私たちはどう学んでいるのか: 創発から見る認知の変化 (ちくまプリマー新書 403) | 鈴木 宏昭 |本 | 通販 | Amazon](https://www.amazon.co.jp/%E7%A7%81%E3%81%9F%E3%81%A1%E3%81%AF%E3%81%A9%E3%81%86%E5%AD%A6%E3%82%93%E3%81%A7%E3%81%84%E3%82%8B%E3%81%AE%E3%81%8B-%E5%89%B5%E7%99%BA%E3%81%8B%E3%82%89%E8%A6%8B%E3%82%8B%E8%AA%8D%E7%9F%A5%E3%81%AE%E5%A4%89%E5%8C%96-%E3%81%A1%E3%81%8F%E3%81%BE%E3%83%97%E3%83%AA%E3%83%9E%E3%83%BC%E6%96%B0%E6%9B%B8-%E9%88%B4%E6%9C%A8-%E5%AE%8F%E6%98%AD/dp/448068431X/ref=asc_df_448068431X_nodl?tag=jpgo-22&linkCode=df0&hvadid=588963902335&hvpos=&hvnetw=g&hvrand=17020413620805368409&hvpone=&hvptwo=&hvqmt=&hvdev=m&hvdvcmdl=&hvlocint=&hvlocphy=1009461&hvtargid=pla-1662726905881&psc=1&th=1&psc=1&dplnkId=e3a11205-1f7c-4ee0-9666-94997d75ec25)
- [The DevOps ハンドブック 理論・原則・実践のすべて | ジーン・キム, ジェズ・ハンブル, パトリック・ボア, ジョン・ウィリス, 榊原 彰, 長尾 高弘 |本 | 通販 | Amazon](https://www.amazon.co.jp/DevOps-%E3%83%8F%E3%83%B3%E3%83%89%E3%83%96%E3%83%83%E3%82%AF-%E7%90%86%E8%AB%96%E3%83%BB%E5%8E%9F%E5%89%87%E3%83%BB%E5%AE%9F%E8%B7%B5%E3%81%AE%E3%81%99%E3%81%B9%E3%81%A6-%E3%82%B8%E3%83%BC%E3%83%B3%E3%83%BB%E3%82%AD%E3%83%A0/dp/4822285480/ref=asc_df_4822285480_nodl?tag=jpgo-22&linkCode=df0&hvadid=295678107984&hvpos=&hvnetw=g&hvrand=13053745427372248536&hvpone=&hvptwo=&hvqmt=&hvdev=m&hvdvcmdl=&hvlocint=&hvlocphy=1009461&hvtargid=pla-527091971189&psc=1&th=1&psc=1&dplnkId=befa05ed-f0dd-46d0-b5bd-d1d078527e19)
- [Software Architecture Metrics ](https://www.oreilly.com/library/view/software-architecture-metrics/9781098112226/)

書籍以外だと、DORAの DevOps Capabilities を全部読むなどしました。

### Article

今年も毎日沢山の記事を読みました。仕事や人生の参考になるものばかりでしたが、中でも1番衝撃的だった記事がこちらです。

[経営とソフトウェアエンジニアリングの接続 - WEB SALAD](https://web-salad.hateblo.jp/entry/2022/09/30/130000)

この記事を読んで、慌ててこの本を購入しました。

[新版　財務3表一体理解法 (朝日新書) | 國貞　克則 | ビジネス・経済 | Kindleストア | Amazon](https://www.amazon.co.jp/dp/B08W4YZTBZ/ref=nodl_?tag=yasaichi0c-22&linkCode=ogi&th=1&psc=1&dplnkId=6961b106-9b00-47aa-b1ed-dd84d784c0dd)

2023年はエンジニアリングの枠を飛び出して、コーポレートファイナンスの世界に足を踏み入れていこうと思います。

### Tech

今年新しく触れた技術スタックは以下です。

- メタプログラミング
    - というかRectorを使ったAST操作
- terraform 
- BigQuery
- JS/TS
- deno
- GraphQL
- Datadog 

可処分時間が限られているなかで今後のキャリアをデザインするためには、特定の技術スタックに集中して投資し、軸となる得意領域を持つことが大切だと考えています。
今年はPHPと型検査という得意領域を軸にしてRectorを使った大規模な自動リファクタリングに挑戦しました。
開発生産性の計測プロジェクトでは完全に今までの技術スタックとは異なるチャンレンジでしたが、リーン思考というドメインは自分の得意分野であるため程良くコンフォートゾーンを飛び出すことができたと思います。
来年以降も、無闇に新しいことを覚えようとせず、仕事を中心に投資効果を考えながら技術をキャッチアップしていきたいと思います。

## Home

相変わらず家事育児が大変で、可処分時間どころか8時間勤務も結構難しい状態が続いています。幸いフルリモートかつフレックス勤務なので、9時5時で7時間勤務して足りない分は子供が起きる前の早朝か、就寝してからの夜間に勤務してカバーしています。
それもこれも妻の勤務先がブラックすぎるのが原因なので、サステナビリティの無い働き方を強要する会社は早く滅びてほしいものです。

## Resolution

来年はチームの体制がいきなり変わり、カバーする範囲が一気に増えることが既に確定しています。ある意味これはチャンスで、仕事で新しい領域をキャッチアップできるので、今年以上に来年も楽しくやっていこうと思います。
