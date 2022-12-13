<!-- vpc endpoint -->
{
    "Version": "2012-10-17",
    "Id": "SourceIP",
    "Statement": [
        {
            "Sid": "SourceIPAndVPCe",
            "Effect": "Deny",
            "Principal": "*",
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::s3-test-ecs/*",
            "Condition": {
                "StringNotEquals": {
                    "aws:SourceVpce": "vpce-0a23398e8144e3ce8"
                }
            }
        }
    ]
}


<!-- iam -->
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:ListAllMyBuckets",
            "Resource": "arn:aws:s3:::*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:ListBucketVersions" <=「以前のバージョンの復元」機能を使用する場合に必要
            ],
            "Resource": "arn:aws:s3:::my-bucket"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:DeleteObject",
                "s3:PutObject",
                "s3:GetObjectVersion", <= バージョニングの設定を有効にしている場合に必要
                "s3:DeleteObjectVersion", <= Wasabi / RSTOR でバージョニングを使用する場合に必要
                "s3:GetObjectACL", <= ACL オプションを有効にしている場合に必要
                "s3:PutObjectACL" <= ACL オプションを有効にしている場合に必要
            ],
            "Resource": "arn:aws:s3:::my-bucket/*"
        }
    ]
}
