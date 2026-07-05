Azure Storage に保存するすべてのオブジェクトには、一意の URL アドレスがあります。ストレージ アカウント名は、URL アドレスの「サブドメイン」部分になります。このサブドメインと、サービスごとに固有のドメイン名の組み合わせが、ストレージ アカウントのエンドポイントを形成します。

例を見てみましょう。ストレージ アカウント名が *mystorageaccount* の場合、ストレージ アカウントの既定のエンドポイントは、次の表のように Azure の各サービスに対して形成されます。

| サービス | 既定のエンドポイント |
| --- | --- |
| **コンテナー サービス** | `//`**`mystorageaccount`**`.blob.core.windows.net` |
| **テーブル サービス** | `//`**`mystorageaccount`**`.table.core.windows.net` |
| **キュー サービス** | `//`**`mystorageaccount`**`.queue.core.windows.net` |
| **ファイル サービス** | `//`**`mystorageaccount`**`.file.core.windows.net` |

ストレージ アカウント内のオブジェクトにアクセスするための URL は、エンドポイントにオブジェクトの場所を付け足して作られます。

たとえば、ストレージ アカウントの *mycontainer* にある *myblob* データにアクセスするには、次の URL アドレスを使います。

`//`**`mystorageaccount`**`.blob.core.windows.net/`**`mycontainer`**`/`**`myblob`**.

## カスタム ドメインを構成する

Azure ストレージ アカウント内の BLOB データへのアクセスには、[カスタム ドメイン](/azure/storage/blobs/storage-custom-domain-name)を構成できます。確認したとおり、Azure Blob Storage の既定のエンドポイントは `\<storage-account-name>.blob.core.windows.net` です。`www.contoso.com` のようなカスタム ドメインとサブドメインを、ストレージ アカウントの BLOB または Web のエンドポイントにマップすれば、ユーザーはそのドメインを使ってストレージ アカウント内の BLOB データにアクセスできます。

**直接マッピング**では、サブドメインに対するカスタム ドメインを Azure ストレージ アカウントに対して有効にできます。この方法では、サブドメインから Azure ストレージ アカウントを指す `CNAME` レコードを作成します。

   次の例は、ドメイン ネーム システム (DNS) に `CNAME` レコードを作成して、サブドメインを Azure ストレージ アカウントにマップする方法を示しています。

   - サブドメイン: `blobs.contoso.com`
   - Azure ストレージ アカウント: `\<storage account>\.blob.core.windows.net`
   - 直接の `CNAME` レコード: `contosoblobs.blob.core.windows.net`
