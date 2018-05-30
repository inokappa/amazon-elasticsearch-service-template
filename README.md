# Amazon Elasticsearch Service クラスタ作成用テンプレート

## なにこれ

* Amazon Elasticsearch Service クラスタを VPC 内に作成する CloudFormation テンプレート
* 任意の環境 (本番環境, ステージング環境等) 毎にパラメータ用 JSON ファイルを用意する必要がある
* [direnv](https://github.com/direnv/direnv) を使って, AWS\_PROFILE 等を管理することを前提としている

## 最初に手動なりで作っておくもの

* direnv で利用する .envrc ファイル
* VPC, VPC サブネット, 及びセキュリティグループ

## このテンプレートで作成されるもの

### Amazon Elasticsearch Service クラスタ

* 指定したサブネット内に Amazon Elasticsearch Service クラスタ

## パラメータ用 JSON ファイル

parameters ディレクトリ以下に, 以下のようなパラメータ用の JSON ファイルを用意する.

```sh
$ tree parameters/
parameters/
└── demo.json

0 directories, 1 file
```

demo.json は, 以下のように記載する.

```json
[
  {
    "ParameterKey": "EsDomainEnvironment",
    "ParameterValue": "demo"
  },
  {
    "ParameterKey": "EsDomainNamePrefix",
    "ParameterValue": "oreno-elasticsearch"
  },
  {
    "ParameterKey": "EsInstanceType",
    "ParameterValue": "t2.small.elasticsearch"
  },
  {
    "ParameterKey": "EsInstanceCount",
    "ParameterValue": "1"
  },
  {
    "ParameterKey": "EsVersion",
    "ParameterValue": "6.2"
  },
  {
    "ParameterKey": "EsZoneAwareness",
    "ParameterValue": "false"
  },
  {
    "ParameterKey": "EsStorageVolumeSize",
    "ParameterValue": "10"
  },
  {
    "ParameterKey": "EsSecurityId",
    "ParameterValue": "sg-xxxxxxxx"
  },
  {
    "ParameterKey": "EsSubnetIds",
    "ParameterValue": "subnet-xxxxxxx1, subnet-xxxxxxx2"
  }
]
```

## デプロイスクリプトの使い方

### デプロイスクリプトについて

* AWS CLI をシェルスクリプトでラップして, 更に Rake でラップしている
* 詳細は Rakefile を確認する

### 準備

```sh
bundle install --path vendor/bundle
```

### create stack

```sh
bundle exec rake cfn:create:debug
```

### update stack

```sh
bundle exec rake cfn:update:debug
```

### delete stack

```sh
bundle exec rake cfn:delete:debug
```

### validate template

```sh
bundle exec rake cfn:check:debug
```
