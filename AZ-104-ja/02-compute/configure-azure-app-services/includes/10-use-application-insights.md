[Azure Application Insights](/azure/azure-monitor/app/app-insights-overview) は、稼働中のアプリケーションを監視できる Azure Monitor の機能です。Application Insights を App Service の構成に統合すると、アプリのパフォーマンスの異常を自動的に検出できます。

Application Insights は、アプリのパフォーマンスとユーザビリティを継続的に改善していけるように設計されています。問題の診断や、ユーザーがアプリで実際に何をしているのかの把握に役立つ、強力な分析ツールを備えています。

:::image type="content" source="../media/app-insights-16629887.png" alt-text="Azure Application Insights が Web ページ、クライアント アプリ、Web サービスから情報を受け取り、それがアラート、Power BI、Visual Studio に転送される様子を示す図。" border="false":::

### Application Insights について知っておくべきこと

Azure Monitor の Application Insights の特徴を確認しましょう。

- Application Insights は、.NET、Node.js、Java EE など、さまざまなプラットフォームで動作します。

- オンプレミス、ハイブリッド環境、任意のパブリック クラウドでホストされている構成にも使えます。

- Application Insights は Azure Pipelines のプロセスと統合でき、多くの開発ツールとの接続ポイントを持っています。

### Application Insights を使う際に考慮すべきこと

Application Insights は開発チームの支援に最適です。アプリのパフォーマンスや利用のされ方を開発者が理解するのに役立ちます。App Service の構成シナリオでは、次の項目の監視を検討してください。

- **リクエスト レート、応答時間、エラー率を考慮する**: どのページが、1 日のどの時間帯に人気で、ユーザーがどこにいるのかを把握できます。どのページのパフォーマンスが最も良いかも確認できます。リクエストが増えたときに応答時間とエラー率が上がるなら、リソース不足の問題があるのかもしれません。

- **依存関係のレート、応答時間、エラー率を考慮する**: Application Insights を使えば、外部サービスがアプリのパフォーマンスを低下させていないかを調べられます。

- **例外を考慮する**: 集計された統計を分析することも、特定のインスタンスを選んでスタック トレースや関連リクエストを掘り下げることもできます。サーバーとブラウザーの両方の例外が報告されます。

- **ページ ビューと読み込みパフォーマンスを考慮する**: ユーザーのブラウザーから報告されるページ ビュー数を収集し、読み込みパフォーマンスを分析できます。

- **ユーザー数とセッション数を考慮する**: Application Insights は、アプリに接続しているユーザー数とセッション数の追跡に役立ちます。

- **パフォーマンス カウンターを考慮する**: Windows または Linux のサーバー マシンから Application Insights のパフォーマンス カウンターを追加できます。CPU、メモリ、ネットワーク使用量などのパフォーマンスを監視できます。

- **ホストの診断を考慮する**: Docker や Azure の診断情報をアプリの Application Insights に統合できます。

- **診断トレース ログを考慮する**: アプリからのトレース ログを実装すると、トレース イベントとリクエストを関連付けて問題を診断するのに役立ちます。

- **カスタム イベントとメトリックを考慮する**: クライアントまたはサーバーのコードとして、独自のカスタム イベントとメトリックの追跡ロジックを書けます。販売した商品数や勝利したゲーム数など、ビジネス上のイベントを追跡できます。

> [!TIP]
> 「[*Application Insights を使用してソリューションをトラブルシューティングする*](/training/paths/az-204-instrument-solutions-support-monitoring-logging/)」トレーニング モジュールで学びを広げることをお勧めします。
