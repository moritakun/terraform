# VPC

## 作成方法
1. Terraformのプロジェクトの作成:
   * 新しいディレクトリを作成し、そのディレクトリに移動します。
   * Terraformの設定ファイル（**main.tf**）を作成します。
2. VPCの作成:
   * **main.tf**ファイルに以下のコードを追加します。
        ```text
        # プロバイダ定義"AWS"を指定
        provider "aws" {
            region ="ap-northeast-1"  # 使用するリージョンを指定します
        }

        # VPC
        # https://www.terraform.io/docs/providers/aws/r/vpc.html
        resource "aws_vpc" "sample_vpc" {
            cidr_block = "10.0.0.0/16"  # VPCのCIDRブロックを指定します
            tags={
                Name = "sample-vpc"  # VPCの名前を指定します
            }
        }
        ```
3. Terraformの初期化と実行:
   * コマンドラインでTerraformのプロジェクトディレクトリに移動します。
   * **terraform init**コマンドを実行して、Terraformの初期化を行います。
   * **terraform apply**コマンドを実行して、VPCの作成を開始します。
   * TerraformがAWSにリソースを作成するために必要な変更を表示し、承認を求めるメッセージが表示されます。yesと入力して承認します。

### Appendix
* terraform initでエラーが出た場合（参考：[【初心者向け】MacにTerraform環境を導入してみた](https://dev.classmethod.jp/articles/beginner-terraform-install-mac/)）
    ```text
    cat: /usr/local/Cellar/tfenv/3.0.0/version: No such file or directory
    Version could not be resolved (set by /usr/local/Cellar/tfenv/3.0.0/version or tfenv use <version>)
    ```
    1. ターミナルを開きます。
    2. **tfenv list** コマンドを実行して、インストールされているTerraformのバージョンを確認します。
    3. インストールされているバージョンの中から使用したいバージョンを選び、**tfenv use < version >** コマンドを実行します。ここで **< version >** は使用したいTerraformのバージョンに置き換えてください。
        ```text
       もし必要なバージョンがインストールされていない場合は、tfenv install <version> コマンドを使用してインストールできます。
        ```
        ```text
        terraformのバージョンのリストを確認する場合は、tfenv list-remote コマンドを使用して確認できます。
        ```
