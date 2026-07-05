このユニットでは、Azure Resource Manager テンプレート (ARM テンプレート) を使用して Infrastructure as Code を実装する方法について学習します。ARM テンプレートの各セクションを概観し、ARM テンプレートを Azure にデプロイする方法を学び、ARM テンプレートの *resources* セクションについて詳しく掘り下げます。

## Infrastructure as Code とは

*Infrastructure as Code* を使用すると、アプリケーションに必要なインフラストラクチャをコードで記述できます。

Infrastructure as Code では、アプリケーション コードと、アプリケーションのデプロイに必要なすべてのものを、中央のコード リポジトリで一元管理できます。Infrastructure as Code の利点は次のとおりです。

- 構成の一貫性
- スケーラビリティの向上
- デプロイの高速化
- 追跡可能性の向上

次のビデオでは、Infrastructure as Code について説明しています。

> [!VIDEO https://channel9.msdn.com/Blogs/One-Dev-Minute/What-is-Infrastructure-as-Code--One-Dev-Question/player?format=ny]

## ARM テンプレートとは

ARM テンプレートは、デプロイのインフラストラクチャと構成を定義する JavaScript Object Notation (JSON) ファイルです。テンプレートでは、*宣言型構文*を使用します。宣言型構文とは、制御フローを記述することなく、リソースがどのような状態であるべきかを示す構造と要素を組み立てる方法です。宣言型構文は、コンピューターに実行させるコマンドを使用する*命令型構文*とは異なります。命令型のスクリプトは、リソースをデプロイする各ステップを指定することに焦点を当てています。

ARM テンプレートを使用すると、リソースを作成するための一連のプログラミング コマンドを書くことなく、デプロイしたい内容を宣言できます。ARM テンプレートでは、リソースと、それらのリソースのプロパティを指定します。その情報を基に、[Azure Resource Manager](/azure/azure-resource-manager/management/overview?azure-portal=true) が、整理された一貫性のある方法でリソースをデプロイします。

### ARM テンプレートを使用する利点

ARM テンプレートを使用すると、デプロイを自動化し、Infrastructure as Code (IaC) のプラクティスを採用できます。テンプレート コードは、インフラストラクチャおよび開発プロジェクトの一部になります。アプリケーション コードと同じように、IaC ファイルをソース リポジトリに保存してバージョン管理できます。

ARM テンプレートは*べき等*です。つまり、同じテンプレートを何度デプロイしても、同じ種類のリソースが同じ状態で得られます。

Resource Manager は、リソースが正しい順序で作成されるように、リソースのデプロイをオーケストレーションします。可能な場合、リソースは並列で作成されるため、ARM テンプレートによるデプロイはスクリプトによるデプロイよりも速く完了します。

  :::image type="content" source="../media/2-template-processing.png" alt-text="テンプレート処理手順の対応関係を示す図。スクリプトを処理するための複数の呼び出しとは対照的に、テンプレートの処理には 1 回の呼び出ししか必要ありません。" border="false":::

Resource Manager には検証機能も組み込まれています。デプロイを開始する前にテンプレートをチェックし、デプロイが成功することを確認します。

デプロイがより複雑になった場合は、ARM テンプレートをより小さく再利用可能なコンポーネントに分割できます。これらの小さなテンプレートは、デプロイ時にリンクしてつなぎ合わせることができます。テンプレートを別のテンプレートの中に入れ子にすることもできます。

Azure portal では、デプロイ履歴を確認し、デプロイの状態に関する情報を取得できます。ポータルには、すべてのパラメーターと出力の値が表示されます。

また、ARM テンプレートは、[Azure Pipelines](https://azure.microsoft.com/services/devops/pipelines?azure-portal=true) などの継続的インテグレーションおよび継続的デプロイ (CI/CD) ツールに統合することもできます。これにより、リリース パイプラインを自動化し、アプリケーションとインフラストラクチャを迅速かつ確実に更新できます。Azure DevOps と ARM テンプレート タスクを使用することで、プロジェクトを継続的にビルドしてデプロイできます。

### ARM テンプレート ファイルの構造

ARM テンプレートを書く際には、テンプレートを構成するすべての部分と、それぞれの役割を理解しておく必要があります。ARM テンプレート ファイルは、次の要素で構成されます。

| 要素        | 説明 |
| -------------- | --- |
| **schema** | JSON データの構造を記述する JSON スキーマ ファイルの場所を定義する必須セクション。使用するバージョン番号は、デプロイのスコープと JSON エディターによって異なります。 |
| **contentVersion** | テンプレートのバージョン (1.0.0.0 など) を定義する必須セクション。この値を使用してテンプレートの重要な変更を記録し、正しいテンプレートをデプロイしていることを確認できます。 |
| **apiProfile** | リソースの種類に対する API バージョンのコレクションを定義する省略可能なセクション。この値を使用すると、テンプレート内のリソースごとに API バージョンを指定する必要がなくなります。 |
| **parameters** | デプロイ時に指定する値を定義する省略可能なセクション。これらの値は、パラメーター ファイル、コマンドライン パラメーター、または Azure portal で指定できます。 |
| **variables** | テンプレート言語式を簡潔にするために使用する値を定義する省略可能なセクション。 |
| **functions** | テンプレート内で使用できる[ユーザー定義関数](/azure/azure-resource-manager/templates/template-user-defined-functions?azure-portal=true)を定義できる省略可能なセクション。複雑な式がテンプレート内で繰り返し使用される場合、ユーザー定義関数を使うとテンプレートを簡潔にできます。 |
| **resources** | リソース グループまたはサブスクリプションにデプロイまたは更新する実際の項目を定義する必須セクション。 |
| **output** | デプロイの最後に返される値を指定する省略可能なセクション。 |

## ARM テンプレートを Azure にデプロイする

ARM テンプレートは、次のいずれかの方法で Azure にデプロイできます。

- ローカル テンプレートをデプロイする
- リンクされたテンプレートをデプロイする
- 継続的デプロイ パイプラインでデプロイする

このモジュールでは、ローカルの ARM テンプレートのデプロイを中心に扱います。今後の Learn モジュールでは、より複雑なインフラストラクチャのデプロイ方法や、Azure Pipelines との統合方法を学習します。

ローカル テンプレートをデプロイするには、[Azure PowerShell](/powershell/azure/install-az-ps) または [Azure CLI](/cli/azure/install-azure-cli?azure-portal=true) のいずれかがローカルにインストールされている必要があります。

まず、Azure CLI または Azure PowerShell を使用して Azure にサインインします。

# [Azure CLI](#tab/azure-cli)

```azurecli
az login
```

# [PowerShell](#tab/azure-powershell)

```azurepowershell
Connect-AzAccount
```

---

次に、リソース グループを定義します。既に定義済みのリソース グループを使用することも、次のコマンドで新しいリソース グループを作成することもできます。使用可能な場所の値は、`az account list-locations` (CLI) または `Get-AzLocation` (PowerShell) で取得できます。既定の場所は `az configure --defaults location=<location>` で構成できます。

# [Azure CLI](#tab/azure-cli)

```azurecli
az group create \
  --name {name of your resource group} \
  --location "{location}"
```

# [PowerShell](#tab/azure-powershell)

```azurepowershell
New-AzResourceGroup `
  -Name {name of your resource group} `
  -Location "{location}"
```

---

リソース グループに対するテンプレートのデプロイを開始するには、Azure CLI コマンドの [az deployment group create](/cli/azure/deployment/group#az-deployment-group-create) または Azure PowerShell コマンドの [New-AzResourceGroupDeployment](/powershell/module/az.resources/new-azresourcegroupdeployment) を使用します。

> [!TIP]
> `az deployment group create` と `az group deployment create` の違いは、`az group deployment create` が非推奨となる予定の古いコマンドであり、`az deployment group create` に置き換えられるという点です。そのため、リソース グループ スコープでリソースをデプロイする際は、`az deployment group create` の使用をお勧めします。

どちらのコマンドにも、リソース グループ、リージョン、およびデプロイの名前が必要です。名前を付けることで、デプロイ履歴の中でそのデプロイを簡単に識別できます。便宜上、演習ではテンプレート ファイルへのパスを格納する変数を作成します。この変数を使うと、デプロイのたびにパスを入力し直す必要がなくなるため、デプロイ コマンドを実行しやすくなります。次に例を示します。

# [Azure CLI](#tab/azure-cli)

このデプロイ コマンドを実行するには、[最新バージョン](/cli/azure/install-azure-cli)の Azure CLI が必要です。

```azurecli
templateFile="{provide-the-path-to-the-template-file}"
az deployment group create \
  --name blanktemplate \
  --resource-group myResourceGroup \
  --template-file $templateFile
```

# [PowerShell](#tab/azure-powershell)

```azurepowershell
$templateFile = "{provide-the-path-to-the-template-file}"
New-AzResourceGroupDeployment `
  -Name blanktemplate `
  -ResourceGroupName myResourceGroup `
  -TemplateFile $templateFile
```

---

複雑なソリューションをデプロイするには、リンクされたテンプレートを使用します。テンプレートを複数のテンプレートに分割し、メイン テンプレートを通じてそれらのテンプレートをデプロイできます。メイン テンプレートをデプロイすると、リンクされたテンプレートのデプロイがトリガーされます。リンクされたテンプレートは、SAS トークンを使用して保存し、保護できます。

CI/CD パイプラインは、ARM テンプレート プロジェクトを含む開発プロジェクトの作成とデプロイを自動化します。テンプレートのデプロイに使用される最も一般的な 2 つのパイプラインは、Azure Pipelines と [GitHub Actions](/training/paths/github-actions/?azure-portal=true) です。

これら 2 種類のデプロイの詳細については、他のモジュールで説明します。

## テンプレートにリソースを追加する

テンプレートにリソースを追加するには、リソース プロバイダーとそのリソースの種類を知っておく必要があります。この組み合わせの構文は、*{リソース プロバイダー}/{リソースの種類}* という形式です。たとえば、ストレージ アカウント リソースをテンプレートに追加するには、`Microsoft.Storage` リソース プロバイダーが必要です。このプロバイダーの種類の 1 つが `storageAccount` です。したがって、リソースの種類は `Microsoft.Storage/storageAccounts` と表記されます。必要なプロバイダーは、[Azure サービスのリソース プロバイダー](/azure/azure-resource-manager/management/azure-services-resource-providers?azure-portal=true)の一覧から探すことができます。

プロバイダーとリソースの種類を定義したら、使用したい各リソースの種類のプロパティを理解する必要があります。詳細については、「[Azure Resource Manager テンプレートでのリソースの定義](/azure/templates?azure-portal=true)」を参照してください。リソースを見つけるには、左側の列の一覧を確認します。プロパティは API バージョンごとに整理されている点に注意してください。

:::image type="content" source="../media/2-resource-type-properties.png" alt-text="ストレージ アカウントのドキュメントが選択されている Microsoft ドキュメント ページのスクリーンショット。":::

Storage Accounts ページに記載されているプロパティの一部の例を次に示します。

![ストレージ アカウントのプロパティの一部を示す Microsoft ドキュメント ページのスクリーンショット。](../media/2-storage-account-properties.png)

このストレージの例では、テンプレートは次のようになります。

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.1",
  "apiProfile": "",
  "parameters": {},
  "variables": {},
  "functions": [],
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2025-01-01",
      "name": "learntemplatestorage123",
      "location": "westus",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "StorageV2",
      "properties": {
        "supportsHttpsTrafficOnly": true
      }
    }
  ],
  "outputs": {}
}
```
