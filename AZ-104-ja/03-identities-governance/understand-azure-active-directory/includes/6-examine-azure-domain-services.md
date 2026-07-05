

今日、ほとんどの組織では、基幹業務 (LOB) アプリケーションがドメイン メンバーであるコンピューターやデバイスにデプロイされています。これらの組織は認証に AD DS ベースの資格情報を使い、グループ ポリシーで管理しています。これらのアプリを Azure で動かすことを検討する際、重要な課題のひとつが、アプリへの認証サービスをどう提供するかです。このニーズを満たすには、ローカル インフラと Azure IaaS の間にサイト間の仮想プライベート ネットワーク (VPN) を実装するか、ローカルの AD DS のレプリカ ドメイン コントローラーを Azure の仮想マシン (VM) としてデプロイするかを選べます。これらのアプローチには、追加のコストと管理の手間がかかることがあります。また、この 2 つのアプローチの違いとして、前者では認証トラフィックが VPN を通過するのに対し、後者ではレプリケーション トラフィックが VPN を通過し、認証トラフィックはクラウド内にとどまります。

Microsoft は、これらのアプローチの代替として Microsoft Entra Domain Services を提供しています。Microsoft Entra ID P1 または P2 レベルの一部として動作するこのサービスは、グループ ポリシー管理、ドメイン参加、Kerberos 認証といったドメイン サービスを Microsoft Entra テナントに提供します。これらのサービスはローカルにデプロイされた AD DS と完全な互換性があるため、クラウドに追加のドメイン コントローラーをデプロイ・管理することなく利用できます。

:::image type="content" source="../media/azure-active-directory-virtual-network-340081c4.png" alt-text="Microsoft Entra Domain Services の概要を示す図。":::


Microsoft Entra ID はローカルの AD DS と統合できるため、Microsoft Entra Connect を実装すると、ユーザーはオンプレミスの AD DS と Microsoft Entra Domain Services の両方で組織の資格情報を利用できます。ローカルに AD DS をデプロイしていない場合でも、Microsoft Entra Domain Services をクラウド専用サービスとして使うことを選べます。これにより、オンプレミスにもクラウドにもドメイン コントローラーを 1 台もデプロイすることなく、ローカルにデプロイされた AD DS と同様の機能を持てます。たとえば、組織は Microsoft Entra テナントを作成して Microsoft Entra Domain Services を有効にし、オンプレミスのリソースと Microsoft Entra テナントの間に仮想ネットワークをデプロイできます。この仮想ネットワークに対して Microsoft Entra Domain Services を有効にすれば、オンプレミスのすべてのユーザーとサービスが Microsoft Entra ID のドメイン サービスを利用できます。

Microsoft Entra Domain Services は、組織に次のような利点をもたらします。

 -  管理者がドメイン コントローラーの管理、更新、監視を行う必要がありません。
 -  管理者が Active Directory のレプリケーションをデプロイ・管理する必要がありません。
 -  Microsoft Entra ID が管理するドメインには、Domain Admins や Enterprise Admins のグループを持つ必要がありません。

Microsoft Entra Domain Services の実装を選ぶ場合は、このサービスの現在の制限を把握しておく必要があります。制限には次のものがあります。

 -  基本のコンピューター Active Directory オブジェクトのみがサポートされます。
 -  Microsoft Entra Domain Services のドメインのスキーマは拡張できません。
 -  組織単位 (OU) の構造はフラットで、入れ子の OU は現在サポートされていません。
 -  組み込みのグループ ポリシー オブジェクト (GPO) があり、コンピューター アカウントとユーザー アカウント用に存在します。
 -  組み込みの GPO を OU に対して適用することはできません。また、Windows Management Instrumentation フィルターやセキュリティ グループのフィルター処理も使えません。

Microsoft Entra Domain Services を使えば、LDAP、NTLM、Kerberos の各プロトコルを使うアプリケーションを、オンプレミスのインフラからクラウドへ自由に移行できます。また、クラウドにドメイン コントローラーを置いたりローカル インフラへの VPN を用意したりしなくても、Microsoft SQL Server や Microsoft SharePoint Server などのアプリケーションを VM 上で使ったり、Azure IaaS にデプロイしたりできます。

Microsoft Entra Domain Services は Azure portal で有効化できます。このサービスは、ディレクトリのサイズに基づいて時間単位で課金されます。
