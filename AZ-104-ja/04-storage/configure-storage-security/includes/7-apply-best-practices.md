[Storage insights](/azure/storage/common/storage-insights-overview?toc=%2Fazure%2Fstorage%2Fblobs%2Ftoc.json&bc=%2Fazure%2Fstorage%2Fblobs%2Fbreadcrumb%2Ftoc.json) は、Azure ストレージ アカウントの包括的な監視を提供します。Storage insights は、Azure Storage サービスのパフォーマンス、容量、可用性を一元的に確認できるビューを提供します。

:::image type="content" source="../media/storage-insights.png" alt-text="ポータルの Storage insights のスクリーンショット。" border="false":::

### Storage insights の利点は?

- **詳細なメトリックとログ**: Azure Storage insights は、ストレージの運用状況をより見えやすくする、詳細なメトリック、ログ、診断情報を提供します。遅延、スループット、容量使用率、トランザクションといった主要業績評価指標 (KPI) の監視に役立ちます。

- **セキュリティとコンプライアンスの強化**: Azure Storage insights を使うことで、セキュリティとコンプライアンスを強化できます。実行につながる洞察とアラートが提供され、セキュリティの問題を素早く特定して解決するのに役立ちます。

- **ロールベースのアクセス制御 (RBAC)**: Azure Storage insights は、ロールベースのアクセス制御 (RBAC)、Microsoft Entra ID、接続文字列、アクセス制御リスト (ACL) のアクセス許可といった Azure のセキュリティ機能と統合されています。RBAC により、データとリソースへの安全なアクセスが保証されます。

- **統一されたビュー**: Azure Storage サービスのパフォーマンス、容量、可用性を一元的に確認できるビューを提供します。これは、ストレージ アカウントのセキュリティと効率の維持に不可欠です。

### Storage insights を使うべき場面

- **リアルタイム監視**: Azure Storage insights はストレージ アカウントのリアルタイム監視を可能にし、利用傾向の追跡、パフォーマンスの監視、異常に対するアラートの設定ができます。

- **セキュリティ監査**: 包括的な監視と詳細なログを提供することで、セキュリティ監査を支援します。これらはコンプライアンスの確保とセキュリティ問題の特定に不可欠です。

- **正常性の分析と最適化**: このツールは、ストレージ アカウントの正常性の分析と最適化を支援し、セキュリティと最適なパフォーマンスを確保します。

### Microsoft Defender for Storage を使うべき場面

Storage insights が受動的な監視と履歴分析を提供するのに対し、Microsoft Defender for Storage は、アクティブなセキュリティ脅威に対する事前予防的な脅威検出を提供します。

**主な機能**

- **マルウェア スキャン**: BLOB のアップロードを自動的にスキャンして、マルウェアやウイルスを検出します。

-	**機微データの脅威検出**: 個人を特定できる情報 (PII) や資格情報が不適切に保存されている場合に検出します。

-	**アクティビティ ベースの脅威検出**: 異常なアクセス パターン、疑わしいダウンロード量、ハッシュ レピュテーション分析を監視します。

Microsoft Defender for Storage は、事後対応的な監視と履歴レポートではなく、能動的な脅威検出を提供することで、Storage insights を補完します。
