前のユニットでは、Azure Resource Manager (ARM) テンプレートを作成し、そこに Azure ストレージ アカウントを追加しました。ここで、テンプレートに問題があることに気付くかもしれません。ストレージ アカウント名がハードコーディングされているのです。このテンプレートでは、毎回同じストレージ アカウントしかデプロイできません。別の名前でストレージ アカウントをデプロイするには、新しいテンプレートを作成する必要があり、これはデプロイを自動化する方法としては実用的ではありません。ストレージ アカウントの SKU もハードコーディングされているため、環境ごとにストレージ アカウントの種類を変えることもできません。今回のシナリオでは、デプロイごとに異なる種類のストレージ アカウントが必要になる可能性があったことを思い出してください。ストレージ アカウント SKU のパラメーターを追加することで、テンプレートの再利用性を高めることができます。

このユニットでは、テンプレートの *parameters* セクションと *outputs* セクションについて学習します。

## ARM テンプレートのパラメーター

ARM テンプレートのパラメーターを使用すると、特定の環境に合わせた値を指定して、デプロイをカスタマイズできます。たとえば、開発、テスト、運用など、デプロイ先の環境に応じて異なる値を渡します。たとえば、前のテンプレートでは *Standard_LRS* ストレージ アカウント SKU を使用していました。ストレージ アカウント SKU の名前をパラメーターにすることで、ストレージ アカウントを作成する他のデプロイでもこのテンプレートを再利用できます。テンプレートのデプロイ時に、そのデプロイで使用したい SKU の名前を渡します。この手順は、コマンドラインまたはパラメーター ファイルのどちらでも行えます。

テンプレートの `parameters` セクションでは、リソースのデプロイ時に入力できる値を指定します。1 つのテンプレートで使用できるパラメーターは 256 個までです。パラメーターの定義では、ほとんどのテンプレート関数を使用できます。

パラメーターで使用できるプロパティは次のとおりです。

```json
"parameters": {
  "<parameter-name>": {
    "type": "<type-of-parameter-value>",
    "defaultValue": "<default-value-of-parameter>",
    "allowedValues": [
      "<array-of-allowed-values>"
    ],
    "minValue": <minimum-value-for-int>,
    "maxValue": <maximum-value-for-int>,
    "minLength": <minimum-length-for-string-or-array>,
    "maxLength": <maximum-length-for-string-or-array-parameters>,
    "metadata": {
      "description": "<description-of-the-parameter>"
    }
  }
}
```

使用できるパラメーターの型は次のとおりです。

- string
- secureString
- integers
- boolean
- object
- secureObject
- array

### パラメーター使用の推奨事項

SKU、サイズ、容量など、環境によって異なる設定にはパラメーターを使用します。また、識別しやすくするため、あるいは社内の名前付け規則に準拠するために自分で指定したいリソース名にもパラメーターを使用します。各パラメーターには説明を付け、可能な限り既定値を使用してください。

セキュリティ上の理由から、ユーザー名やパスワードをテンプレートにハードコーディングしたり、既定値として指定したりしてはいけません。ユーザー名とパスワード (またはシークレット) には必ずパラメーターを使用します。すべてのパスワードとシークレットには *secureString* を使用します。機密データを JSON オブジェクトとして渡す場合は、*secureObject* 型を使用します。*secureString* 型または *secureObject* 型のテンプレート パラメーターは、リソースのデプロイ後に読み取ったり取得したりすることはできません。

### ARM テンプレートでパラメーターを使用する

ARM テンプレートの parameters セクションでは、リソースのデプロイ時に入力できるパラメーターを指定します。1 つのテンプレートで使用できるパラメーターは 256 個までです。

テンプレートの `parameters` セクションでストレージ アカウント SKU のパラメーターを定義したテンプレート ファイルの例を次に示します。実行時に値が指定されなかった場合に使用される既定値をパラメーターに指定できます。

```json
"parameters": {
  "storageAccountType": {
    "type": "string",
    "defaultValue": "Standard_LRS",
    "allowedValues": [
      "Standard_LRS",
      "Standard_GRS",
      "Standard_ZRS",
      "Premium_LRS"
    ],
    "metadata": {
      "description": "Storage Account type"
    }
  }
}
```

次に、リソース定義でパラメーターを使用します。構文は ```[parameters('name of the parameter')]``` です。デプロイ時には ```parameters``` 関数を使用します。関数については、次のモジュールで詳しく学習します。

```json
"resources": [
  {
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2025-01-01",
    "name": "learntemplatestorage123",
    "location": "[resourceGroup().location]",
    "sku": {
      "name": "[parameters('storageAccountType')]"
    },
    "kind": "StorageV2",
    "properties": {
      "supportsHttpsTrafficOnly": true
    }
  }
]
```

テンプレートのデプロイ時に、パラメーターの値を指定できます。次のコマンドの最後の行に注目してください。

# [Azure CLI](#tab/azure-cli)

```azurecli
templateFile="azuredeploy.json"
az deployment group create \
  --name testdeployment1 \
  --template-file $templateFile \
  --parameters storageAccountType=Standard_LRS
```

# [PowerShell](#tab/azure-powershell)

```azurepowershell
$templateFile="azuredeploy.json"
New-AzResourceGroupDeployment `
  -Name testdeployment1 `
  -TemplateFile $templateFile `
  -storageAccountType Standard_LRS
```

---

## ARM テンプレートの出力

ARM テンプレートの outputs セクションでは、デプロイが成功した後に返される値を指定できます。outputs セクションを構成する要素は次のとおりです。

```json
"outputs": {
  "<output-name>": {
    "condition": "<boolean-value-whether-to-output-value>",
    "type": "<type-of-output-value>",
    "value": "<output-value-expression>",
    "copy": {
      "count": <number-of-iterations>,
      "input": <values-for-the-variable>
    }
  }
}
```

| 要素 | 説明 |
|--- | --- |
| **output-name** | 有効な JavaScript 識別子である必要があります。 |
| **condition** | (省略可能) この出力値を返すかどうかを示すブール値。true の場合、その値はデプロイの出力に含まれます。false の場合、そのデプロイでは出力値がスキップされます。指定しない場合の既定値は true です。 |
| **type** | 出力値の型。 |
| **value** | (省略可能) 評価されて出力値として返されるテンプレート言語式。 |
| **copy** | (省略可能) 出力として複数の値を返す場合に copy を使用します。 |

### ARM テンプレートで出力を使用する

ストレージ アカウントのエンドポイントを出力する例を次に示します。

```json
"outputs": {
  "storageEndpoint": {
    "type": "object",
    "value": "[reference('learntemplatestorage123').primaryEndpoints]"
  }
}
```

式の ```reference``` の部分に注目してください。この関数は、ストレージ アカウントの実行時の状態を取得します。

## ARM テンプレートを再度デプロイする

ARM テンプレートは*べき等*であることを思い出してください。つまり、同じ環境にテンプレートを再度デプロイしても、テンプレートに変更がなければ、環境にも変更は生じません。テンプレートに変更を加えた場合 (たとえばパラメーター値を変更した場合) は、その変更だけがデプロイされます。テンプレートには Azure ソリューションに必要なすべてのリソースを含めることができ、テンプレートを安全に再実行できます。リソースは、まだ存在しない場合にのみ作成され、変更がある場合にのみ更新されます。
