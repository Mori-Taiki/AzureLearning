Azure portal は、Azure DevOps サービス、GitHub、Bitbucket、FTP、または開発マシン上のローカル Git リポジトリとの継続的インテグレーションとデプロイを、すぐに使える形で提供します。上記のいずれかのソースと Web アプリを接続すれば、あとは App Service が処理してくれます。App Service は、コードとその後の変更を自動的に Web アプリへ同期します。Azure DevOps サービスを使えば、独自のビルドとリリースのプロセスを定義することもできます。コードをコミットするたびに、ソース コードのコンパイル、テストの実行、リリースのビルドと Web アプリへのデプロイが行われます。これらの操作はすべて暗黙的に行われ、人手による管理は必要ありません。

:::image type="content" source="../media/continuous-development-a0dfd350.png" alt-text="2 人の開発者が 1 つの GitHub ソースを共有し、Azure App Service で構築された Web サイトを作成する様子を示す図。" border="false":::

### 継続的デプロイと手動デプロイについて知っておくべきこと

App Service で Web アプリを作成する際に、継続的デプロイまたは手動デプロイを選べます。これらの選択肢を確認しながら、自分の App Service アプリにはどのデプロイ方法を実装すべきか考えてみてください。これらのオプションはデプロイ センターにあります。

:::image type="content" source="../media/deployment-center.png" alt-text="デプロイ センターの設定オプションのスクリーンショット。" border="false":::

**継続的デプロイ (CI/CD)** は、エンド ユーザーへの影響を最小限に抑えながら、新機能やバグ修正を素早く繰り返しリリースするためのプロセスです。Azure は、複数のソースからの自動デプロイを直接サポートします。

   - **GitHub**: Azure は GitHub からの自動デプロイを直接サポートします。GitHub からの自動デプロイでは、2 つのビルド プロバイダーを利用できます。GitHub リポジトリを Azure に接続する際に、**[GitHub Actions](/azure/developer/github/github-actions)** (既定) と **[App Service ビルド サービス](/azure/app-service/deploy-continuous-deployment?tabs=others#enable-continuous-deployment)** のどちらかを選べます。

   - **Bitbucket**: GitHub と似ているため、Bitbucket でも自動デプロイを構成できます。

   - **ローカル Git**: App Service の Web Apps 機能は、リポジトリとして追加できるローカル URL を提供します。

   - **Azure Repos**: Azure Repos は、コードを管理するためのバージョン管理ツール群です。ソフトウェア プロジェクトの規模にかかわらず、できるだけ早い段階からバージョン管理を使うのが得策です。

**手動デプロイ**では、コードを手動で Azure にプッシュできます。

   - **リモート Git**: App Service の Web Apps 機能は、リモート リポジトリとして追加できる Git URL を提供します。このリモート リポジトリにプッシュすると、アプリがデプロイされます。
