Contoso Corporation の IT 管理者であるあなたは、オンコール対応として、管理タスクの実行や、組織の Azure サブスクリプション内のリソースで発生したワークロード障害の解決を頻繁に求められます。オンコール当番の週末に親戚の家を訪れていたところ、開発チームから Azure 仮想マシン (VM) に問題が発生したという連絡を受けました。その VM は、VM 上で動作するアプリケーションのアップグレードのための計画メンテナンス中に応答しなくなりました。開発者には、基盤となる Azure 仮想マシン ホスティング インフラストラクチャへのアクセス権が付与されていないため、VM が正常に動作しているときにしかリモート アクセスできません。そこで、問題の診断と修復のためにあなたが呼び出されました。

親戚の家を訪問中のため、管理用ワークステーションや診断スクリプトにはアクセスできません。手元にあるのは、インターネット ブラウザーを備えたラップトップだけです。このラップトップから Azure portal にアクセスし、組織の Azure サブスクリプションに対して認証を行い、Azure Cloud Shell を開いて Azure ファイル共有をマウントし、診断スクリプトにアクセスして VM の問題を診断・修復し、VM を稼働状態に戻します。

## Cloud Shell へのアクセス

Azure Cloud Shell にアクセスするには、いくつかの方法があります。

- 直接リンクから: <https://shell.azure.com>

  :::image type="content" source="../media/access-cloud-shell-directly.png" alt-text="リンクから直接アクセスした Cloud Shell のスクリーンショット。" lightbox="../media/access-cloud-shell-directly.png":::

- Azure portal から

  :::image type="content" source="../media/access-cloud-shell-from-azure-portal.png" alt-text="Azure portal からアクセスした Cloud Shell のスクリーンショット。" lightbox="../media/access-cloud-shell-from-azure-portal.png":::

- Microsoft Learn の閲覧中にコード スニペットから:

  :::image type="content" source="../media/access-cloud-shell-from-code-snippets.png" alt-text="コード スニペットからアクセスした Cloud Shell のスクリーンショット。" lightbox="../media/access-cloud-shell-from-code-snippets.png":::

Cloud Shell セッションを開くと、セッション用に一時的なホストが割り当てられます。この VM には、最新バージョンの PowerShell と Bash があらかじめ構成されています。使用したいコマンドライン エクスペリエンスを選択できます。

:::image type="content" source="../media/select-cli-experience.png" alt-text="Cloud Shell セッションでコマンドライン エクスペリエンスを選択する方法のスクリーンショット。" lightbox="../media/select-cli-experience.png":::

使用するシェル エクスペリエンスを選択したら、Azure リソースの管理を開始できます。

:::image type="content" source="../media/manage-azure-resources-in-cloud-shell.png" alt-text="Cloud Shell を使用して Azure リソースを管理する方法のスクリーンショット。" lightbox="../media/manage-azure-resources-in-cloud-shell.png":::

Cloud Shell セッションは、20 分間操作がないと終了します。セッションが終了しても、CloudDrive 上のファイルは保持されますが、Cloud Shell 環境にアクセスするには新しいセッションを開始する必要があります。

## 独自のスクリプトやファイルへのアクセス

Cloud Shell を使用する際、さまざまな操作のためにスクリプトを実行したりファイルを使用したりする必要が生じることがあります。Azure CloudDrive を使用すると、Cloud Shell 上にファイルを保持できます。

:::image type="content" source="../media/use-azure-cloud-drive.png" alt-text="Cloud Shell セッションで CloudDrive にアクセスする方法のスクリーンショット。" lightbox="../media/use-azure-cloud-drive.png":::

ファイルをアップロードした後は、通常の PowerShell や Bash のセッションと同じようにファイルを操作できます。

:::image type="content" source="../media/manage-files-in-cloud-drive.png" alt-text="CloudDrive でファイルを管理する方法のスクリーンショット。" lightbox="../media/manage-files-in-cloud-drive.png":::

ファイルが CloudDrive 上に保存されていれば、セッションを閉じて別のデバイスで新しいセッションを開いても、同じファイルにアクセスできます。Cloud Shell では、特定のリージョンに関連付けられた Azure Storage のファイル共有をマップすることもできます。Azure ファイル共有にアクセスできれば、その共有の内容を Cloud Shell から操作できます。

CloudDrive またはファイル共有上にあるスクリプトを編集する必要がある場合は、Cloud Shell エディターを使用できます。ブラウザー上で中かっこ {} のアイコンを選択して編集したいファイルを開くか、`code` コマンドにファイル名を指定して実行します。次に例を示します。

```bash
code temp.txt
```

:::image type="content" source="../media/cloud-shell-edit-scripts.png" alt-text="Cloud Shell のエディター モードにアクセスする方法のスクリーンショット。" lightbox="../media/cloud-shell-edit-scripts.png":::

> [!NOTE]
> `code` コマンドは、Cloud Shell のクラシック モードでのみ動作します。クラシック モードを有効にするには、**その他** アイコン (**...**) を選択し、**[設定]** > **[クラシック バージョンに移動]** を選択します。

## Cloud Shell のツール

Docker コンテナーや Kubernetes クラスターなどのリソースを管理する必要がある場合や、Ansible や Terraform などの Microsoft 以外のツールを Cloud Shell で使用したい場合も、Cloud Shell セッションにはこれらのアドオンがあらかじめ構成されています。

Cloud Shell セッション内で利用できるすべてのアドオンの一覧を次に示します。

| カテゴリ | 名前 |
|---|---|
| **Linux ツール** | bash<br>zsh<br>sh<br>tmux<br>dig |
| **Azure ツール** | [Azure CLI](/cli/azure/)<br>AzCopy<br>Azure Functions CLI<br>Service Fabric CLI<br>Batch Shipyard<br>blobxfer |
| **テキスト エディター** | code (Cloud Shell エディター)<br>vim<br>nano<br>emacs |
| **ソース管理** | git |
| **ビルド ツール** | make<br>maven<br>npm<br>pip |
| **コンテナー** | Docker Machine<br>Kubectl<br>Helm<br>DC/OS CLI |
| **データベース** | MySQL クライアント<br>PostgreSql クライアント<br>sqlcmd ユーティリティ<br>mssql-scripter |
| **その他** | iPython クライアント<br>Cloud Foundry CLI<br>Terraform<br>Ansible<br>Chef InSpec<br>Puppet Bolt<br>HashiCorp Packer<br>Office 365 CLI |
