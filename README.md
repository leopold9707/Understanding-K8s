# [翔泳社 しくみがわかる Kubernetes](https://www.shoeisha.co.jp/book/detail/9784798157849) サンプルコード [工事中]

## 第1部 導入編

## 第2部 基本編

## 第3部 実践編

### サンプルの設計方針

* Terraformを主に使います
  * Azure関連リソースとKubernetes関連リソースをまとめて作成できることを重視しました
* Terraformでの管理単位を、共用リソース(shared)、AKSクラスター(cluster-xxx)で分割しています。ライフサイクルとリスクプロファイルが異なるためです
  * さらに該当する章ではBlue/Greenクラスターで分割しています
  * deploy/cleanup用 ヘルパーbashスクリプトからTerraformを実行します
* シークレットは主に環境変数で渡していますが、よりセキュアにするにはAzure Key Vaultもおすすめです
* サンプルToDoアプリのコンテナーイメージはDocker Hubで公開しています。ソースは[shared/app/todo](https://github.com/ToruMakabe/Understanding-K8s/tree/master/shared/app/todo)にあります
* 実行方法は各章のREADMEをご覧ください
* 以下環境でテストしています
  * Windows Subsystem for Linux (Ubuntu 18.04)
  * macOS Mojave 10.14.2
  * Azure CLI 2.0.52
  * Terraform 0.11.10

### chap08-12-all-in-one

第3部で説明した環境を全部入りで作成できます。各章で都度環境を作成、削除したくない時はこちらを。
クラスターが4つ作成されますので、コストやリソース制限にご注意を。

### chap08

第8章、可用性に関する設計、機能を試すコードです。Primary/Failover 2つのクラスターで冗長化します。

* Primary/Failover 2つのAKSクラスター
* PrimaryとFailoverはリージョンを分けて作成可能
* 共有リソースとしてAzure Cosmos DBとAzure Traffic Manager
* サンプルToDoアプリ

### chap09

第9章、拡張性に関する設計、機能を試すコードです。Cluster Autoscalerを導入します。

* 1つのAKSクラスター
* Cluster Autoscaler
* NGINX Deploymentマニフェスト (Pending状態のPod作成用)

### chap10

第10章、保守性に関する設計、機能を試すコードです。Blue/Green 2つのクラスターで冗長化します。

* Blue/Green 2つのAKSクラスター
* 共有リソースとしてAzure Cosmos DBとAzure Traffic Manager
* サンプルToDoアプリケーション
* Kured関連マニフェスト
* NGINX Deploymentマニフェスト (Cordon/Drainの挙動確認用)

### chap11

第11章、リソース分離に関する設計、機能を試すコードです。Azure AD(Active Directory)との認証統合を設定します。Azure AD認証なしの演習オプションも用意しました。

* 1つのAKSクラスター
* Azure Active Directory統合設定
* リソース分離関連マニフェスト (Namespace、Role、Role Bindingなど)
* 負荷がけ用アプリ

### chap12

第12章、可観測性に関する設計、機能を試すコードです。Azure Monitor関連の設定をします。

* 1つのAKSクラスター
* Azure Monitor関連設定