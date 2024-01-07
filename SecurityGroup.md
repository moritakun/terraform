# SecurityGroup

## 作成方法

1. SecurityGroupの作成:
   * **SecurityGroup.tf**ファイルに以下のコードを追加します。
      ```text
      # SecurityGroup
      # https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group#example-usage
      resource "aws_security_group" "sample_sg" {
        name        = "sample_sg"
        description = "Allow TLS inbound traffic"
        vpc_id      = aws_vpc.sample_vpc.id

        # インバウンド
        ingress {
            description      = "TLS from VPC"
            from_port        = 443
            to_port          = 443
            protocol         = "tcp"
            cidr_blocks      = [aws_vpc.sample_vpc.cidr_block]
        }

        # アウトバウンド
        egress {
            from_port        = 0
            to_port          = 0
            protocol         = "-1"
            cidr_blocks      = ["0.0.0.0/0"]
        }

        tags = {
            Name = "sample-sg"
        }
      }
      ```