# Terraform Wiki

- tfファイルはHCL (HashiCorp Configuration Language) と呼ばれる、HashiCorp社開発の独自記法でコードを書く必要があります。

| ファイル名   | ファイルの定義内容                                                                             |
| ------------ | ---------------------------------------------------------------------------------------------- |
| main.tf      | "AWS" などTerraformを実行する環境（プロバイダーと呼ぶ）を定義                                  |
| variables.tf | Terraformで使用する変数を定義（変数は他のtfファイルから${var.変数名}やvar.変数名で参照できる） |
| vpc.tf       | VPCを作成するためのリソースを定義                                                              |
| ec2.tf       | EC2を作成するためのリソースを定義                                                              |
| output.tf    | 作成したEC2のパブリックIPアドレスを出力する設定を定義                                          |
| terraform.tfvars    | variables.tfのdefaultで定義したものに指定の値を再定義(Gitignoreに設定するファイル)            |