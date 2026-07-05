使い始めの段階では、VM などのリソースを作るのに Azure portal が一番簡単です。しかし、特に複数のリソースをまとめて作る必要がある場合、ポータルが最も効率的で速い方法とは限りません。今回のケースでは、最終的にさまざまなタスクをこなす数十台の VM を作ることになります。それを Azure portal で手作業で作るのは、楽しい作業とは言えないでしょう。

Azure でリソースを作成・管理する他の方法を見てみましょう。

- Azure Resource Manager テンプレート
- Azure PowerShell
- Azure CLI
- Azure REST API
- Azure クライアント SDK
- Azure VM 拡張機能
- Azure Automation サービス

## Resource Manager テンプレート

同じ設定の VM のコピーを作りたいとしましょう。VM イメージを作成して Azure にアップロードし、それを新しい VM の基にするという方法もありますが、この手順は非効率で時間がかかります。Azure には、VM の正確なコピーを作成するためのテンプレートを作る仕組みが用意されています。

**Resource Manager テンプレート**は、ソリューションのデプロイに必要なリソースを定義する JSON ファイルです。

VM のリソース テンプレートを作成できます。VM のメニューで、**[オートメーション]** の下にある **[テンプレートのエクスポート]** を選択します。

![VM の [テンプレートのエクスポート] オプションを示すスクリーンショット。](../media/4-automation-script.png)

> [!NOTE]
> この Learn モジュールのサンドボックスに含まれるリソースのポリシーにより、先ほど作成した VM はエクスポートできません。とはいえ、エクスポートされたテンプレートは編集しやすい JSON ファイルです。
テンプレートは、後で使うためにダウンロードや保存をすることも、テンプレートを基に新しい VM をすぐにデプロイすることもできます。たとえば、テスト環境でテンプレートから VM を作ってみたものの、オンプレミスのマシンの置き換えとしてはうまくいかないことが分かったとします。その場合、リソース グループを削除すればすべてのリソースが削除されるので、テンプレートを調整してやり直せます。デプロイ済みのリソースに変更を加えたいだけなら、作成に使ったテンプレートを変更して再デプロイします。Resource Manager が、新しいテンプレートに合うようにリソースを変更してくれます。

意図どおりに動くようになったら、そのテンプレートを使って、ステージングや運用など、インフラの複数のバージョンを簡単に複製できます。VM 名、ネットワーク名、ストレージ アカウント名などのフィールドをパラメーター化しておけば、異なるパラメーターでテンプレートを繰り返し読み込んで、環境ごとにカスタマイズできます。

テンプレートの使い方について詳しくは、「[クイックスタート: ARM テンプレートを使用して Ubuntu Linux 仮想マシンを作成する](/azure/virtual-machines/linux/quick-create-template)」を参照してください。


## Azure CLI

スクリプトやコマンドラインで Azure を操作するための選択肢のひとつが **Azure CLI** です。

Azure CLI は、仮想マシンやディスクなどの Azure リソースをコマンドラインから管理するための、Microsoft のクロスプラットフォーム コマンドライン ツールです。Linux、macOS、Windows で利用できるほか、Cloud Shell を使えばブラウザーでも利用できます。

たとえば CLI では、`az vm create` コマンドで Azure VM を作成できます。

```azurecli
az vm create \
    --resource-group TestResourceGroup \
    --name test-wp1-eus-vm \
    --image Ubuntu2204 \
    --admin-username azureuser \
    --generate-ssh-keys
```

Azure CLI は、Ruby や Python など、他のスクリプト言語と組み合わせて使うこともできます。

VM の作成と管理について詳しくは、**Manage virtual machines with the Azure CLI tool** モジュールで学べます。

Azure CLI を使った VM の作成について詳しくは、「[クイックスタート: CLI を使用して Linux 仮想マシンを作成する](/azure/virtual-machines/linux/quick-create-cli)」を参照してください。

## Azure PowerShell

**Azure PowerShell** は、単発の対話的なタスクや、繰り返し行うタスクの自動化に最適です。

> [!NOTE]
> PowerShell は、シェル ウィンドウやコマンド解析などの機能を提供するクロスプラットフォームのシェルです。Azure PowerShell は、Azure 固有のコマンド (**コマンドレット**と呼ばれます) を追加するオプションのアドオン パッケージです。Azure PowerShell のインストールと使い方については、別のトレーニング モジュールで詳しく学べます。

たとえば、`New-AzVM` コマンドレットを使うと、Debian ベースの Azure 仮想マシンを新規作成できます。

```powershell
New-AzVm `
    -ResourceGroupName "TestResourceGroup" `
    -Name "test-wp1-eus-vm" `
    -Location "East US" `
    -Image Debian11 `
    -VirtualNetworkName "test-wp1-eus-network" `
    -SubnetName "default" `
    -SecurityGroupName "test-wp1-eus-nsg" `
    -PublicIpAddressName "test-wp1-eus-pubip" `
    -GenerateSshKey `
    -SshKeyName myPSKey
    -OpenPorts 22
```

ここに示したように、数多くある VM の構成設定に対応するため、さまざまなパラメーターを指定します。ほとんどのパラメーターには妥当な既定値があるので、必須のパラメーターだけ指定すれば済みます。Azure PowerShell での VM の作成と管理について詳しくは、**Automate Azure tasks using scripts with PowerShell** モジュールで学べます。

PowerShell を使った VM の作成について詳しくは、「[クイックスタート: PowerShell を使用して Linux 仮想マシンを作成する](/azure/virtual-machines/linux/quick-create-powershell)」を参照してください。

## Terraform

Azure には Terraform プロバイダーもあるため、Terraform を使って VM を簡単に作成・管理できます。Terraform では、クラウド インフラの定義、プレビュー、デプロイが行えます。Terraform を使う場合、HCL 構文で構成ファイルを作成します。HCL 構文では、Azure などのクラウド プロバイダーと、クラウド インフラを構成する要素を指定できます。構成ファイルを作成したら、実行プランを作成し、デプロイ前にインフラの変更内容をプレビューできます。変更内容を確認したら、実行プランを適用してインフラをデプロイします。

詳しくは、[Azure Terraform プロバイダー](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)と「[クイックスタート: Terraform を使用して VM を作成する](/azure/virtual-machines/linux/quick-create-terraform)」を参照してください。
## プログラムによる操作 (API)

一般的に言えば、実行するのが単純なスクリプトで、コマンドライン ツールで完結させたいなら、Azure PowerShell も Azure CLI も良い選択肢です。しかし、VM の作成と管理が、複雑なロジックを持つ大きなアプリケーションの一部になるような、より複雑なシナリオでは、別のアプローチが必要です。

Azure のあらゆる種類のリソースは、プログラムから操作できます。

### Azure REST API

Azure REST API は、リソースごとに分類された操作を開発者に提供し、VM の作成と管理を可能にします。操作は URI として公開され、対応する HTTP メソッド (`GET`、`PUT`、`POST`、`DELETE`、`PATCH`) とレスポンスを持ちます。

Azure Compute API を使うと、仮想マシンとそれを支えるリソースにプログラムからアクセスできます。

詳しくは、[Virtual Machines REST API リファレンス](/rest/api/compute/virtual-machines)を参照してください。

### Azure クライアント SDK

REST API はプラットフォームにも言語にも依存しませんが、開発者はより高いレベルの抽象化を求めることが多いものです。Azure クライアント SDK は Azure REST API をカプセル化しており、開発者が Azure をずっと簡単に操作できるようにします。

Azure クライアント SDK は、C# などの .NET 系言語、Java、Node.js、PHP、Python、Ruby、Go といった、さまざまな言語とフレームワークで利用できます。

`Microsoft.Azure.Management.Fluent` NuGet パッケージを使って Azure VM を作成する C# コードのスニペット例を示します。

```csharp
var azure = Azure
    .Configure()
    .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
    .Authenticate(credentials)
    .WithDefaultSubscription();
// ...
var vmName = "test-wp1-eus-vm";

azure.VirtualMachines.Define(vmName)
    .WithRegion(Region.USEast)
    .WithExistingResourceGroup("TestResourceGroup")
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("jonc")
    .WithAdminPassword("aReallyGoodPasswordHere")
    .WithComputerName(vmName)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

同じ処理を **Azure Java SDK** を使って Java で書いたスニペットは次のとおりです。

```java
String vmName = "test-wp1-eus-vm";
// ...
VirtualMachine virtualMachine = azure.virtualMachines()
    .define(vmName)
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("TestResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("jonc")
    .withAdminPassword("aReallyGoodPasswordHere")
    .withComputerName(vmName)
    .withSize("Standard_DS1")
    .create();
```

## Azure VM 拡張機能

最初のデプロイの後に、仮想マシンに追加のソフトウェアをインストール・構成したいとしましょう。このタスクを特定の構成で、自動的に監視・実行させたいところです。

**Azure VM 拡張機能**は、初期デプロイ後の Azure VM でタスクの構成と自動化を行える小さなアプリケーションです。

詳しくは、「[Azure 仮想マシン拡張機能と機能](/azure/virtual-machines/extensions/overview)」を参照してください。
## Azure Automation サービス

時間の節約、ミスの削減、効率の向上は、リモートのインフラを管理するうえで最も大きな運用管理上の課題です。多数のインフラ サービスを抱えているなら、より高いレベルから運用できるように、Azure の上位サービスの利用を検討するとよいでしょう。

**Azure Automation** を使うと、頻繁で時間がかかり、ミスの起きやすい管理タスクを手軽に自動化するためのサービス群を統合できます。これらのサービスには、**プロセス オートメーション**、**構成管理**、**更新の管理**が含まれます。

- **プロセス オートメーション**: 特定のエラー イベントを監視している VM があるとしましょう。問題が報告されたらすぐに対処して修正したいはずです。プロセス オートメーションを使うと、データセンターで発生しうるイベントに対応できるウォッチャー タスクをセットアップできます。

- **構成管理**: VM で動作するオペレーティング システム向けに提供されるソフトウェア更新プログラムを追跡したい場合もあるでしょう。含めたい更新プログラムや除外したい更新プログラムがあるかもしれません。構成管理を使うと、これらの更新プログラムを追跡し、必要に応じて対処できます。会社の PC、サーバー、モバイル デバイスの管理には **Microsoft Endpoint Configuration Manager** を使います。Configuration Manager によるこの管理は、Azure VM にも広げられます。

- **更新の管理**: VM の更新プログラムとパッチの管理には、このサービスを使います。このサービスでは、利用可能な更新プログラムの状態の評価、インストールのスケジュール設定、デプロイ結果の確認による更新の適用検証が行えます。更新の管理には、プロセス管理と構成管理を提供するサービスが組み込まれています。VM の更新の管理は、**Azure Automation** アカウントから直接有効化できます。ポータルの仮想マシン ペインから、単一の仮想マシンに対して有効化することもできます。

## 自動シャットダウン

自動シャットダウンは、スケジュールに従って VM を自動的にシャットダウンできる Azure の機能です。自動シャットダウンを使えば、必要のないときに VM が動き続けないようにして、コストを節約できます。自動シャットダウンのスケジュールは毎日または毎週に設定でき、スケジュールのタイム ゾーンも指定できます。

Azure portal で VM の自動シャットダウン機能に移動するには、ポータルで VM のブレードを開き、[操作] セクションの [自動シャットダウン] をクリックして、好みに応じて自動シャットダウンの設定を構成します。

![VM の自動シャットダウン オプションを示すスクリーンショット。](../media/4-auto-shutdown-option.png)

詳しくは、「[自動シャットダウン](/azure/virtual-machines/auto-shutdown-vm)」を参照してください。

このように、Azure にはリソースの作成と管理のためのさまざまなツールが用意されており、管理作業を「自分に合った」プロセスに組み込めます。次は、インフラ リソースを円滑に稼働させ続けるための、その他の Azure サービスを見ていきましょう。
