この演習では、デプロイ時に Azure ストレージ アカウント名を定義するパラメーターを追加します。次に、許可するストレージ アカウント SKU を定義するパラメーターを追加し、このデプロイで使用する SKU を指定します。また、デプロイ プロセスの後段で利用できる出力を追加して、Azure Resource Manager テンプレート (ARM テンプレート) の利便性を高めます。

## ARM テンプレートのパラメーターを作成する

ここでは、実行時に設定できるパラメーターを追加して、ARM テンプレートをより柔軟にします。```storageName``` の値のパラメーターを作成します。

1. Visual Studio Code の *azuredeploy.json* ファイルで、```"parameters":{},``` を次のように更新します。

    ```json
    "parameters": {
      "storageName": {
        "type": "string",
        "minLength": 3,
        "maxLength": 24,
        "metadata": {
          "description": "The name of the Azure storage resource"
        }
      }
    },
    ```

    JSON ファイルを正しくフォーマットするには、<kbd>Alt+Shift+F</kbd> キーを押します。

1. ```resources``` ブロック内の ```name``` と ```displayName``` の両方の値で、この新しいパラメーターを使用します。ファイル全体は、次のコード例のようになります。

   [!code-json[](code/parameter2.json?highlight=5-12,20,22)]

1. ファイルを保存します。

### パラメーター化した ARM テンプレートをデプロイする

ここでは、このデプロイの内容をより適切に表すようにデプロイ名を変更し、新しいパラメーターの値を入力します。

::: zone pivot="cli"

ターミナルで次の Azure CLI コマンドを実行します。このスクリプトは以前使用したものと同じですが、デプロイ名が変更されています。```storageName``` パラメーターには一意の値を入力してください。この名前は Azure 全体でグローバルに一意である必要があり、3 〜 24 文字で、小文字、数字、ハイフンのみを使用できます。前のユニットで作成した一意の名前を再利用してもかまいません。その場合、Azure は新しいリソースを作成する代わりに既存のリソースを更新します。

```azurecli
templateFile="azuredeploy.json"
today=$(date +"%d-%b-%Y")
DeploymentName="addnameparameter-"$today

az deployment group create \
  --name $DeploymentName \
  --template-file $templateFile \
  --parameters storageName={your-unique-name}
```

  ::: zone-end

  ::: zone pivot="powershell"

ターミナルで次の Azure PowerShell コマンドを実行します。このスクリプトは以前使用したものと同じですが、デプロイ名が変更されています。`storageName` パラメーターには一意の値を入力してください。この名前は Azure 全体でグローバルに一意である必要があり、3 〜 24 文字で、小文字、数字、ハイフンのみを使用できます。前のユニットで作成した一意の名前を再利用してもかまいません。その場合、Azure は新しいリソースを作成する代わりに既存のリソースを更新します。

```azurepowershell
$templateFile="azuredeploy.json"
$today=Get-Date -Format "MM-dd-yyyy"
$deploymentName="addnameparameter-"+"$today"
New-AzResourceGroupDeployment `
  -Name $deploymentName `
  -TemplateFile $templateFile `
  -storageName {your-unique-name}
```

::: zone-end

### デプロイを確認する

1. デプロイが完了したら、ブラウザーで Azure portal に戻ります。リソース グループに移動すると、**[3 成功]** と表示されています。このリンクを選択します。

    3 件のデプロイがすべて一覧に表示されていることに注目してください。

1. 前回と同じ手順で、*addnameparameter* デプロイの内容を確認します。

### 許可される値を制限するパラメーターを追加する

ここでは、パラメーターに指定できる値を制限します。

1. *azuredeploy.json* ファイルの ```parameters``` セクションに、```storageSKU``` という名前の新しいパラメーターを追加します。

    ```json
    // This is the allowed values for an Azure storage account
    "storageSKU": {
       "type": "string",
       "defaultValue": "Standard_LRS",
       "allowedValues": [
         "Standard_LRS",
         "Standard_GRS",
         "Standard_RAGRS",
         "Standard_ZRS",
         "Premium_LRS",
         "Premium_ZRS",
         "Standard_GZRS",
         "Standard_RAGZRS"
       ]
     }
    ```

    1 行目はコメントです。ARM テンプレートは ```//``` と ```/* */``` のコメントをサポートしています。

1. ```storageSKU``` パラメーターを使用するように **resources** を更新します。Visual Studio Code の IntelliSense を活用すると、この手順が簡単になります。

    ```json
    "sku": {
         "name": "[parameters('storageSKU')]"
       }
    ```

    ファイル全体は、次のコード例のようになります。

    [!code-json[](code/parameter3.json?highlight=13-26,41)]

1. ファイルを保存します。

### ARM テンプレートをデプロイする

ここでは、許可リストに含まれる ```storageSKU``` パラメーターを使用してデプロイを成功させます。その後、許可リストに含まれない ```storageSKU``` パラメーターを使用してテンプレートのデプロイを試みます。2 回目のデプロイは、想定どおり失敗します。

::: zone pivot="cli"

1. 次のコマンドを実行して、テンプレートをデプロイします。```storageName``` パラメーターには一意の名前を入力してください。この名前は Azure 全体でグローバルに一意である必要があり、3 〜 24 文字で、小文字、数字、ハイフンのみを使用できます。前のユニットで作成した一意の名前を再利用してもかまいません。その場合、Azure は新しいリソースを作成する代わりに既存のリソースを更新します。

    ```azurecli
    templateFile="azuredeploy.json"
    today=$(date +"%d-%b-%Y")
    DeploymentName="addSkuParameter-"$today

    az deployment group create \
      --name $DeploymentName \
      --template-file $templateFile \
      --parameters storageSKU=Standard_GRS storageName={your-unique-name}
    ```

      このデプロイが完了するまで待ちます。このデプロイは想定どおり成功します。許可される値の一覧により、テンプレートの利用者がリソースに対して機能しないパラメーター値を渡すことを防げます。次に、無効な SKU を指定するとどうなるかを見てみましょう。

1. 次のコマンドを実行して、許可されていないパラメーターでテンプレートをデプロイします。ここでは、```storageSKU``` パラメーターを **Basic** に変更しています。```storageName``` パラメーターには一意の名前を入力してください。この名前は Azure 全体でグローバルに一意である必要があり、3 〜 24 文字で、小文字、数字、ハイフンのみを使用できます。前のユニットで作成した一意の名前を再利用してもかまいません。その場合、Azure は新しいリソースを作成する代わりに既存のリソースを更新します。

    ```azurecli
    templateFile="azuredeploy.json"
    today=$(date +"%d-%b-%Y")
    DeploymentName="addSkuParameter-"$today

    az deployment group create \
      --name $DeploymentName \
      --template-file $templateFile \
      --parameters storageSKU=Basic storageName={your-unique-name}
    ```

    このデプロイは失敗します。エラーに注目してください。

    :::image type="content" source="../media/3-deploy-validation-failed.png" alt-text="デプロイの検証エラーが表示されているターミナル ウィンドウのスクリーンショット。" border="true":::

::: zone-end

::: zone pivot="powershell"

1. 次のコマンドを実行して、テンプレートをデプロイします。```storageName``` パラメーターには一意の名前を入力してください。この名前は Azure 全体でグローバルに一意である必要があり、3 〜 24 文字で、小文字、数字、ハイフンのみを使用できます。前のユニットで作成した一意の名前を再利用してもかまいません。その場合、Azure は新しいリソースを作成する代わりに既存のリソースを更新します。

    ```azurepowershell
    $today=Get-Date -Format "MM-dd-yyyy"
    $deploymentName="addSkuParameter-"+"$today"
    New-AzResourceGroupDeployment `
      -Name $deploymentName `
      -TemplateFile $templateFile `
      -storageName {your-unique-name} `
      -storageSKU Standard_GRS
    ```

      このデプロイが完了するまで待ちます。このデプロイは想定どおり成功します。許可される値の一覧により、テンプレートの利用者がリソースに対して機能しないパラメーター値を渡すことを防げます。次に、無効な SKU を指定するとどうなるかを見てみましょう。

1. 次のコマンドを実行して、許可されていないパラメーターでテンプレートをデプロイします。ここでは、```storageSKU``` パラメーターを **Basic** に変更しています。```storageName``` パラメーターには一意の名前を入力してください。この名前は Azure 全体でグローバルに一意である必要があり、3 〜 24 文字で、小文字、数字、ハイフンのみを使用できます。前のユニットで作成した一意の名前を再利用してもかまいません。その場合、Azure は新しいリソースを作成する代わりに既存のリソースを更新します。

    ```azurepowershell
    $today=Get-Date -Format "MM-dd-yyyy"
    $deploymentName="addSkuParameter-"+"$today"
    New-AzResourceGroupDeployment `
      -Name $deploymentName `
      -TemplateFile $templateFile `
      -storageName {your-unique-name} `
      -storageSKU Basic
    ```

    このデプロイは失敗します。エラーに注目してください。

    :::image type="content" source="../media/3-deploy-validation-failed.png" alt-text="デプロイの検証エラーが表示されているターミナル ウィンドウのスクリーンショット。" border="true":::

::: zone-end

## ARM テンプレートに出力を追加する

ここでは、ARM テンプレートの ```outputs``` セクションに、ストレージ アカウント リソースのエンドポイントを出力する記述を追加します。

1. Visual Studio Code の *azuredeploy.json* ファイルで、```"outputs":{},``` を次のように更新します。

    ```json
    "outputs": {
      "storageEndpoint": {
        "type": "object",
        "value": "[reference(parameters('storageName')).primaryEndpoints]"
      }
    }
    ```

1. ファイルを保存します。

### 出力を追加した ARM テンプレートをデプロイする

ここでは、テンプレートをデプロイし、エンドポイントが JSON として出力されることを確認します。```storageName``` パラメーターには一意の名前を入力する必要があります。この名前は Azure 全体でグローバルに一意である必要があり、3 〜 24 文字で、小文字、数字、ハイフンのみを使用できます。前のユニットで作成した一意の名前を再利用してもかまいません。その場合、Azure は新しいリソースを作成する代わりに既存のリソースを更新します。

::: zone pivot="cli"

1. 次のコマンドを実行して、テンプレートをデプロイします。*{your-unique-name}* は、自分専用の一意の文字列に必ず置き換えてください。

    ```azurecli
    templateFile="azuredeploy.json"
    today=$(date +"%d-%b-%Y")
    DeploymentName="addoutputs-"$today

    az deployment group create \
      --name $DeploymentName \
      --template-file $templateFile \
      --parameters storageSKU=Standard_LRS storageName={your-unique-name}
    ```

    出力に注目してください。

    :::image type="content" source="../media/3-add-output-result.png" alt-text="プライマリ エンドポイントが JSON として出力されているターミナル ウィンドウのスクリーンショット。" border="true":::

::: zone-end

::: zone pivot="powershell"

1. 次のコマンドを実行して、テンプレートをデプロイします。*{your-unique-name}* は、自分専用の一意の文字列に必ず置き換えてください。

    ```azurepowershell
    $today=Get-Date -Format "MM-dd-yyyy"
    $deploymentName="addOutputs-"+"$today"
    New-AzResourceGroupDeployment `
      -Name $deploymentName `
      -TemplateFile $templateFile `
      -storageName {your-unique-name} `
      -storageSKU Standard_LRS
    ```

    出力に注目してください。

    :::image type="content" source="../media/3-add-output-result.png" alt-text="プライマリ エンドポイントが JSON として出力されているターミナル ウィンドウのスクリーンショット。" border="true":::

::: zone-end

### 出力のデプロイを確認する

Azure portal で *addOutputs* デプロイに移動します。ここでも出力を確認できます。

  :::image type="content" source="../media/3-portal-outputs.png" alt-text="左側のメニューで出力が選択されている Azure portal のスクリーンショット。" border="true":::
