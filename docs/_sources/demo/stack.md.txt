# LambdaとEvent作成フロー
## 開発環境準備
### gitlabのリポジトリ作成
lambdaとEventBridgeを作成するので、lambda-eventと言うリポジトリを作成する。
このリポジトリに、lambdaとEventBridgeを作成するテンプレートファイルを格納していく。

![](../img/demo-make-gitlab.png)

### ローカルでの開発準備
ローカルで開発をしていくために作成したPJをローカルにCloneする。


### ミラーリング設定
codecommitでHTTPSのURLを取得し、CodeCommitのミラーリング用のIAMユーザーで作成した`ServiceUserName@`をhtts://の後ろに挿入
```
# 取得したHTTPSのgitURL
https://git-codecommit.ap-northeast-1.amazonaws.com/v1/repos/codecommit-dev-cfn-ProjectX

# 挿入後
https://user-dev-codecommit-mirroring-at-XXXXXXXXXXXX@git-codecommit.ap-northeast-1.amazonaws.com/v1/repos/codecommit-dev-cfn-ProjectX
```

gitlab側で、設定からミラーリポジトリを開いて、各種情報を設定してミラーリングを行う。
![](../img/demo-mirroring.png)
- URL：上記で作成した挿入後のURL
- ユーザー名：ServiceUserName
- パスワード：ServicePassword

ミラーリング設定を行なったら、gitlabでミラーリングの更新ボタンを押下すると、codecommit側にgitlabの中身が確認できる。







# スタックの作成
## Roleの作成
### Roleのスタック作成
### codedeployのRole修正
### codepipelineのRole確認

## Eventの作成
### Eventのスタック作成
### codedeployのRole確認

## Lambdaの作成
### Lambdaのスタック作成
### codedeployのRole確認
