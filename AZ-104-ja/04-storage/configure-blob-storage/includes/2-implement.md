[Azure Blob Storage](/azure/storage/blobs/storage-blobs-overview) は、非構造化データをオブジェクト (BLOB) としてクラウドに保存するサービスです。Blob は Binary Large Object の略です。Blob Storage は「オブジェクト ストレージ」や「コンテナー ストレージ」とも呼ばれます。

> [!VIDEO https://learn-video.azurefd.net/vod/player?id=bd4c1a69-d3d4-4914-a0a9-7d5b24aa57ba]

### Azure Blob Storage について知っておくべきこと

Blob Storage の構成上の特徴を見ていきましょう。

:::image type="content" source="../media/blob-storage-94fb52b8.png" alt-text="Azure Blob Storage のアーキテクチャを示す図。" border="false":::

- Blob Storage には、あらゆる種類のテキストまたはバイナリ データを保存できます。テキスト ドキュメント、画像、ビデオ ファイル、アプリケーションのインストーラーなどが例です。

- Blob Storage は、データの保存と管理に 3 つのリソースを使います。
   - Azure ストレージ アカウント
   - Azure ストレージ アカウント内のコンテナー
   - コンテナー内の BLOB

- Blob Storage を実装するには、いくつかの設定を構成します。
   - BLOB コンテナーのオプション。
   - BLOB の種類とアップロードのオプション。
   - Blob Storage のアクセス層。
   - BLOB のライフサイクル ルール。
   - BLOB のオブジェクト レプリケーションのオプション。

### Azure Blob Storage を実装する際に考慮すべきこと

Blob Storage には多くの一般的な用途があります。次のシナリオを検討しながら、自分のデータのニーズについて考えてみてください。

- **ブラウザーへの配信を考慮する**: Blob Storage を使って、画像やドキュメントをブラウザーに直接配信できます。

- **分散アクセスを考慮する**: Blob Storage は、インストール プロセス中など、分散アクセス用のファイルを保存できます。

- **ストリーミング データを考慮する**: Blob Storage を使って、ビデオとオーディオをストリーミングできます。

- **アーカイブと復旧を考慮する**: Blob Storage は、バックアップと復元、災害復旧、アーカイブのためのデータ保存に最適なソリューションです。

- **アプリケーションからのアクセスを考慮する**: オンプレミスまたは Azure でホストされるサービスによる分析用のデータを Blob Storage に保存できます。
