このモジュールでは、Azure Blob Storage とその構成方法を学びました。Blob Storage が、クラウド向けの Microsoft のオブジェクト ストレージ ソリューションであることを確認しました。Azure Blob Storage は、テキストやバイナリ ファイルといった膨大な量の非構造化データの保存に最適化されていることも学びました。Blob Storage の機能と利用ケースを確認し、コストを削減してパフォーマンスを向上させる適切なアクセス層の選択を含めて、Blob Storage の構成方法を学びました。また、ライフサイクル管理戦略の作成と、フェールオーバーのためのオブジェクト レプリケーションの構成についても学びました。

**このモジュールの要点は次のとおりです。**
- Azure Blob Storage は、テキスト ドキュメント、画像、ビデオなど、非構造化データをクラウドに保存するための強力なソリューションです。
- Blob Storage には、データの利用パターンに基づいてパフォーマンスとコストを最適化するためのアクセス層 (ホット、クール、コールド、アーカイブ) があります。
- ライフサイクル管理ポリシーを構成すると、アクセス層間でのデータの自動移行や、データの有効期限の設定ができます。
- オブジェクト レプリケーションを使うと、異なるリージョンのコンテナー間で BLOB を非同期にコピーでき、冗長性の確保と読み取りリクエストの遅延削減が実現します。

## Copilot でさらに学ぶ

Copilot は、Azure インフラストラクチャ ソリューションの構成を支援してくれます。より詳しい情報が必要な製品やサービスについて、Copilot に比較、推奨、解説、調査を頼めます。Microsoft Edge ブラウザーを開いて右上の Copilot を選ぶか、copilot.microsoft.com にアクセスしてください。少し時間を取って次のプロンプトを試し、Copilot で学びを深めましょう。

- What are common administration tasks associated with Azure blob storage?

- How is Azure blob storage priced?

## Azure ドキュメントでさらに学ぶ

- [Azure Blob Storage のドキュメント](/azure/storage/blobs/) - Microsoft Azure の公式ドキュメントには、BLOB ストレージの構成と管理に関する包括的な情報があります。BLOB ストレージの構成のさまざまな側面を進めるのに役立つ、詳細なガイド、チュートリアル、例が見つかります。

- [Azure Blob Storage の概念](/azure/storage/blobs/storage-blobs-introduction) - ストレージ アカウント、コンテナー、BLOB など、Azure Blob Storage に関連する主要な概念の概要を示す記事です。これらのエンティティの作成と管理の方法を説明し、さまざまな構成オプションを扱います。

- [Azure Blob Storage のセキュリティ](/azure/storage/blobs/security-recommendations) - BLOB ストレージのセキュリティ面の理解は、適切な構成に不可欠です。この記事では、Azure Blob Storage で利用できる認証、認可、暗号化の選択肢を探ります。BLOB ストレージのリソースを保護するベスト プラクティスも扱います。

- [Azure Blob Storage のパフォーマンスとスケーラビリティ](/azure/storage/blobs/scalability-targets) - BLOB ストレージを構成する際のパフォーマンスの考慮事項を掘り下げる記事です。ストレージ アカウントの種類や、データ転送の最適化を扱います。

- [Azure Blob Storage のライフサイクル管理](/azure/storage/blobs/storage-lifecycle-management-concepts) - BLOB ストレージのライフサイクル管理を使うと、あらかじめ定義したルールに基づいてデータの移動と削除を自動化できます。この記事では、ストレージ コストを最適化しデータ管理を改善するための、ライフサイクル ポリシーの構成と管理の方法を説明します。
