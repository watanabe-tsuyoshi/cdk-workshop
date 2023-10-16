# ポイント
①ある処理を追加した際に、他のテストケースへ影響する点に注意
例：
指定不要だったパラメータを必須にする処理へ変更した
今まで、パタメータを指定していなかったテストケースでパラメータを追加する必要がある
そうしないと、今まで通ってたテストケースが通らないことがある

②デプロイ先のエンドポイントはlibではなくbinで定義されておりそちらを変更する必要がある
const app = new cdk.App();
new WorkshopPipelineStack(app, 'CdkWorkshopPipelineStack');

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

④git pushすると失敗する
fatal: unable to access 'https://git-codecommit.ap-northeast-1.amazonaws.com/v1/repos/WorkshopRepo/': The requested URL returned error: 403
↑
複数の gitconfig が存在しており、Keychain Access ユーティリティの認証情報でpushしていた
はじめは成功するが、以下の記述の通り一定時間経過すると機能しなくなる。
よって、codecommitのみのために使用するために、helper=osxkeychainがあるファイルをコメントアウトすれば解決する。
（そもそも設定している認証情報古い可能性もあるからそっちも一応要確認）

>セキュリティ上の理由により、CodeCommit リポジトリへのアクセス用に生成されるパスワードは一時的なものであり、約 15 分後にキーチェーンに保存されている認証情報は機能しなくなります。

参考：https://docs.aws.amazon.com/ja_jp/codecommit/latest/userguide/troubleshooting-ch.html

以下は本失敗と無関係なので気にしない
```
 Committer: XXXX <XXXX@XXXX.local>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author
```
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
