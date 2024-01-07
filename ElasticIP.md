# Elastic IP

## 料金
AWSのElastic IPは、固定的なパブリックIPv4アドレスを提供します。料金は以下のようになります。（公式は[こちら](https://aws.amazon.com/jp/ec2/pricing/on-demand/#Elastic_IP_Addresses)）

1. 割り当てられているが使用されていないElastic IP:

    Elastic IPがEC2インスタンスに関連付けられていない場合、または関連付けられているインスタンスが停止している場合、料金が発生します。

2. 追加のElastic IP:
   
   インスタンスに割り当てられているElastic IPが1つを超える場合、追加のElastic IPに対して料金が発生します。

3. Elastic IPの再マッピング:
   
   24時間以内に新しいまたは既存のElastic IPを同じインスタンスに再マッピングすると、料金が発生します。

```
注意点として、Elastic IPは使用しない場合は解放することを推奨します。使用していないElastic IPには料金が発生するためです。
```
* 0.005USD 実行中のインスタンスと関連付けられている追加の IP アドレス/時間あたり (プロラタベース)
* 0.005USD 実行中のインスタンスと関連付けられていない Elastic IP アドレス/時間あたり (プロラタベース)
* 0.00USD Elastic IP アドレスのリマップ 1 回あたり – 1 か月間で 100 リマップまで
* 0.10USD Elastic IP アドレスのリマップ 1 回あたり – 1 か月間で 100 を超えた追加のリマップについて

## 作成方法
1. ElasticIPの作成:
   * **ElasticIP.tf**ファイルに以下のコードを追加します。
        ```
        resource "aws_eip" "sample_eip" {
            vpc = true  # VPC内でElastic IPを使用する場合はtrueにします
        }
        ```
