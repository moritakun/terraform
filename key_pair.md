# Key pair

## 作成方法

1. key pairの作成
   * **key_pair.tf**ファイルに以下のコードを追加します。
   * key pairの作成
        ```text
        # tls_private_key
        # https://registry.terraform.io/providers/hashicorp/tls/latest/docs/resources/private_key
        resource "tls_private_key" "create_key_pair" {
            algorithm = "RSA"
            rsa_bits = 4096
        }
        ```
   * AWSのキーペアは公開鍵をopenssh形式で登録する必要があるので、３つめを利用します。
        ```text
        # 秘密鍵（PEMフォーマット）
        tls_private_key.create_key_pair.private_key_pem

        # 公開鍵（PEMフォーマット）
        tls_private_key.create_key_pair.public_key_pem

        # 公開鍵（OPENSSHフォーマット）
        tls_private_key.create_key_pair.public_key_openssh
        ```
   * 作成したキーペアをaws_key_pairリソースで、キーペアとして登録します。
        ```text
        # aws_key_pair
        # https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/key_pair#example-usage
        resource "aws_key_pair" "sample_key_pair" {
            key_name = "sample-key-pair"
            public_key = tls_private_key.create_key_pair.public_key_openssh

            tags = {
                Name = "sample-key-pair"
            }
        }
        ```
2. キーペアをローカルに保存する方法
    * localプロバイダを使用してローカルにファイルとして保存をする
    ```text
    # local_file（非推奨）
    # https://registry.terraform.io/providers/hashicorp/local/latest/docs/resources/file
    # local_sensitive_file（推奨）
    # https://registry.terraform.io/providers/hashicorp/local/latest/docs/resources/sensitive_file
    resource "local_sensitive_file" "keypair_pem" {
        filename = "${path.module}/keypair.pem"
        sensitive_content = tls_private_key.create_key_pair.private_key_pem
        file_permission = "0600" # 秘密鍵は権限を0600に変更する。
    }

    resource "local_sensitive_file" "keypair_pub" {
        filename = "${path.module}/keypair.pub"
        sensitive_content = tls_private_key.create_key_pair.public_key_openssh
        file_permission = "0600" # 公開鍵も権限を0600に変更する。（必須ではない。）
    }
    ```
