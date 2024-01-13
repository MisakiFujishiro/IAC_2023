# gitlabとjiraの連携
## 連携単位
連携はJIRAのアカウント単位と、GitLabのグループ単位で連携を行うことができる。
GitLabのグループは設定から追加ができる。



## 設定手順
SaaSのgitlabとjiraを利用しているのか、Server上のものを利用しているのかで、利用するプラグインが異なる。  
今回はGitlab.com for Jira Cloudを利用して設定手順を整理する。

|プラグインの名称|対象製品|手順|
|:----|:----|:----|
|[GitLab.com for Jira Cloud](https://marketplace.atlassian.com/apps/1221011/gitlab-com-for-jira-cloud?hosting=cloud&tab=overview)|GitLab Saas と Jira Cloud版の連携に使用する|[手順書](https://support.atlassian.com/ja/jira-cloud-administration/docs/integrate-gitlab-with-jira/)|
|[GitLab Connector for Jira Software](https://marketplace.atlassian.com/apps/1224039/gitlab-connector-for-jira-software?tab=overview&hosting=datacenter)|GitLab Self-Managed と Jira DataCenter版・Server版 の連携に使用する|[手順書](https://aslead.nri.co.jp/products/gitlab/column/introduction-of-gitlab-connector-for-jira-software.html)|



基本的には、公式の
[手順書](https://support.atlassian.com/ja/jira-cloud-administration/docs/integrate-gitlab-with-jira/)
に従って、設定を行う。
### マーケットプレイスのインストール
Atlassian Marketplace に進んで GitLab.com for Jira Cloud アプリをインストール

![](../img/jira_gitlab_setting_1.png)
### jira側の設定
1. Jira の [アプリを管理] ページで、GitLab for Jira アプリの詳細を展開して [開始] を選択

![](../img/jira_gitlab_setting_2.png)

2. Sign in to gitlabを選択してgitlabを認証
3. Linkの画面で連携するgitlabでPJを選択

![](../img/jira_gitlab_setting_3.png)


4. API Tokenの取得    
[こちらのURL](https://id.atlassian.com/manage-profile/security/api-tokens)からAPIを発行し、取得したAPIキーをメモしておく記憶しておく(gitlabの設定で利用)

### gitlab側の設定
1. プロジェクトに移動して [設定] > [統合] の順に選択します。
2. [統合を追加] で [Jira] を選択します。

![](../img/jira_gitlab_setting_4.png)

3. Jira サイトの詳細を次のように入力します。
    - Web URL - Jira サイトの URL (例: https://myjirasite.atlassian.net)
    - ユーザー名またはメール アドレス - Jira プロファイルに登録されているユーザー名またはメール アドレス。
    - パスワードまたは API トークン - 先ほど作成したAPI トークンを作成してクリップボードにコピー & ペーストします。
4. [変更を保存] を選択

### 統合の設定
Gitlabのアクション（CommitやMergeRequest）に応じて、Jira側のIssueにどのようなアクションを反映させるかの設定を行う。

![](../img/jira_gitlab_setting_5.png)

|設定名|設定項目|内容|
|:----|:----|:----|
|Triger|Commit/Merge Request|GitlabのCommitやMerge Requestのアクションに対して、JIRAのイベントを発行するかを設定する|
|コメント設定|True/False|GitlabのCommitやMerge Requestのアクションの記録をコメントとして残すか否かを設定する|
||Standard|コミットタイトルやブランチ名が表示される|
| |Detail|コミットメッセージも表示される|
|Jira Issueを最終状態に移行|True/False|Gitlabのアクションに応じて、イシューを移動させるかの設定|
| |完了に移動|完了に移動させる|
| |カスタムトランジション|カスタム設定をして、所定の状態に移動させる|

最後に、Jira issue matchingを設定する。これは、Gitlabが紐付けるJIRAのIssueを発見するための設定。




## JIRAからGITLABの操作
### JIRAからBranchを作成
連携が完了すると、jiraの課題やIssueからBranchを作成することが可能になる。

![](../img/jira_gitlab_branch_1.png)

ブランチを作成を押下すると、gitlabのページに移動して、ブランチを作成するProjectとブランチ名を指定する。

![](../img/jira_gitlab_branch_2.png)


### コミットの管理・MRの管理
gitlabでのコミットメッセージおよびMergeRequestのコメントにをJIRAに反映させることができる。
コミットメッセージに、`PJID-NUM`を入れておくと、対象のJIRAのIssueにメッセージが反映される。

作成したブランチのコミットメッセージにIDを追加しておく
![](../img/jira_gitlab_commit_1.png)


jiraの画面から、「すべての開発状況を表示ボタン」から連携状況を見ると、コミットのメッセージが反映されている

![](../img/jira_gitlab_commit_2.png)




### より高度なコミットの管理・MRの管理
#### JIRAのコメントへのGitlabのアクション反映
上記のCommitやMerge RequestのアクティビティをJIRAのコメントに反映させることができる。
CommitとMerge Requestどのアクションでコメントをするかやどのレベルのメッセージを反映させるかは、gitlab側の設定である「統合の設定」で定義可能

以下の例では、MRのすべての詳細を有効化していた場合。

![](../img/jira_gitlab_comment_connect.png)


#### MRでIssueを完了にする
gitlab側の設定である「統合の設定」で行った設定で「Jira Issueを最終状態に移行」を有効にしておくと、ブランチがMergeされた際に、Issueをクローズさせることができる。

Closeについては、コミットと同様に、`Close PJID-NUM`と記述しておくと連携をして、移動させておいてくれる。


#### 詳細なルール設定
MRでIssueを完了にするだけでなく、JIRAからBranchを作成、MRを作成したタイミングでもステータスを変更することができる。

例えば、下表のように設定するとJIRA側から進行状況が分かりやすくなる。
|アクション|状態|
|:----|:----|
|ブランチ作成|進行中|
|MR作成|RV中|
|MR完了（Close）|完了|


設定方法は以下
- プロジェクト設定
- 自動化
- ルール作成

![](../img/jira_gitlab_flow.png)

作成ルールは以下にすると良い
|トリガ設定|条件設定|アクション設定|
|:----|:----|:----|
|branchの作成|ステータスがTODOと等しい|課題のトランジションで、進行中に変更|
|PullRequestの作成|ステータスが進行中と等しい|課題のトランジションで、RV中に変更|
|PullRequestのマージ|ステータスがRVと等しい|課題のトランジションで、完了に変更|

![](../img/jira_gitlab_rule.png)

## GITLABからJIRAの操作
GITLAB側で`PJID-NUM`を設定すると、自動でLINKが設定される。

gitlabで作業をしている際に、どのJIRAの課題に紐づいているかをワンクリックで確認できる。

![](../img/jira_gitlab_connect.png)





### JIRAからIssue作成（プレミアム）
gitlabがプレミアムの場合に、JIRAからIssueを発行できる。



