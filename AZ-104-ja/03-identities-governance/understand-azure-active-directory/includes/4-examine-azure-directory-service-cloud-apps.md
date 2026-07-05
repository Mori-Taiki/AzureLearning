
Microsoft 365 や Intune などのクラウド サービスをデプロイするときには、これらのサービスの認証と認可を提供するディレクトリ サービスもクラウド上に必要です。そのため、認証を必要とする各クラウド サービスは、それぞれ独自の Microsoft Entra テナントを作成します。1 つの組織が複数のクラウド サービスを使う場合、サービスごとに別々のディレクトリを持つより、これらのクラウド サービスが単一のクラウド ディレクトリを使うほうがずっと便利です。

現在では、Microsoft 365、Azure、Microsoft Dynamics 365、Intune といった Microsoft のすべてのクラウドベース サービスをカバーする、1 つの ID サービスを持つことができます。Microsoft Entra ID は、他の ID プロバイダーやオンプレミスの AD DS を利用して、Azure 上のアプリケーションに対する集中型の認証と認可を開発者に提供します。Microsoft Entra ID は、Facebook、Google のサービス、Yahoo、Microsoft のクラウド サービスなどのアプリケーションを使う際に、ユーザーに SSO の体験を提供できます。

カスタム アプリケーションに Microsoft Entra ID のサポートを実装するプロセスはかなり複雑で、このコースの範囲を超えます。ただし、Azure portal と Microsoft Visual Studio 2013 以降を使えば、そのようなサポートの構成プロセスはより簡単になります。

特に、Azure App Service の Web Apps 機能に対する Microsoft Entra 認証は、Azure portal の [認証/認可] ブレードから直接有効化できます。Microsoft Entra テナントを指定することで、そのディレクトリにアカウントを持つユーザーだけが Web サイトにアクセスできるようにできます。デプロイ スロットごとに異なる認証設定を適用することも可能です。

詳しくは、「[Microsoft Entra ログインを使用するように App Service アプリを構成する](/azure/app-service/configure-authentication-provider-aad)」を参照してください。
