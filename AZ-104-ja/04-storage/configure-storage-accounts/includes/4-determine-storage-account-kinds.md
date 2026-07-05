汎用の Azure ストレージ アカウントには、Standard と Premium という 2 つの基本的な[種類](/azure/storage/common/storage-account-overview?toc=%2Fazure%2Fstorage%2Fblobs%2Ftoc.json#types-of-storage-accounts)があります。

> [!VIDEO https://learn-video.azurefd.net/vod/player?id=52c7296b-212e-4818-a8cb-9f1648d5dd7d]

### ストレージ アカウントの種類について知っておくべきこと

**Standard** ストレージ アカウントは、磁気ハード ディスク ドライブ (HDD) を基盤としています。Standard ストレージ アカウントは、GB あたりのコストが最も低くなります。大容量のストレージが必要なアプリケーションや、データへのアクセス頻度が低いアプリケーションに Standard ストレージを使えます。

**Premium** ストレージ アカウントは、ソリッドステート ドライブ (SSD) を基盤とし、一貫した低遅延のパフォーマンスを提供します。データベースなど I/O 集約型のアプリケーションを動かす Azure 仮想マシンのディスクに Premium ストレージを使えます。

> [!NOTE]
> Standard ストレージ アカウントを Premium に変換することも、その逆もできません。目的の種類の新しいストレージ アカウントを作成し、必要に応じてデータを新しいストレージ アカウントにコピーする必要があります。すべての種類のストレージ アカウントで、保存データはストレージ サービス暗号化 (SSE) により暗号化されます。


| ストレージ&nbsp;アカウント| サポートされるサービス| 冗長性の選択肢 | 推奨される用途 |
| --- | --- | ---| --- |
| [**Standard** __汎用 v2__](/azure/storage/common/storage-account-upgrade)| Blob Storage (Data Lake Storage を含む)、Queue Storage、Table Storage、Azure Files | LRS、GRS、RA-GRS、ZRS、GZRS、RA-GZRS | BLOB、ファイル共有、キュー、テーブル、ディスク (ページ BLOB) を含む、ほとんどのシナリオに対応する標準のストレージ アカウント。 |
| [**Premium** __ブロック BLOB__](/azure/storage/blobs/storage-blob-block-blob-premium)| Blob Storage (Data Lake Storage を含む) | LRS、ZRS | ブロック BLOB と追加 BLOB 用の Premium ストレージ アカウント。トランザクション レートの高いアプリケーションに推奨されます。小さめのオブジェクトを扱う場合や、一貫して低いストレージ遅延が必要な場合は、Premium ブロック BLOB を使ってください。このストレージは、アプリケーションに合わせてスケールするよう設計されています。 |
| [**Premium** __ファイル共有__](/azure/storage/files/storage-how-to-create-file-share)| Azure Files | LRS、ZRS | ファイル共有専用の Premium ストレージ アカウント。エンタープライズまたは高パフォーマンスのスケール アプリケーションに推奨されます。サーバー メッセージ ブロック (SMB) と NFS の両方のファイル共有のサポートが必要な場合は、Premium ファイル共有を使ってください。 |
| [**Premium** __ページ BLOB__](/azure/storage/blobs/storage-blob-pageblob-overview)| ページ BLOB のみ | LRS のみ | ページ BLOB 専用の Premium 高パフォーマンス ストレージ アカウント。ページ BLOB は、オペレーティング システム、仮想マシンのデータ ディスク、データベースなど、インデックス ベースで疎なデータ構造の保存に最適です。 |

> [!NOTE]
> 既存の Azure サブスクリプションを管理している管理者は、汎用 v1 (GPv1) や従来の BlobStorage アカウントといったレガシなストレージ アカウントの種類に出会うことがあります。Microsoft は、現在のすべての機能を利用できるように、レガシ アカウントを汎用 v2 にアップグレードすることを推奨しています。アップグレードは、Azure portal、Azure CLI、または PowerShell からその場で実行できます。

> [!TIP]
> 先に進む前に、「[*ストレージ アカウントを作成する*](/training/modules/create-azure-storage-account/)」トレーニング モジュールに取り組むことをお勧めします。
