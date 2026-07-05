[Azure File Sync](/azure/storage/file-sync/file-sync-introduction) を使うと、複数の Azure Files 共有を、オンプレミスの Windows Server またはクラウドの仮想マシンにキャッシュできます。Azure File Sync を使えば、オンプレミスのファイル サーバーの柔軟性、パフォーマンス、互換性を保ちながら、組織のファイル共有を Azure Files に集約できます。

Azure File Sync は、オンプレミスの Windows Server と Azure ファイル共有の間でファイルを同期するために連携して動く、5 つの主要コンポーネントで構成されます。

:::image type="content" source="../media/file-sync-1d3fd2e7.png" alt-text="Azure File Sync を使って組織のファイル共有を Azure Files にキャッシュする方法を描いた図。" border="false":::

- **ストレージ同期サービス**は、ファイル同期の管理を担う主要な Azure リソースです。最大 100 個の同期グループをサポートでき、単一の Azure リージョン内で動作し、最大 99 台の登録済み Windows Server を扱えます。

- **同期グループ**は同期の構成を確立するもので、1 つのクラウド エンドポイント (Azure ファイル共有) と最大 50 個のサーバー エンドポイントを含みます。サーバー エンドポイントは登録済み Windows Server 上の特定の NTFS パスですが、システム ボリューム上には置けず、その場合クラウド階層化もサポートされません。

- **クラウド エンドポイント**は、同期グループに参加する Azure ファイル共有です。同期グループごとに許可されるクラウド エンドポイントは 1 つだけです。

- **サーバー エンドポイント**は、クラウド エンドポイントと同期する、登録済み Windows Server 上のパスです。サーバー エンドポイントは NTFS でフォーマットされたボリュームである必要があり、システム ボリュームにはできません。

- **Azure File Sync エージェント**は、各 Windows Server にインストールします。エージェントは、同期操作と管理タスクのためのバックグラウンドの Windows サービスです。


### Azure File Sync について知っておくべきこと

Azure File Sync の特徴を見てみましょう。

- Azure File Sync は、Windows Server を Azure Files 共有の高速なキャッシュに変えます。

- Azure File Sync では、SMB、NFS、FTPS など、Windows Server で利用できる任意のプロトコルを使ってデータにローカルでアクセスできます。

- Azure File Sync は、世界中で必要なだけの数のキャッシュをサポートします。

- ストレージ同期サービスごとの同期グループは最大 100 個、同期グループごとのサーバー エンドポイントは最大 50 個です。

### Azure File Sync を使う際に考慮すべきこと

Azure File Sync には多くの利点があります。次のシナリオを検討し、自分の Azure Files 共有で Azure File Sync をどう活用できるか考えてみてください。

- **アプリケーションのリフト アンド シフトを考慮する**: Azure とオンプレミスのシステムの間でのアクセスを必要とするアプリケーションの移行に Azure File Sync を使えます。Windows Server と Azure Files をまたいで、同じデータへの書き込みアクセスを提供できます。

- **支社のサポートを考慮する**: ファイルのバックアップが必要な支社を Azure File Sync で支援できます。このサービスを使って、Azure ストレージに接続する新しいサーバーをセットアップできます。

- **バックアップと災害復旧を考慮する**: Azure File Sync を実装すると、Azure Backup がオンプレミスのデータをバックアップします。ファイルのメタデータを即座に復元し、必要に応じてデータを呼び戻すことで、迅速な災害復旧が可能です。

- **クラウド階層化によるファイルのアーカイブを考慮する**: Azure File Sync は、最近アクセスされたデータだけをローカル サーバーに保持します。クラウド階層化を実装すれば、古いデータは Azure Files へ移動します。
