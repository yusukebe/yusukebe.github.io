# 僕の見た<br />Perlコミュニティと<br />これから

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

___

### 今年書いたコード

- Bokete-Delta
  - [ボケて](http://bokete.jp/) の内部コード=「Bokete」
  - Alpha => Beta => Gamma => **Delta** <- 今ココ
  - 今年でほぼ完成まで持ち込んだ
  - 企業とのコラボ、スマホやアプリ対応 etc.
- Shodo
  - 次期Boketeバージョンで使うために開発

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
        limit => { isa => 'Int', default => 20, optional => 1, documentation => '...' }
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
                    entries => [ { title => 'Hello', body => 'This is an example.' } ]
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
- `Shodo::Test::JSONRPC` (ネーミング再考の必要あり)
- リクエストパラメータをテストの中で記述
- モック内のレスポンスをそのままJSONで表示
- テストを走らせる => ドキュメント共有@GitHub
- 補足は*README.md*に書いておく

___

### 今年使い始めたモジュール

- Cinnamon
- Carton
- SQL::Maker
- Harriet
- JSON::RPC
- OAuth::Lite2
- etc.

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
- 一人暮らしをはじめる ラーメンを食い過ぎて太る
- 自炊にはまる
- 若干痩せる

___

### 今年は色々なところへ行きました！

- 大阪 => Kansai.pm
- 台湾 => 視察
- アメリカ => YAPC::NA + サンフランシスコ見学
- 熱海 => 合宿 + 温泉 etc.
- 福岡 => Fukuoka.pm

___

###

