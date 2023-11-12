# EC2
* disable_api_termination
  * 終了保護を有効にする場合「true」とする
* iam_instance_profile
  * ec2起動後iam設定（aws configure）があらかじめ設定された状態になるかも。

## LB（Loard Brancer）
  * [作成方法](https://dev.classmethod.jp/articles/terraform-alb/)
### 【疑問点】
  * Moduleについて
    * module内でsgなどのresourceを記述しても実行されない。もしくは適応されない。
  * 勝手にdefaultのsgが作成される。
    * awsの使用の可能性あり。