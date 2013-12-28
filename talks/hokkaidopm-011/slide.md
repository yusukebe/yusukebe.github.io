## これからはじまります

![papix](images/papix.jpg)

___

# 今年見た<br />Perlコミュニティ<br />そしてこれから

### Yusuke Wada a.k.a. yusukebe

#### 2013-12-28
#### Hokkaido.pm#11

___

## 自己紹介

- 和田裕介 / 1981年12月23日生まれ
- 横浜 / 鎌倉 / 熱海
- (株) ワディット代表取締役
- (株) オモロキ取締役兼最高技術責任者
- 一般社団法人 Japan Perl Association 理事
- Webアプリケーションデベロッパー

___

## 飛行機で来ました^^

![地図](images/map.png)

___

## 本題の前に...

> 今年書いたコードとか

___

### 主に...

![ボケて](images/bokete.png)

___

### 今年の実績

- ピーク時 **250-300req/1sec**
- iOS+Androidアプリ **280万インストール**
- **Yahoo! Japan**その他と連携

> そして...

___

### 第17回**メディア芸術祭<br />審査委員会推薦作品**

![メディア芸術祭](images/media.png)

___

### Bokete-Delta

- ボケての内部コード「**Bokete**」
- Alpha => Beta => Gamma => **Delta** <- 今ココ
- 今年でほぼ完成まで持ち込んだ
- 企業とのコラボ、スマホやアプリ対応 etc.

___

### Shodo

- 次期Boketeバージョンで使うために開発
- Rubyのautodocに触発される
- HTTP::Request / HTTP::Responseを食わせる
- ドキュメントをMarkdown出力
- JSON-RPCのAPIで利用
- `Shodo` / `Shodo::Suzuri` / `Shodo::Hanshi`

___

### use Shodo #01

    my $shodo = Shodo->new( document_root => 'sample_documents' );
    my $suzuri = $shodo->new_suzuri('get_entries');

    my $parameters = {
        method => 'get_entries',
        params => { category => 'technology', limit => 1 },
    };
    $suzuri->params(
        category => { isa => 'Str', documentation => '...' },
        limit => { isa => 'Int', default => 20,
                   optional => 1, documentation => '...' }
    );
    ok $suzuri->validate($parameters->{params}); # Validate Parameter

    my $req = POST '/endpoint';
    $req->content(to_json($parameters));
    $suzuri->request($req); # Pass Request Object

___

### use Shodo #02

    my $res = HTTP::Response->new(200);
    $res->content(
        to_json(
            {
                result => {
                    entries => [{ title => 'Hello', body => 'It is fine tody.' }]
                },
            }
        )
    );
    $suzuri->response($res); # Pass Response Object

    $shodo->stock($suzuri->doc());
    $shodo->write('test.md'); # Write the Markdown to file

___

### Markdown形式でドキュメント出力

![Markdown](images/shodo.png)

___

### 実際使っている

- JSON-RPCのAPIを試験するため
- `Test::Shodo::JSONRPC`
- リクエストパラメータをテストの中で記述
- モック内のレスポンスをそのままJSONで表示
- テストを走らせる => ドキュメント共有@GitHub
- 補足は*README.md*に書いておく

___

### 今年使い始めたライブラリ

- Cinnamon
- Carton
- SQL::Maker
- Harriet
- JSON::RPC
- OAuth::Lite2
- reveal.js *(JS)*
- **AngularJS** *(JS)*
- etc.

___

## AngularJS

> あんぎゅらーじぇいえす

___

### AngularJSを勉強してたら<br />Gigazineに載ってた...

![Gigazine](images/gigazine.png)

___

### on HTML

![HTML](images/html.png)

___

### on JS

```
var app = angular.module('myApp', []);
app.controller('MyController', function($scope){
  var nextTitle = 'Hello Hokkaido!';
  $scope.changeTitle = function() {
    var currentTitle = $scope.title;
    $scope.title = nextTitle;
    nextTitle = currentTitle;
  };
});
```

___

## デモ

___


<div ng-controller="MyController" ng-init="title='Hello Tokyo!'">
  <h2>{{ title }}</h2>
  <button ng-click="changeTitle()"
   style="font-weight:bold;font-size:1.4em;background-color:#ccc;border-radius:0.2em;padding:0.2em;">Change Title</button>
</div>

___

### 今年使い始めたサービス

- Amazon Web Services
  - EC2
  - ELB
  - RDS
  - ElastiCache
  - SES
- Travis-CI
- Uptimer

___

### 今年のプライベート

- **炎上**
- 一人暮らしをはじめる
- ラーメンを食い過ぎて太る
- 自炊にはまる
- 若干痩せる

___

### 12月23日(誕生日)

![チキン](images/jisui.jpg)

___

> ところで

___

### この地図なーんだぁ！

![地図2](images/map2.png)

___

### 今年は色々なところへ行ったよぉ！

- 大阪 => Kansai.pm
- 台湾 => 視察
- アメリカ => YAPC::NA + サンフランシスコ見学
- 熱海 => 合宿 + 温泉 etc.
- 福岡 => Fukuoka.pm
- 五反田 => Perl入学式
- 渋谷 => PerlCasual / Shibuya.pl
- 八王子 => Hachioji.pm

___

### 賞もいただいたぉ！

![ベストトーク賞](images/prize.jpg)

___

### JPA知事にも就任ぽよ！

![JPA](images/jpa.png)

___

## 今回のボツネタ

> **登記を支える技術**

___

### まとめると...

- Boketeのコードたくさん書いて
- 色んなところに行って
- YAPCでベストトーク賞を取って
- JPAの理事になった！

___

## 結果...

___

### ベストトーク賞の副賞について

> JPAの中の人がJPAが出す<br />副賞で海外行くのおかしい...

僕は賞品無しで結果繰り上げ ＼(^o^)／

___

## それはおいといて...

___

海外を含めいろんなPerlコミュニティを見てきたので
その**個人的まとめ**と、JPA理事になったから今後やりたいことの**妄想話**をします

___

### Perlでよいなって思うところ

どこかな〜？

___

### その大きな一つはCPANとPAUSE

![CPAN](images/cpan.png)

___

### CPANでよかったと思う点

- 集約されているからGitHub等を彷徨う必要がない
- 当然ながら`CPANシェル`や`cpanm`でサクッと入る
- ネームスペースが暗黙的に切られている
- `SYNOPSIS`が分かりいい
- CPAN Testersの存在

> そして... **顔写真が出る！**

___

search.cpan.org/**~miyagawa**/Plack-1.0030

![miyagawa](images/miyagawa.png)

___

### 誰がつくってるか？が一目瞭然！

> そういえばBoketeでも...

___

### 使用モジュールの作者が身近

- Plack / Starman / Carton => *miyagawa*
- Mouse / Data::Validator / HTML::FillInForm::Lite => *gfuji*
- Router::Boom / FormValidator::Lite => *tokuhirom*
- DBIx::Skinny => *nekokak*
- Devel::KYTProf => *onishi*
- Test::mysqld / Server::Starter => *kazuho*
- Cinnamon => *shibazaki*

___

### 顔がわかると...

- キャラクターで判断出来る
- さらに日本人作者だと...
- 気楽に本人に質問出来る
- ドキュメントやBlog記事で使い方を把握出来る
- ユーザー同士で使い方を議論出来る

> ただし！日本国内の<br />ドメスティックなコンテキストによる？

___

## YAPC::NA 2013

![YAPC::NA](images/yapcna.jpg)

___

#### Inside Bokete: <br />Web Application with Mojolicious and others.

![mytalk](images/mytalk.jpg)

___

### 質問した

> Webアプリケーションはどうやって動かしている？

期待した答え => Starman / Starlet etc...

**返ってきた答え**

> nginx、Apache

___

> うっ...

___

### 当然だがコンテキストが異なる

- 英語が伝わってないだけかも知れないが...
- よく使っているモジュールを知らない人が多かった
- Web系のアプリを実践している人が少ない？
- `Catalyst`は根強い

> モジュールが輸出されるといいか？問題

___

### そういう経験が出来たからこそ！

> 海外カンファレンスに行くのは<br />非常に刺激を受けますね^^

___

### ぶっちゃけスゲー楽しかった

![YAPC::NA](images/yapcna2.jpg)

___

### YAPC::NA厨

- 特にYAPC::NAは参加しやすかった
- `Where are you from ?` で話しかけられる
- 一人で積極的に英語で絡んでいく唯一の機会
- 日に日に英語が聞けるようになっていった！
- みんなが海外に行ける機会を増やせればいいのかにゃ...

___

## タオツポス...

![T-shirts](images/t-shirts.jpg)

___

## 話を国内に...

___

### Kansai.pm 第15回ミーティング

![Kansai.pm](images/kansaipm.jpg)

___

### 個性が出てた

- @shibu_yu36さんの**Cinnamon**
- @goccy54さんの**コピペ検出** など
- ライトな話からコアな話まで

> 「関西」だけにいろんな人がいるなー<br />って印象

___

### ちなみに...大阪は

食い物が安い！さすが天下の台所

![串かつ](images/kushikatsu.jpg)

___

### Fukuoka.pm #24

![Fukuoka.pm](images/fukuokapm.jpg)

___

### 和気あいあいとしてた

- @h.satoshiさんの**クイズ○ービー**が面白かった
- 福岡の人の発表が少なかったのが残念？
- 屋台カルチャーなのかいろんな人と知り合った

> いい意味での仲間感がよかった

___

### ちなみに...福岡は

魚もうまーーーい！

![魚](images/sakana.jpg)

___

### PerlCasual #05 & Shibuya.pl #01

![PerlCasual](images/perlcasual.jpg)

___

### 学びがある

- LINEさんのカフェ非常に良い
- [@koba04さんのサービスつくった話](http://koba04.com/slide/perl-casual-5/)
- [@fujiwaraさんのPlack/PSGIおさらい話](http://dl.dropboxusercontent.com/u/224433/plackcon/index.html)
- 個人的には@bayashiさんの小ネタがツボ
- こう言っちゃなんだけど**つぶぞろい感**すごい

___

### Perl入学式

![Perl入学式](images/perlentrance.jpg)

___

### 新境地を感じる

> こんなPerlやりたい人いたのか！！

- 丁寧な教えとサポート
- テーブル毎に参加者が教え合っている
- かなり**ビックリ**した

___

### ちなみに寿司が安くてウマい

![寿司](images/sushi.jpg)

___

### Hachioji.pm #34

![Hachioji.pm](images/hachiojipm.jpg)

Photo by @uzulla

___

### 温泉いい！その1

- リラックスした状態でコード書くのよい
- ハッカソン形式なので自然と学びあえる
- タイ料理も美味かった

___

### ちなみに...八王子は

意外と近かった...

![地図](images/map3.png)

___

## 温泉といえば...

___

### 温泉発火村 #2

![温泉発火村](images/onsen.jpg)

___

### 温泉いい！その2

- 進捗なかったけど得るものがあった
- @karupaneruraさんが主催
- 熱海の山木旅館さん
- 今まで話したことない人と技術話出来た

> Dropboxのキーバリューみたいな<br />APIあるらしいよ

とか！

___

### ちなみに...熱海は

定食屋の飯がウマい

![石川屋](images/ishikawaya.jpg)

___

## ここで一旦まとめ

___

- **各々のPM毎に雰囲気が全然違う**
- **地元の人がどんどん表に出るといいかも**
- **温泉はだいぶブレークスルー感ある**

___

なによりも...

## Perlという共通言語を<br />持って各地に行くと<br />楽しくて刺激を受けるよ！

___

## Perl Mongerよ<br />旅に出よ！

___

そして**たくらみ**

___

> 地方活性はするんだけれどもそれ以前にいろんなところに行きたい！
> し、いろんなところに行くといいと思う！

___

## 温泉.pm !?

___

![ツイート](images/tweet.png)

___

![ツイート](images/tweet2.png)

___


### 温泉.pmの妄想

- 参加者が旅館や料理屋についてBlogを書く
- その代わり優遇してもらう
- 宿ごとの施設などの情報が溜まっていく
- Win-Winじゃね？

___

### 現実的なやり方

- 本格的にやるのは2015年度くらいから？
- 来年は有志でやっていく
- 地方自治体や地元の観光協会に実績がわかるように
- ここだけの話「熱海」だと融通が効くかも

___

## そうすると...

> いい感じの3本柱が立つ

___

- **YAPC::Asiaを含むイベント**
- **Perl入学式より派生する教育**
- **地方活性化と称して温泉.pm**

> あくまで現段階では個人的な妄想です^^

___

### 出来るか分からないけどアクティブにしていきます

___

## 最後のまとめと抱負

___

### 2013年と2014年

- コードを書いてまだまだ学びたいと思いました
- いろんなところに行って楽しかったです
- 来年は**YAPCをやる側**としてチャレンジ
- もっと**コントリビュート**したい！

___

## おしまい

