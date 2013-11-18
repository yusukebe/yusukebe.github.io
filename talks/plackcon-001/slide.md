# Mojoliciousの<br />知りたいコト

### Yusuke Wada a.k.a. yusukebe

#### 2013-11-20
#### Shibuya Plack/PSGI Conference (shibuya.pl) #1

___

### 質問

> Mojolicious使っている人ー？(^o^)／

---

Mojolicious力高い人少なそうなので^^

---

### Mojoliciousの知りたいことコト

___

### No.1

> フルスタックってほんと？

---

### Answer

- 機能が揃っているかという意味では**No**
- 機能を自作しているという意味では**Yes**

---

### コアモジュール以外には非依存

    $ cpanm Mojolicious

---

### 例えば最近...

Mojolicious::Validatorが追加された

    my $validator  = Mojolicious::Validator->new;
    my $validation = $validator->validation();

    $validation->input({ message => 'Hello Mojolicioius' });
    $validation->required('message')->size(1, 140);
    if ($validation->has_error()) {
        ...;
    }

実に簡素！

---

特に統合されてて便利！とかじゃないので使わない...？

---

### フルスタックといえども<br />他のモジュールは使う...

___

### No.2

> Mojolicious::Liteで簡単につくれるの？

---

### Answer

これは便利。"code"形式のOAuthアプリを試すとか...

    $ mojo generate lite_app app.pl

---

```
get '/' => sub {
  my $self = shift;
  $self->stash->{message} = 'Hello Mojolicious';
  $self->render('index');
};
app->start;
__DATA__

@@ index.html.ep
<html>
  <body>Message: <%= $message %></body>
</html>
```

---

### テンプレ周りがそこそこ便利

---

### テンプレートをファイルに分離

    $ mkdir templates
    $ emacs templates/index.html.ep

---

### ヘルパーの機能より

templates/layouts/default.html.ep

をレイアウトファイルとして使う

    % layout 'default'; 

___

### No.3

> plackupとかで立ち上げられる？

---

### Answer

Mojolicious::Liteの場合...

    $ plackup app.pl

自動で識別

---

Mojoliciousアプリの場合...

### use Mojo::Server::PSGI;

---

.psgi ファイルつくってます！

    my $psgi = Mojo::Server::PSGI->new( app => Bokete::Web->new );
    my $app  = $psgi->to_psgi_app;
    builder {
        enable...;
        $app;
    };

___

### No.4

> 付属のサーバは使わないの？

---

### 2個ある

- morbo - 開発用
- hypnotoad - 本番用

---

## けど使ってない！

確か遅かったから...

---

### 改めてベンチマーク

    get '/' => sub {
        my $self = shift;
        my $param = $self->req->param('foo');
        $self->stash->{message} = 'x' x 12 . $param;
        $self->render('index');
    };

    app->start;
    __DATA__

    @@ index.html.ep
    % layout 'default';
    % title 'Welcome';
    Message: <%= $message %>
    ...;

ref. <http://kazeburo.hatenablog.com/entry/2013/04/15/173407>

---

### 開発向けサーバ


    # morbo
    Requests per second:    154.40 [#/sec] (mean)

    # plackup
    Requests per second:    152.97 [#/sec] (mean)

---

### 本番用サーバ

    # hypnotoad 10 workers
    Requests per second:    566.82 [#/sec] (mean)

    # starman 10 workers
    Requests per second:    602.90 [#/sec] (mean)

    # starlet 10 workers
    Requests per second:    731.37 [#/sec] (mean)

---

### hypnotoadもそこそこ？

#### そういえばホットデプロイ出来る

立ち上げる

    $ hypnotoad app.pl

リロード

    $ hypnotoad app.pl

停止

    $ hypnotoad -s app.pl

---

### でも...

- .psgiをつくってplackup/starmanとかで動かしている
- Plack::Middleware::* が使える
- 複数アプリをマウント出来る

___


