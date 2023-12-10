# Subnet

## 作成方法
1. Subnetの作成:
   * **Subnet.tf**ファイルに以下のコードを追加します。
        ```text
        # Subnet
        # https://www.terraform.io/docs/providers/aws/r/subnet.html

        # Public Subnets
        resource "aws_subnet" "public_1a" {
            # 先程作成したVPCを参照し、そのVPC内にSubnetを立てる
            vpc_id            = "${aws_vpc.sample_vpc.id}"

            # Subnetを作成するAZ
            availability_zone = "ap-northeast-1a"

            cidr_block        = "10.0.1.0/24"
        
            tags = {
                Name = "sample-public-1a"
            }
        }
        
        resource "aws_subnet" "public_1c" {
            vpc_id            = "${aws_vpc.sample_vpc.id}"
            availability_zone = "ap-northeast-1c"
            cidr_block        = "10.0.2.0/24"
            tags = {
                Name = "sample-public-1c"
            }
        }
        
        # Private Subnets
        resource "aws_subnet" "private_1a" {
            vpc_id            = "${aws_vpc.sample_vpc.id}"
            availability_zone = "ap-northeast-1a"
            cidr_block        = "10.0.10.0/24"
            tags = {
                Name = "sample-private-1a"
            }
        }
        
        resource "aws_subnet" "private_1c" {
            vpc_id            = "${aws_vpc.sample_vpc.id}"
            availability_zone = "ap-northeast-1c"
            cidr_block        = "10.0.20.0/24"
            tags = {
                Name = "sample-private-1c"
            }
        }
        ```