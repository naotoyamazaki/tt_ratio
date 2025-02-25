# [T.T.LOG]

## サービス概要
T.T.LOGは卓球の試合映像を見ながら場面別(サーブ・レシーブ)や技術別(ドライブ・ツッツキ・ブロックなど)の項目をスピンボックスにてカウントしていくことでそれぞれの得点率が集計され、それに伴ったアドバイスがもらえる卓球専門の試合分析サービスです。

## 想定されるユーザー層
老若男女問わず卓球が趣味でよく大会に参加に参加される方。
自分のプレーを撮影して見返す方。

## サービスコンセプト
私は小学生から現在に至るまでアマチュア選手として卓球を続けてきており、現在は一般の方に卓球を指導する仕事をしています。
その経験の中で卓球をする方は「自分のプレーを客観視できておらず、必要のない練習をしてしまう」または「自分は何を練習したらいいのかわからない」などの課題感があります。
そして卓球をする方は自分の試合を撮影して後で見返すという習慣が浸透しています。
これらの課題感と習慣があることから撮影した動画を見ながら場面別(サーブ・レシーブ)や技術別(ドライブ・ツッツキ・ブロックなど)の項目をスピンボックスにてカウントしていくことでそれぞれの得点率が集計され、それに伴ったアドバイスがもらえるというサービスがあれば課題感の解決につながるのではないかと考えました。
卓球の競技者が自身のプレーを客観視できて練習内容の効率化を図ることで成長スピードを促進させることができるサービスにしていきたいです。

## 実装を予定している機能
### MVP
* 会員登録
* ログイン
* 試合分析結果一覧
* 場面別での得点率の分析フォーマット
* 場面別分析結果詳細
* 試合ごとのマルチ検索・オートコンプリート機能

### その後の機能
* 技術別の得点率分析フォーマット
* OpenAI APIによる分析アドバイス
* 1ゲームごとの分析フォーマット
* 練習メニュー提案
* パスワードリセット
* ログインの保持
* デモログイン
* X(旧Twitter)での共有機能
* マイページ更新

### 分析用データ
* 場面別
  * サーブ
  * レシーブ

* 技術別
  * フォアドライブ
  * バックドライブ
  * フォアツッツキ
  * バックツッツキ
  * フォアストップ
  * バックストップ
  * フォアフリック
  * バックフリック
  * チキータ
  * フォアブロック
  * バックブロック
  * フォアカウンター
  * バックカウンター

* ゲーム別
  * 1ゲーム目
  * 2ゲーム目
  * 3ゲーム目
  * 4ゲーム目
  * 5ゲーム目
  * 6ゲーム目
  * 7ゲーム目

## 機能の実装方針予定
### 場面別の分析とアドバイス機能について
  * サーブからの得点率が60％以上、レシーブからの得点率が40％以上の場合
　  →「サーブとレシーブどちらも安定しています。引き続きどちらもバランスよく練習していきましょう！」と表示。
  * サーブからの得点率が60％以上、レシーブからの得点率が40％以下の場合
　  →「サーブからの得点率が高いですね。ただレシーブからの得点率が少し低いのでレシーブからの展開を多めに練習していきましょう！」と表示。
  * サーブからの得点率が60％以下、レシーブからの得点率が40％以上の場合
　  →「レシーブからの得点率が高いですね。ただサーブからの得点率が少し低いのでサーブからの展開を多めに練習していきましょう！」と表示。
  * サーブからの得点率が60％以下、レシーブからの得点率が40％以下の場合
　  →「サーブからもレシーブからもあまり得点できていませんね。相手がかなり格上だったのかもしれません。気を取り直して引き続き練習頑張っていきましょう！」と表示。

### 技術別の分析とアドバイス機能について
  * 技術別の得点数と失点数を集計後に下記のプロンプトでOpenAI APIに分析リクエスト
　  以下は卓球の1試合で使用した技術ごとの得点数と失点数データです。このデータを基に、次の項目について日本語で簡潔にアドバイスを作成してください。
    なお、フォアプッシュはフォアツッツキ、バックプッシュはバックツッツキと表示してください。
    【得点が多く失点が少ない技術の活用方法】
    【得点が多いが失点も多い技術の改善方法】
    【得点が少なく失点が多い技術の改善方法】
    【使用頻度が低い技術や未使用技術の導入方法】

### 使用技術
* 開発環境: Docker
* サーバーサイド Ruby: 3.2.2, Rails: 7.1.2
* ユーザ登録及び認証機能: Sorcery
* マルチ検索・オートコンプリート機能: Stimulus Autocomplete（Rails7）
* フロントエンド: Javascript(importmap-railsによるモジュール管理)
* CSSフレームワーク: bootstrap: 5.3.2(cssbundling-railsによる統合)
* WebAPI: 
  - OpenAI API
  - TwitterAPI
* インフラ:
  - Webアプリケーションサーバ: heroku
  - データベースサーバ: PostgreSQL
* その他:
  - VCS: GitHub
  - CI/CD: GitHubActions

## 画面遷移図
https://www.figma.com/file/MJdJwaQDsET1HkfhQ1KO25/RUNTEQ%E7%94%BB%E9%9D%A2%E9%81%B7%E7%A7%BB%E5%9B%B3?type=design&node-id=427-798&mode=design&t=rC1St5srpN7nLmEV-0

## ER図
<a href="https://gyazo.com/0e84be89aa9908ae40d8ede02e6fbbba"><img src="https://i.gyazo.com/0e84be89aa9908ae40d8ede02e6fbbba.png" alt="Image from Gyazo" width="547"/></a>
