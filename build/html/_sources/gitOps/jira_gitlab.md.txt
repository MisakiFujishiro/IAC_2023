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
### gitlab側の設定
1. プロジェクトに移動して [設定] > [統合] の順に選択します。
2. [統合を追加] で [Jira] を選択します。

![](../img/jira_gitlab_setting_4.png)

3. Jira サイトの詳細を次のように入力します。
    - Web URL - Jira サイトの URL (例: https://myjirasite.atlassian.net)
    - ユーザー名またはメール アドレス - Jira プロファイルに登録されているユーザー名またはメール アドレス。
    - パスワードまたは API トークン - API トークンを作成してクリップボードにコピー & ペーストします。
4. [変更を保存] を選択

### 統合の設定
★★★★★要確認★★★★★
![](../img/jira_gitlab_setting_5.png)



## 連携機能
### JIRAからBranchを作成
連携が完了すると、jiraの課題やIssueからBranchを作成することが可能になる。

![](../img/jira_gitlab_branch_1.png)

ブランチを作成を押下すると、gitlabのページに移動して、ブランチを作成するProjectとブランチ名を指定する。

![](../img/jira_gitlab_branch_2.png)

### ブランチの管理
#### コミット管理
作成されたブランチに対する、コミットやマージリクエストの状態を一覧で確認することが可能で、進捗状況を見ることができる。

コミットを管理するためには、gitlabでBranchを修正する際のコミットメッセージに、`PJID-NUM`を入れる。

![](../img/jira_gitlab_branch_4.png)


#### MR管理
MRについては、2つの方法でMRとJIRAの課題を紐づけることができる
- JIRAから作成されたブランチについては、自動的に作成元の課題と紐付けられる  
![](../img/jira_gitlab_branch_3.png)

- コミットと同様にMRのコメントに`PJID-NUM`を追加すると、対象の課題とMRも紐付けられる。
    以下の例では、SCRUM-11から作成されたMRだがコメントにSCRUM-3と入っているので両方の課題に紐付けられる
![](../img/jira_gitlab_branch_5.png)



★★★★★MRしたらストーリーを完了に移動できるかチェック★★★★★


### JIRAからIssue作成（プレミアム）
gitlabがプレミアムの場合に、JIRAからIssueを発行できる。




## おすすめの利用方法




# 参考サイト
- [GitLab（ギットラボ）とJira（ジラ）を連携しよう！「GitLab Connector for Jira Software」とは](https://aslead.nri.co.jp/products/gitlab/column/introduction-of-gitlab-connector-for-jira-software.html)
- [JiraとGitLabの連携してもっと便利に使おう！](https://qiita.com/_superdry/items/e4f30cdedc14da6ddf83)
- [JIRAとGitLabを連携して、マージリクエストがマージされた際自動でステータス移動をできるようにする](https://zenn.dev/maronn/articles/d973dd85980070)
- [GitLabとJIRAの連携で出来ることをメモ](https://rimever.hatenablog.com/entry/2020/06/13/000000)