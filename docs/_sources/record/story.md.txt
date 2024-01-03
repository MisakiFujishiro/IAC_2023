# テーマ
複数チーム開発におけるIaC運用ルールの体系化と実践のための方法論

# ストーリー
[reveal](https://misakifujishiro.github.io/reveal_iac_2023/test.html#/0/1)

- Chap1: DevOpsとIaC
    - DevOpsの思想
        - DevOpsの価値
    - DevOpsに必要なもの
    - IaCの価値
        - DevOpsにおけるIaC・GitOpsの価値・役割
            - 見える化に寄与できる
- Chap2: IaCを運用する
    - アンチパターン
        - 対応すべきテーマの選定
            - 始め方がわからない。何から始めれば良いかわからない
            - 正しく運用されない。
- Chap3: IaCを始める
    - 始め方がわからないことに対する対策
        - CICDの価値
        - IaCとCICD・GitOpsについて
            - IaC単独：リソースの設定などを可視化できる
            - CICD：属人性を排除することができる
            - GitOps：環境への反映を可視化できる
    - スターターセット
- Chap4: IaCを運用する
    - 正しく運用されない問題に対する対策
        - コードの品質担保について：横展開
            - Readme
                - InputとOutputの明記
            - 命名規則
            - テンプレートの作成
                - テンプレートファイル（リソース単位か機能単位か）
                - MR
                - Issue
            - ソースコードのRV体制
        - テスト
        - 開発フローについて
            - JIRAとgitlab共通的な必要最低限のベストプラクティス利用方法
            - JIRAとgitlabの比較
                - 情報と知見の共有
                - チケット管理
                - ブランチ管理
                - PJ管理
                - 比較
                    - gitlab
                        - Epic/Issue/Branchを一気通貫でみれる
                        - Issue間の紐付けが苦手
                        - MileStoneなどで進捗管理が可能
                        - テンプレート化
                    - jiraではEpic/Issue
                        - Branchへの紐付けができない
                        - Issue間の紐付けなどは得意
                        - Agileの思想を強く受けているので可視化パターンが多い
                    - gitlabとjiraの組み合わせ
- Chap3: デモ


## ポイント
- JIRAとGitlabの利用方法について
    - 両者の対応比較表作成
        - 何が可視化できる？（コミットの数やチケットの消化率）
        - 何が得意（ブランチとチケットの連携か、スケジュール管理か）
    - 両者を組み合わせた方が良い場合や、gitlabやjiraがいい場合など
    - 管理者は何が可視化できるかなどに強い興味を持っていたりする
- 中間報告のコメント
    - 全く導入されれていない時にどこから始めればいいのか
    - 始め方などを教えてほしい

## スターターイメージ
![](../img/starterset-image.png)

## でもストーリー
![](../img/starterset-1.png)
![](../img/starterset-2.png)
![](../img/starterset-3.png)
![](../img/starterset-4.png)
