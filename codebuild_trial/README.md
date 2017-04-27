# CIを待ちたくない気持ち -AWS CodeBuild試用-
subtitle
:   2016/12/20 オプト社内ハッカソン

===

# 問題意識
ADPLAN v7のCI実行が遅くて、頭が痛い

![](quote1.png){:relative_width="80"}

![](quote2.png){:relative_width="50"}

![](quote3.png){:relative_width="80"}

# やったこと
AWSから出た新サービス「CodeBuild」を試そう！

* Dockerベース
* 従量課金
* CircleCIと違い同時ビルド数の制約なし
* 使えるインスタンスは3タイプ、最大だと15 GB memory, 8 vCPU

# 結果

* まともにテストを走らせるには至らず
  * MySQLにちゃんと接続できていないっぽい。。。
* でもコンパイルまで15分程度で終わってるので、希望はありそう
  * CircleCIだとコンパイルだけで25分くらいかかる

# 感想
* Docker image準備がめんどくさい
* .ivy2をキャッシュしてくれない
* うまく動かないときの調査がつらい
* CloudWatchで結果を見ることになるが、色がつかないので見づらい

# まとめ
* 自分のDocker力の低さが明るみに
* CircleCI、実は偉大だった
* とはいえ継続調査はしたいよね
