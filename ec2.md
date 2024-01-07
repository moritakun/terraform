# EC2

## 作成方法
1. ec2の作成:
   * **ec2.tf**ファイルに以下のコードを追加します。
      ```text
      # EC2
      # https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance
      resource "aws_instance" "sample_instance" {
        ami = "ami-07c589821f2b353aa" # Ubuntu Server 22.04 LTS(無料利用枠の対象)
        instance_type = "t2.micro" # (無料利用枠の対象)
        subnet_id = "${aws_subnet.public_1a.id}"
        vpc_security_group_ids = [aws_security_group.sample_sg.id] # 指定しない場合、defaultが自動的に付与される
        associate_public_ip_address = true # パブリックIPを割り当てる（動的）
        key_name = "sample-key-pair"
        tags = {
          Name = "sample-instance"
        }
      }
      ```
* disable_api_termination
  * 終了保護を有効にする場合「true」とする
* iam_instance_profile
  * ec2起動後iam設定（aws configure）があらかじめ設定された状態になるかも。
* associate_public_ip_address = true # パブリックIPを割り当てる（動的）
  * [terraformでこれ関連でエラーが出た際に役立ちそう](https://qiita.com/TBT/items/1e87604293842efa0743)

### LB（Loard Brancer）
  * [作成方法](https://dev.classmethod.jp/articles/terraform-alb/)
#### 補足
* SGの指定をしないと、defaultが設定される。