

Microsoft Entra ID を単純に AD DS のクラウド版と考えることもできますが、Microsoft Entra ID と AD DS には共通する特徴がある一方で、重要な違いもいくつかあります。

### AD DS の特徴

AD DS は、物理サーバーまたは仮想サーバー上での Windows Server ベースの Active Directory の従来型デプロイです。AD DS は主にディレクトリ サービスと見なされることが多いですが、実際には Windows Active Directory テクノロジ スイートの 1 コンポーネントにすぎません。このスイートには、Active Directory 証明書サービス (AD CS)、Active Directory ライトウェイト ディレクトリ サービス (AD LDS)、Active Directory フェデレーション サービス (AD FS)、Active Directory Rights Management サービス (AD RMS) も含まれます。

AD DS を Microsoft Entra ID と比較する際には、AD DS の次の特徴を押さえておくことが重要です。

 -  AD DS は、X.500 ベースの階層構造を持つ、本来の意味でのディレクトリ サービスです。
 -  AD DS は、ドメイン コントローラーなどのリソースの検索にドメイン ネーム システム (DNS) を使います。
 -  AD DS は、ライトウェイト ディレクトリ アクセス プロトコル (LDAP) の呼び出しでクエリと管理を行えます。
 -  AD DS は、認証に主に Kerberos プロトコルを使います。
 -  AD DS は、管理に OU と GPO を使います。
 -  AD DS には、Active Directory ドメインに参加したコンピューターを表すコンピューター オブジェクトがあります。
 -  AD DS は、委任された管理のためにドメイン間の信頼を使います。

オンプレミスの AD DS のスケーラビリティと可用性を高めるために、Azure 仮想マシン上に AD DS をデプロイすることもできます。ただし、Azure 仮想マシン上に AD DS をデプロイしても、Microsoft Entra ID を利用することにはなりません。

> [!NOTE]
> Azure 仮想マシンへの AD DS のデプロイには、1 つ以上の追加の Azure データ ディスクが必要です。AD DS のストレージに C ドライブを使うべきではないためです。これらのディスクは、AD DS データベース、ログ、sysvol フォルダーの保存に必要です。これらのディスクのホスト キャッシュ設定は [なし] にする必要があります。

<a name='characteristics-of-azure-ad'></a>

### Microsoft Entra ID の特徴

Microsoft Entra ID には AD DS と似ている点が多くありますが、違いも多くあります。Microsoft Entra を使うことは、Azure 仮想マシンに Active Directory ドメイン コントローラーをデプロイしてオンプレミスのドメインに追加することとは別物だと理解しておくことが重要です。

Microsoft Entra ID を AD DS と比較する際には、Microsoft Entra ID の次の特徴を押さえておくことが重要です。

 -  Microsoft Entra ID は主に ID ソリューションであり、HTTP (ポート 80) と HTTPS (ポート 443) の通信を使う、インターネット ベースのアプリケーション向けに設計されています。
 -  Microsoft Entra ID は、マルチテナントのディレクトリ サービスです。
 -  Microsoft Entra のユーザーとグループはフラットな構造で作成され、OU や GPO はありません。
 -  Microsoft Entra ID に LDAP でクエリすることはできません。代わりに、HTTP および HTTPS 上の REST API を使います。
 -  Microsoft Entra ID は Kerberos 認証を使いません。代わりに、SAML、WS-Federation、OpenID Connect といった HTTP・HTTPS のプロトコルを認証に使い、認可には OAuth を使います。
 -  Microsoft Entra ID にはフェデレーション サービスが含まれており、Facebook など多くのサードパーティ サービスが Microsoft Entra ID とフェデレーションし、これを信頼しています。
