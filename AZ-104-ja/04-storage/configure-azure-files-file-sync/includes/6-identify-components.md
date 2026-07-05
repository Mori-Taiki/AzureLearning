[Azure Storage Explorer](/azure/storage/storage-explorer/vs-azure-tools-storage-manage-with-storage-explorer?tabs=windows) は、Windows、macOS、Linux で Azure Storage のデータを簡単に扱えるスタンドアロン アプリケーションです。Azure Storage Explorer を使えば、複数のアカウントとサブスクリプションにアクセスして、すべての Storage コンテンツを管理できます。

:::image type="content" source="../media/storage-explorer.png" alt-text="フォルダーと複数のドキュメントを持つエミュレーターのストレージ アカウントが開かれている Azure Storage Explorer のスクリーンショット。アクセス層の情報が表示されています。" border="false":::

### Azure Storage Explorer について知っておくべきこと

Azure Storage Explorer には、次の特徴があります。

- Azure Storage Explorer でリソースへの完全なアクセスを行うには、管理 (Azure Resource Manager) とデータ層の両方のアクセス許可が必要です。ストレージ アカウント、アカウント内のコンテナー、コンテナー内のデータへのアクセスには、Microsoft Entra ID のアクセス許可が必要です。

- Azure Storage Explorer では、さまざまなストレージ アカウントに接続できます。
   - 自分の Azure サブスクリプションに関連付けられたストレージ アカウントに接続する。
   - 他の Azure サブスクリプションから共有されたストレージ アカウントとサービスに接続する。
   - Azure Storage エミュレーターを使って、ローカル ストレージに接続して管理する。

   :::image type="content" source="../media/connection-options-1df9c8f7.png" alt-text="Azure Storage Explorer の [アカウントの管理] ページのスクリーンショット。":::

### Azure Storage Explorer を使う際に考慮すべきこと

Azure Storage Explorer は、Azure のストレージ アカウントを扱う多くのシナリオをサポートします。これらの選択肢を確認しながら、自分の Azure Storage の実装にどのシナリオが当てはまるか考えてみてください。

| シナリオ | 説明 |
| --- | --- |
| **Azure サブスクリプションに接続する** | 自分の Azure サブスクリプションに属するストレージ リソースを管理します。 |
| **ローカルの開発用ストレージを扱う** | Azure Storage エミュレーターを使ってローカル ストレージを管理します。 |
| **外部ストレージにアタッチする** | ストレージ アカウント名、キー、エンドポイントを使って、別の Azure サブスクリプションに属するストレージ リソースや、各国の Azure クラウドの配下にあるストレージ リソースを管理します。このシナリオは次のセクションで詳しく説明します。 |
| **SAS でストレージ アカウントをアタッチする** | 共有アクセス署名 (SAS) を使って、別の Azure サブスクリプションに属するストレージ リソースを管理します。 |
| **SAS でサービスをアタッチする** | SAS を使って、別の Azure サブスクリプションに属する特定の Azure Storage サービス (BLOB コンテナー、キュー、テーブル) を管理します。 |

## 外部のストレージ アカウントにアタッチする

Azure Storage Explorer では、外部のストレージ アカウントにアタッチできるため、ストレージ アカウントを簡単に共有できます。

接続の作成には、外部ストレージの**アカウント名**と**アカウント キー**が必要です。Azure portal では、アカウント キーは **key1** と呼ばれます。

:::image type="content" source="../media/attach-name-key-13fe3ba3.png" alt-text="外部のストレージ アカウントに接続するための Azure Storage Explorer ウィザードのスクリーンショット。":::

各国の Azure クラウドのストレージ アカウント名とキーを使うには、**[ストレージ エンドポイントのドメイン]** のドロップダウン メニューで **[その他]** を選び、カスタムのストレージ アカウント エンドポイントのドメインを入力します。

### アクセス キー

アクセス キーは、ストレージ アカウント全体へのアクセスを提供します。アクセス キーは 2 つ提供されるため、一方のキーで接続を維持しながら、もう一方を再生成できます。

> [!Important]
> アクセス キーは安全に保管してください。アクセス キーは定期的に再生成することをお勧めします。

アクセス キーを再生成したら、このストレージ アカウントにアクセスするすべての Azure リソースとアプリケーションを新しいキーを使うように更新しなければなりません。この操作によって、仮想マシンからのディスクへのアクセスが中断されることはありません。
