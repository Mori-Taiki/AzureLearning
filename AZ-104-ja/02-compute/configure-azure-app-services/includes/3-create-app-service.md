Azure App Service の Web Apps、Mobile Apps、API Apps の機能を使って、Azure portal で独自のアプリを作成できます。

### 構成設定について知っておくべきこと

App Service でアプリを作成するのに必要な基本的な構成設定を見ていきましょう。

- **名前**: アプリの名前は一意である必要があります。名前は、Azure でアプリを識別し、その場所を特定するために使われます。名前の例は `webappces1.azurewebsites.net` です。代わりにカスタム ドメイン名をマップすることもできます。

- **公開**: App Service は、アプリをコードとして、または Docker コンテナーとしてホスト (公開) します。

- **ランタイム スタック**: App Service は、言語や SDK のバージョンを含むソフトウェア スタックを使ってアプリを実行します。Linux アプリとカスタム コンテナー アプリでは、任意で起動コマンドまたは起動ファイルを設定できます。スタックの選択肢には、.NET Core、.NET Framework、Node.js、PHP、Python があります。各製品のさまざまなバージョンが Linux と Windows で利用できます。

- **オペレーティング システム**: アプリのランタイム スタックのオペレーティング システムは、Linux または Windows を選べます。

- **リージョン**: アプリに選んだリージョンによって、利用できる App Service プランが変わります。

- **価格プラン**: 利用可能なリソース、機能、容量を確定するために、アプリを Azure App Service プランに関連付ける必要があります。選択したリージョンで利用できる価格レベルから選べます。

#### 作成後の設定

アプリの作成後、Azure portal では、アプリのデプロイ オプションやパス マッピングなど、その他の **[構成]** 設定が利用できるようになります。

:::image type="content" source="../media/web-app-configuration-27facdc5.png" alt-text="Azure portal で App Service のアプリのその他の構成オプションを示すスクリーンショット。":::

追加の構成設定の中には、開発者のコードに含められるものもあれば、アプリ側で構成できるものもあります。追加のアプリケーション設定の一部を紹介します。

- **Always On**: トラフィックがないときでもアプリを読み込んだままにできます。この設定は、継続的な WebJobs や、CRON 式でトリガーされる WebJobs には必須です。

- **セッション アフィニティ**: 複数インスタンスのデプロイで、アプリのクライアントがセッションの間ずっと同じインスタンスにルーティングされるようにできます。

- **HTTPS のみ**: 有効にすると、すべての HTTP トラフィックが HTTPS にリダイレクトされます。


> [!TIP]
> 「[演習 - Azure portal で Web アプリを作成する](/training/modules/host-a-web-app-with-azure-app-service/3-exercise-create-a-web-app-in-the-azure-portal?pivots=csharp)」で、自分で練習してみることをお勧めします。この演習にはサンドボックスが用意されています。
