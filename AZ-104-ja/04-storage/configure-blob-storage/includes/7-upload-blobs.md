BLOB は、あらゆる種類・サイズのデータ ファイルにできます。Azure Storage には、*ブロック BLOB*、*ページ BLOB*、*追加 BLOB* という 3 種類の BLOB があります。

### BLOB の種類について知っておくべきこと

BLOB の種類ごとの特徴を詳しく見てみましょう。

- **ブロック BLOB**: ブロック BLOB は、組み合わさって 1 つの BLOB を構成するデータのブロックからなります。Blob Storage のほとんどのシナリオではブロック BLOB を使います。ブロック BLOB は、ファイル、画像、ビデオなど、テキストやバイナリのデータをクラウドに保存するのに最適です。ブロック BLOB は、新しい BLOB の既定の種類です。新しい BLOB を作成する際に特定の種類を選ばなければ、ブロック BLOB として作成されます。

- **追加 BLOB**: 追加 BLOB もデータのブロックからなる点でブロック BLOB に似ています。追加 BLOB のデータ ブロックは、「追加 (append)」操作に最適化されています。追加 BLOB は、ログ記録が続くにつれてデータ量が増えていくログのシナリオに便利です。

- **ページ BLOB**: ページ BLOB は最大 8 TB のサイズにできます。ページ BLOB は、頻繁な読み書き操作をより効率的に行えます。Azure Virtual Machines は、オペレーティング システム ディスクとデータ ディスクにページ BLOB を使っています。

> [!NOTE]
> BLOB は、作成後に種類を変更できません。

### BLOB ストレージを管理する際に考慮すべきこと

BLOB のアップロードと管理にはポータルを使えます。この方法は、ファイルが少ない場合に適しています。アップロードするファイルを決めたら、BLOB の種類とブロック サイズ、コンテナーのフォルダーを選びます。アクセス層と暗号化スコープも設定します。

:::image type="content" source="../media/upload-blobs-7ad73d30.png" alt-text="認証の種類、BLOB の種類、ブロック サイズが表示されている [BLOB のアップロード] ページのスクリーンショット。":::

ファイル数が多い場合は、ツールを使うのが一番です。次の選択肢を確認し、どのツールが自分の構成ニーズに合うか考えてみてください。

- [**Azure Storage Explorer**](/azure/storage/storage-explorer/vs-azure-tools-storage-manage-with-storage-explorer)。BLOB、ファイル、キュー、テーブルに加え、Azure Data Lake Storage のエンティティやマネージド ディスクのアップロード、ダウンロード、管理が行えます。リソースの表示、編集、管理、データのプレビュー、ストレージのアクセス許可とアクセス制御の構成もできます。

:::image type="content" source="../media/blob-storage-explorer.png" alt-text="Storage Explorer のページのスクリーンショット。":::

- [**AzCopy**](/azure/storage/common/storage-use-azcopy-v10)。Windows と Linux で使える、扱いやすいコマンドライン ツールです。Blob Storage との間、コンテナー間、ストレージ アカウント間でデータをコピーできます。

- [**Azure Data Box Disk**](/azure/databox/data-box-disk-overview)。データセットが大きい、あるいはネットワークの制約があり、回線経由でのアップロードが現実的でない場合に、オンプレミスのデータを Blob Storage へ転送するためのサービスです。Azure Data Box Disk を使って Microsoft にソリッドステート ディスク (SSD) を依頼できます。ディスクにデータをコピーして Microsoft に送り返すと、Blob Storage にアップロードされます。
