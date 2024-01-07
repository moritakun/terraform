# Internet Gateway

## 作成方法
1. Internet Gatewayの作成:
   * **InternetGateway.tf**ファイルに以下のコードを追加します。
        ```text
        # Internet Gateway
        # https://www.terraform.io/docs/providers/aws/r/internet_gateway.html
        resource "aws_internet_gateway" "sample_igw" {
            vpc_id = "${aws_vpc.sample_vpc.id}"
            tags = {
                Name = "sample-igw"
            }
        }
        ```


