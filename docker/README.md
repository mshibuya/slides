# 雑にDocker使ってみたよ

subtitle
:   2017/8/22 「未挑戦は可能性のかたまり」共有会

allotted-time
:   10m

# 自己紹介
渋谷　充宏 @m4buya

* なんでも屋
* サーバーサイドプログラマだった
* Ruby / Scala / インフラ(New!)
* https://github.com/mshibuya
* RailsAdmin/CarrierWave committer

# アジェンダ
- Dockerとは
- なぜDockerか
- AWS CodeBuildでの利用
- CircleCI 2.0での利用
- Docker Compose
- まとめ

# Dockerとは
- 軽量コンテナ環境(雑)

![](https://www.docker.com/sites/default/files/Whale%20Logo332_5.png){:relative_width="30"}

# なぜDockerか
- 軽量
- コンテナ
- CIサービスみたいなのと相性がよい
  - テストに必要なものをあらかじめコンテナに入れておくことで、毎回インストールしていた時間を短縮できる
- Macでも動くし

# AWS CodeBuildでの利用
- v7のCIビルドに時間がかかっているので、移行先候補として検証
- コンテナベースのサービス
- AWS提供のプリセットのイメージ or カスタムイメージを選択可能

# AWS CodeBuildでの利用
- 単一のカスタムイメージを利用
  - ちょっと変更があるたびにDockerイメージを焼き直すのがめんどくさい。。。

# AWS CodeBuildでの利用
- Docker Composeにはそのままでは対応していないが、自分でインストールすれば使える
  - イメージ焼き直し問題は解決し、いい感じ

# AWS CodeBuildでの利用
- 並列ビルド制限がないのは超よい
- テスト実行結果がCloudWatchログでしか見れない！
  - 超見づらい
- この問題のため、CI実行環境としては採用せず

# CircleCI 2.0での利用
- コンテナベースになり、スペック選択可能になったりした
- v7ではカスタムイメージによりビルドしている(by中澤さん)
- Docker Composeも使える
https://github.com/opt-tech/v7-apps/blob/develop/.circleci/config.yml#L59

# Docker Compose
- 複数のDockerイメージを組み合わせて起動する方法を定義できる
- 開発環境構築に使うと、複数のミドルウェアをコマンド一発で起動可能になる
- めっちゃよい！！！

# Docker Compose
- これまで複数プロジェクト用のローカル開発環境を用意すると、ミドルウェアの複数バージョンをどう共存させるかが課題だった
- localhostのportにバインドできるので、普通にミドルウェアを入れるのと変わらない使い勝手

# Docker Compose
- ホストのディレクトリをコンテナにマウントしてそこにデータを保存すれば簡単に永続化できる
- ライフチェンジング

# Docker Compose
- 詳しくはこちら
https://github.com/opt-tech/v7-apps/tree/develop/docker

# まとめ
- Docker Compose超便利
- コンテナベースのデプロイとかもやりたいですねー
