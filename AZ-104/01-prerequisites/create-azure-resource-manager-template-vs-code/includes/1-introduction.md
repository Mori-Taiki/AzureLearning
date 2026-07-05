JSON 形式の Azure Resource Manager テンプレート (ARM テンプレート) を使用すると、プロジェクトのインフラストラクチャを宣言的かつ再利用可能な方法で指定できます。テンプレートは、開発プロジェクトと同じソース管理でバージョン管理し、保存できます。

あなたは、パートナー企業向けの在庫管理システムを開発しているソフトウェア チームを管理しているとします。この製品を Azure にデプロイし、各パートナー企業がそれぞれ専用のソリューションを持てるようにする計画です。デプロイごとに異なる Azure ストレージ アカウントを使用して、異なるポリシーを実装する予定です。そこで、ARM テンプレートを使用した *Infrastructure as Code* のプラクティスを採用することにしました。このアプローチにより、さまざまなバージョンを追跡でき、各環境へのインフラストラクチャのデプロイに一貫性と柔軟性を確保できます。

このモジュールでは、ARM テンプレートの構造を紹介し、ARM テンプレートを作成して Azure にデプロイする練習を行います。

[!INCLUDE [Bicep introduction for JSON modules](../../includes/azure-template-json-bicep-intro.md)]

## 学習の目標

このモジュールでは、次のことを行います。

- Visual Studio Code を使用して JSON ARM テンプレートを実装する。
- リソースを宣言し、パラメーターと出力を追加してテンプレートに柔軟性を持たせる。

## 前提条件

- Azure portal、サブスクリプション、リソース グループ、リソース定義など、Azure に関する基本知識。
- Azure アカウント。無料アカウントは[こちら](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)から取得できます。
- [Visual Studio Code](https://code.visualstudio.com?azure-portal=true) がローカルにインストールされていること。
- 次のいずれか:
  - 最新の [Azure CLI](/cli/azure/install-azure-cli?azure-portal=true) ツールがローカルにインストールされていること。
  - 最新の [Azure PowerShell](/powershell/azure/install-az-ps?azure-portal=true) がローカルにインストールされていること。
