# TerraForm
* 実行手順
  * terraform init
    * 初期化
    * .terraformファイルが作成される
  * terraform plan
    * ビルド
  * terraform apply
    * 実行、インフラアプリケーションの作成
  * terraform destroy
    * 削除、インフラアプリケーションの削除
* tfenv
  * terraformのバージョン管理ができる。バージョンの切り替えが安易。
* tfstateファイル
  * 一番大切なファイル
  * terraformで管理しているインフラリソースを全て記載したjsonファイル
  * s3で管理するべきもの。ただしローカルで管理する場合は不要。
* 仕様
  * 原則、.tfは同階層(同じディレクトリ)に配置すること。
* 構成
  * data
    * リソースの情報を取得できる
  * resource
    * リソースを作成できる
* ec2
  * disable_api_termination
    * 終了保護。有効にする場合「ture」とする
  * iam_instance_profile
    * ec2起動後IAM設定(aws configure)が予め設定された状態になるかも。
* LB
  * [作成方法](https://dev.classmethod.jp/articles/terraform-alb/)
* 疑問点
  * Moduleについて
    * module内でsgなどのresourceを記述しても実行されない。もしくは適応されない。
  * 勝手にdefaultのsgが作成される。
    * awsの使用の可能性あり。