この演習では、Azure Resource Manager (ARM) テンプレートを作成して Azure にデプロイし、その後 ARM テンプレートを更新してパラメーターと出力を追加します。

## ARM テンプレートを作成する

1. Visual Studio Code を開き、*azuredeploy.json* という名前の新しいファイルを作成します。

1. 次のコードをコピーしてファイルに貼り付けます。

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {},
      "functions": [],
      "variables": {},
      "resources": [],
      "outputs": {}
    }
    ```

    このファイルには、前のユニットで説明した ARM テンプレートのすべてのセクションが含まれていることに注目してください。

1. <kbd>Ctrl+S</kbd> キーを押して、ファイルへの変更を保存します。

## ARM テンプレートを Azure にデプロイする

::: zone pivot="cli"

このテンプレートを Azure にデプロイするには、Visual Studio Code のターミナルから Azure アカウントにサインインする必要があります。[Azure CLI](/cli/azure/install-azure-cli) ツールがインストールされていることを確認してください。

1. **[ターミナル] > [新しいターミナル]** を選択して、ターミナル ウィンドウを開きます。

1. ターミナル ウィンドウのコマンド バーに **bash** と表示されていれば、作業に適したシェルが開いているので、次のセクションに進んでください。

    1. そうでない場合は、ドロップダウンを選択し、**[既定のプロファイルの選択]** を選択します。

          :::image type="content" source="../media/3-bash.png" alt-text="ドロップダウンに bash が表示されている Visual Studio Code ターミナル ウィンドウのスクリーンショット。":::

    1. **[Git Bash]** を選択します。

          :::image type="content" source="../media/3-select-shell-bash.png" alt-text="シェル選択のドロップダウンが表示されている Visual Studio Code ターミナル ウィンドウのスクリーンショット。":::

1. ARM テンプレート ファイルが保存されているフォルダーにディレクトリを移動します。

### Azure にサインインする

ターミナル ウィンドウで次のコマンドを実行して、Azure にサインインします。

```azurecli
az login
```

開いたブラウザー ウィンドウで、自分のアカウントにサインインします。サインインすると、このアカウントに関連付けられているサブスクリプションの一覧がターミナルに表示されます。既定のサブスクリプションにはアスタリスク (*) が付いています。複数のサブスクリプションがある場合は、この演習で使用するサブスクリプションを選択してください。

### 既定のリソース グループを作成して設定する

```azurecli
az group create --name <resource-group-name> --location <location>
```

*\<resource-group-name>* は、リソース グループの一意の名前に置き換えます。*\<location>* は、最寄りの Azure リージョンに置き換えます。たとえば、米国東部の場合は *eastus* を使用します。

既定のリソース グループを設定しておくと、この演習の Azure CLI コマンドからそのパラメーターを省略できます。リソース グループを設定するには、次のコマンドを実行します。

```azurecli
az configure --defaults group="<resource-group-name>"
```

*\<resource-group-name>* は、自分のリソース グループ名に置き換えてください。

### テンプレートを Azure にデプロイする

次のコマンドを実行して、ARM テンプレートを Azure にデプロイします。この ARM テンプレートにはまだリソースが含まれていないため、リソースは作成されません。デプロイは成功するはずです。

```azurecli
templateFile="azuredeploy.json"
today=$(date +"%d-%b-%Y")
DeploymentName="blanktemplate-"$today

az deployment group create \
 --name $DeploymentName \
 --template-file $templateFile
```

上記コードの前半では、デプロイするテンプレート ファイルへのパスとデプロイ名を含む Azure CLI の変数を設定しています。後半の ```az  deployment group create``` で、テンプレートを Azure にデプロイします。デプロイ名は `blanktemplate` に日付がサフィックスとして付いたものになる点に注目してください。

ターミナルに ```Running...``` と表示されるはずです。

::: zone-end

::: zone pivot="powershell"

このテンプレートを Azure にデプロイするには、Visual Studio Code のターミナルから Azure アカウントにサインインする必要があります。Visual Studio Code の拡張機能から Azure PowerShell Tools がインストールされていることを確認してください。

1. コマンド バーで **[ターミナル] > [新しいターミナル]** を選択して、PowerShell ウィンドウを開きます。

1. ターミナル ウィンドウのコマンド バーに **PowerShell** と表示されていれば、作業に適したシェルが開いているので、次のセクションに進んでください。

      :::image type="content" source="../media/3-pwsh.png" alt-text="'pwsh' ターミナルが選択されている Visual Studio Code ターミナル ウィンドウのスクリーンショット。":::

    1. そうでない場合は、下向き矢印を選択し、ドロップダウン リストで PowerShell を選択します。その選択肢がない場合は、**[既定のプロファイルの選択]** を選択します。

    1. 入力フィールドで下にスクロールし、**[PowerShell]** を選択します。

          :::image type="content" source="../media/3-select-shell-powershell.png" alt-text="シェル選択のドロップダウンが表示されている Visual Studio Code ターミナル ウィンドウのスクリーンショット。":::

1. ARM テンプレート ファイルが保存されているフォルダーにディレクトリを移動します。

### Azure PowerShell を使用して Azure にサインインする

Visual Studio Code のターミナルから次のコマンドを実行して、Azure にサインインします。ブラウザーが開くので、自分のアカウントにサインインできます。

  ```azurepowershell
  Connect-AzAccount
  ```

開いたブラウザー ウィンドウ (現在のウィンドウの背後に開くことがあります。その場合は現在のウィンドウを最小化して確認してください) で、自分のアカウントにサインインします。サインインすると、このアカウントに関連付けられているサブスクリプションの一覧がターミナルに表示されます。既定のサブスクリプションにはアスタリスク (*) が付いています。複数のサブスクリプションがある場合は、この演習で使用するサブスクリプションを選択してください。

### テンプレートを Azure にデプロイする

```azurepowershell
New-AzResourceGroup -Name <ResourceGroupName> -Location <Location>
```

リソース グループの一意の名前に置き換えます。また、最寄りの Azure リージョンに置き換えます。たとえば、米国東部の場合は eastus を使用します。

既定のリソース グループを設定しておくと、この演習の Azure CLI コマンドからそのパラメーターを省略できます。リソース グループを設定するには、次のコマンドを実行します。

```azurepowershell
Set-AzDefault -ResourceGroupName <ResourceGroupName>
```

*\<ResourceGroupName>* は、自分のリソース グループ名に置き換えてください。

次のコマンドを実行して、テンプレートを Azure にデプロイします。この ARM テンプレートにはまだリソースが含まれていないため、リソースは作成されません。

```azurepowershell
$templateFile="azuredeploy.json"
$today=Get-Date -Format "MM-dd-yyyy"
$deploymentName="blanktemplate-"+"$today"
New-AzResourceGroupDeployment `
  -Name $deploymentName `
  -TemplateFile $templateFile
```

上記コードの前半では、デプロイ ファイルへのパスとデプロイ名を含む Azure PowerShell の変数を設定しています。その後、```New-AzResourceGroupDeployment``` コマンドでテンプレートを Azure にデプロイします。デプロイ名は `blanktemplate` に日付がサフィックスとして付いたものになる点に注目してください。

::: zone-end

ARM テンプレートを Azure にデプロイしたら、[Azure portal](https://portal.azure.com?azure-portal=true) にアクセスします。

1. リソース メニューで **[リソース グループ]** を選択します。

1. この演習で作成したリソース グループを選択します。

1. **[概要]** ペインに、1 件のデプロイが成功したことが表示されます。

    :::image type="content" source="../media/3-deployment-succeeded.png" alt-text="デプロイ セクションに 1 件の成功が表示されている、リソース グループの概要の Azure portal インターフェイス。":::

1. **[1 成功]** を選択して、デプロイの詳細を表示します。

    :::image type="content" source="../media/3-blanktemplate.png" alt-text="1 件のデプロイが成功ステータスで一覧表示されている、デプロイの Azure portal インターフェイス。":::

1. `blanktemplate` を選択して、どのようなリソースがデプロイされたかを確認します。今回は、テンプレートにまだリソースを指定していないため、空になっています。

    :::image type="content" source="../media/3-no-results.png" alt-text="リソースが一覧に表示されていない、特定のデプロイの Azure portal インターフェイス。":::

1. 後でデプロイを再度確認できるように、このページをブラウザーで開いたままにしておきます。

## ARM テンプレートにリソースを追加する

前のタスクでは、空のテンプレートを作成してデプロイする方法を学習しました。次は、実際のリソースをデプロイします。このタスクでは、ARM テンプレートに Azure ストレージ アカウント リソースを追加します。

1. Visual Studio Code で *azuredeploy.json* ファイルを次のように更新します。

    [!code-json[](code/parameter1.json)]

1. リソースの *name* と *displayName* の値を一意のものに変更します (例: **learnexercise12321**)。この名前は Azure 全体でグローバルに一意である必要があり、3 〜 24 文字で、小文字、数字、ハイフンのみを使用できます。

1. リソースの場所は、リソースがデプロイされるリソース グループと同じ場所に設定されています。ここでは既定のままにします。

1. ファイルを保存します。

### 更新した ARM テンプレートをデプロイする

ここでは、このデプロイの内容をより適切に表すように、デプロイの名前を変更します。

::: zone pivot="cli"

ターミナルで次の Azure CLI コマンドを実行します。このスニペットは以前使用したものと同じコードですが、デプロイの名前が変更されています。

```azurecli
templateFile="azuredeploy.json"
today=$(date +"%d-%b-%Y")
DeploymentName="addstorage-"$today

az deployment group create \
  --name $DeploymentName \
  --template-file $templateFile
```

::: zone-end

::: zone pivot="powershell"

ターミナルで次の Azure PowerShell コマンドを実行します。このスニペットは以前使用したものと同じコードですが、デプロイの名前が変更されています。

```azurepowershell
$templateFile="azuredeploy.json"
$today=Get-Date -Format "MM-dd-yyyy"
$deploymentName="addstorage-"+"$today"
New-AzResourceGroupDeployment `
  -Name $deploymentName `
  -TemplateFile $templateFile
```

::: zone-end

### デプロイを確認する

1. デプロイが完了したら、ブラウザーで Azure portal に戻ります。リソース グループに移動すると、**[2 成功]** と表示されています。このリンクを選択します。

    2 件のデプロイが両方とも一覧に表示されていることに注目してください。

    :::image type="content" source="../media/3-addstorage-deployment.png" alt-text="2 件のデプロイが成功ステータスで一覧表示されている、デプロイの Azure portal インターフェイスのスクリーンショット。":::

1. **addstorage** を選択します。

    :::image type="content" source="../media/3-show-resource-deployed.png" alt-text="1 件のリソースが一覧表示されている、特定のデプロイの Azure portal インターフェイスのスクリーンショット。" :::

ストレージ アカウントがデプロイされていることを確認してください。
