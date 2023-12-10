# Terraform Wiki

### 【前提】
* tfファイルはHCL (HashiCorp Configuration Language) と呼ばれる、HashiCorp社開発の独自記法でコードを書く必要があります。
* 原則、.tfは同階層(同じディレクトリ)に配置すること。

### 【構成】
|ファイル名|ファイルの定義内容|
|------------|-----------|
|main.tf|"AWS"などTerraformを実行する環境（プロバイダーと呼ぶ）を定義|
|variables.tf|Terraformで使用する変数を定義（変数は他のtfファイルから${var.変数名}やvar.変数名で参照できる）|
|vpc.tf|VPCを作成するためのリソースを定義|
|ec2.tf|EC2を作成するためのリソースを定義|
|output.tf|作成したEC2のパブリックIPアドレスを出力する設定を定義|
|terraform.tfvars|variables.tfのdefaultで定義したものに指定の値を再定義(Gitignoreに設定するファイル)|

### 当たり前実行手順（コマンド）
1. 初期化".terraform"ファイルが作成される
    ```text
    terraform init
    ```
2. ビルド
    ```text
    terraform plan
    ```
3. 実行、インフラアプリケーションの作成
    ```text
    terraform apply
    ```
4. 削除、インフラアプリケーションの削除
    ```text
    terraform destroy
    ```
### Appendix
* terraform initでエラーが出た場合
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
* tfenv
  * terraformのバージョン管理ができる。バージョンの切り替えが安易。
* tfstateファイル
  * 一番大切なファイル
  * terraformで管理しているインフラリソースを全て記載したjsonファイル
  * s3で管理するべきもの。ただしローカルで管理する場合は不要。