# ポイント
①ある処理を追加した際に、他のテストケースへ影響する点に注意
例：
指定不要だったパラメータを必須にする処理へ変更した
今まで、パタメータを指定していなかったテストケースでパラメータを追加する必要がある
そうしないと、今まで通ってたテストケースが通らないことがある

②デプロイ先のエンドポイントはlibではなくbinで定義されておりそちらを変更する必要がある
const app = new cdk.App();
new WorkshopPipelineStack(app, 'CdkWorkshopPipelineStack');
git config --global credential.UseHttpPath true

③IAMユーザが作れないかつSSOユーザの認証情報が使える場合
認証情報設定
↓
git config --global credential.helper '!aws codecommit credential-helper $@'
git config --global credential.UseHttpPath true
↓
cloneなりremote addからのpushするなりができる

参考：
https://qiita.com/atsumjp/items/1fbd6aae3c8c00d62610
https://docs.aws.amazon.com/ja_jp/codecommit/latest/userguide/setting-up-https-unixes.html

# Welcome to your CDK TypeScript project

You should explore the contents of this project. It demonstrates a CDK app with an instance of a stack (`CdkWorkshopStack`)
which contains an Amazon SQS queue that is subscribed to an Amazon SNS topic.

The `cdk.json` file tells the CDK Toolkit how to execute your app.

## Useful commands

* `npm run build`   compile typescript to js
* `npm run watch`   watch for changes and compile
* `npm run test`    perform the jest unit tests
* `cdk deploy`      deploy this stack to your default AWS account/region
* `cdk diff`        compare deployed stack with current state
* `cdk synth`       emits the synthesized CloudFormation template
