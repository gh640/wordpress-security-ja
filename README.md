# WordPress サイトのセキュリティ

WordPress サイトのセキュリティに関するまとめです。

## 攻撃の種類

WordPress サイトに対してよくある攻撃の種類として以下のようなものがあります。

- コードインジェクション
- <ruby>CSRF <rp>(></rp><rt>クロスサイト・リクエスト・フォージェリ</rt><rp>)</rp></ruby>
- ディレクトリ・トラバーサル
- アクセス制御・認可制御の不備の悪用
- セッション管理の不備の悪用
- ブルートフォースアタック
- クリックジャッキング
- DoS

WordPress サイトの運用時にはこれらの攻撃の可能性を考慮してリスクレベルに応じた防御施策を行うことが必要です。

## セキュリティ施策

WordPress サイトにおけるセキュリティ施策として以下のようなものがあります。

### 開発

- [ ] 一般的なウェブアプリケーションセキュリティの原則を学び実践する
- [ ] WordPress の適切な API を利用する
    - [ ] ユーザーの入力値・クライアントから送信されたデータにはインジェクション対策を行う
    - [ ] カスタムフォーム実装時には nonce の利用・チェックを行う
- [ ] カスタムテーマやカスタムプラグインの PHP ファイルへの直アクセスを拒否する
    - `defined( 'ABSPATH' ) || exit;`
- [ ] ユーザーロールと権限を適切に設定する
- [ ] ユーザー登録権限を適切に設定する
- [ ] クライアントからのリクエストデータや入力値に適切な上限値を設定する
- [ ] セキュリティ向上に有用な HTTP ヘッダーを付ける
    - [ ] `X-Content-Type-Options`
    - [ ] `X-Frame-Options`
    - [ ] `Cross-Origin-Resource-Policy`
    - [ ] `Strict-Transport-Security`
    - 参考: [HTTP Headers - OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Headers_Cheat_Sheet.html)

### デプロイ

- [ ] 設定ファイル `wp-config.php` で十分な強度の認証キーとソルトを設定する
    - [WordPress 公式の秘密鍵生成 API](https://api.wordpress.org/secret-key/1.1/salt/)
- [ ] ファイルとディレクトリのパーミッションを適切に設定する
- [ ] 直アクセスが必要無いファイルとディレクトリへのアクセスを拒否する
    - `wp-admin/`
    - `wp-includes/`
    - `wp-config.php`
    - その他開発用の `.txt` `.json` など
- [ ] 開発用のプラグインを無効化・削除する
- [ ] 開発用の機能を無効化する
    - `WP_DEBUG` など
- [ ] WordPress アカウントに十分な強度のパスワードを設定する
- [ ] 管理画面に HTTP 認証（ Basic 認証）をかける
- [ ] ログインページにブルートフォース対策を施す
    - reCAPTCHA など
- [ ] プロトコルには HTTPS を強制する
- [ ] データベースのユーザー名・パスワードには十分な強度のものを設定する

### サーバー運用

- [ ] ソフトウェアを適時更新する
    - [ ] WordPress コアを更新する
        - WordPress の自動更新機能を有効にする
        - 自動更新機能を使わない場合は別の方法で WordPress コアの更新を行う
    - [ ] プラグインを更新する
        - WordPress の自動更新機能を有効にする
        - 自動更新機能を使わない場合は別の方法でプラグインの更新を行う
    - [ ] テーマを更新する
    - [ ] Composer パッケージを更新する
    - [ ] NPM パッケージを更新する
    - [ ] PHP を更新する
    - [ ] HTTP サーバーを更新する
- [ ] WordPress アカウントの管理を適切に行う
    - [ ] アカウントの使い回しをしない
    - [ ] 使わなくなったアカウントは適時削除する
- [ ] セキュリティ強化プラグインを利用する
- [ ] ホスティング会社が提供するセキュリティ強化機能を利用する
- [ ] サーバーマシンへの接続に安全なプロトコル（ SSH / SFTP など）を使う
- [ ] サイトのバックアップを定期的に行う
- [ ] ファイヤウォールを利用する
- [ ] 攻撃の多いアクセス元を遮断する

### モニタリング

- [ ] アクセスログ・エラーログを出力する
- [ ] エラー発生時に管理者に通知を送り適時対応する

### 情報収集

- [ ] 関連するセキュリティ情報をウォッチする
    - [Security – WordPress News](https://wordpress.org/news/category/security/)

## 参考文献

- [Security – WordPress.org](https://wordpress.org/about/security/)
- [Hardening WordPress – WordPress.org Documentation](https://wordpress.org/documentation/article/hardening-wordpress/)
- [Security | Common APIs Handbook | WordPress Developer Resources](https://developer.wordpress.org/apis/security/)
- [OWASP Top Ten | OWASP Foundation](https://owasp.org/www-project-top-ten/)
- [安全なウェブサイトの作り方 | 情報セキュリティ | IPA 独立行政法人 情報処理推進機構](https://www.ipa.go.jp/security/vuln/websecurity/index.html)
