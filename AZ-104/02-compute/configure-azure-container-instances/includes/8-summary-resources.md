このモジュールでは、Azure Container Instances と Azure 仮想マシンをいつ使い分けるかを学びました。Azure Container Instances の機能と利用ケースを確認し、Azure コンテナー グループの実装方法を学びました。

このモジュールの要点は次のとおりです。

- コンテナーは軽量な分離を提供し、仮想マシンに比べて使用するシステム リソースが少なくて済みます。
- コンテナーは、Docker で個別にデプロイすることも、Azure Container Apps のようなオーケストレーターでデプロイすることもできます。
- コンテナーは、ストレージに Azure Disks または Azure Files を使います。
- コンテナー グループとは、同じホスト マシン上にスケジュールされるコンテナーの集まりです。
- ノードに障害が起きても、コンテナーは別のクラスター ノード上で速やかに再作成できます。

## Copilot でさらに学ぶ
Copilot は、Azure インフラストラクチャ ソリューションの構成を支援してくれます。より詳しい情報が必要な製品やサービスについて、Copilot に比較、推奨、解説、調査を頼めます。Microsoft Edge ブラウザーを開いて右上の Copilot を選ぶか、copilot.microsoft.com にアクセスしてください。少し時間を取って次のプロンプトを試し、Copilot で学びを深めましょう。

- Compare benefits and usage cases for containers and virtual machines.

- What are the best practices for configuring Azure Container Instances for task-based workloads? Explain the restart policies.

- How do I deploy a multi-container group in Azure Container Instances using Bicep? Show an example with environment variables.


## ドキュメントでさらに学ぶ

- [コンテナーと仮想マシンの比較](/virtualization/windowscontainers/about/containers-vs-vm)。コンテナーと仮想マシン (VM) の主な類似点と相違点、およびそれぞれをどんなときに使うべきかを解説する記事です。

- [クイックスタート: Azure portal を使用して Azure にコンテナー インスタンスをデプロイする](/azure/container-instances/container-instances-quickstart-portal)。このクイックスタートでは、Azure portal を使って分離された Docker コンテナーをデプロイし、そのアプリケーションを完全修飾ドメイン名 (FQDN) で利用できるようにします。いくつかの設定を構成してコンテナーをデプロイした後、動作中のアプリケーションにブラウザーでアクセスできます。

- [Azure Container Instances のコンテナー グループ](/azure/container-instances/container-instances-container-groups)。コンテナー グループとは何か、どのようなシナリオを実現できるかを説明する記事です。

## 自習型トレーニングでさらに学ぶ

- [Azure Container Instances でコンテナー イメージを実行する](/training/modules/create-run-container-images-azure-container-instances/)。Azure Container Instances でコンテナーを素早くデプロイする方法、環境変数の設定方法、コンテナーの再起動ポリシーの指定方法を学びます。

- [Azure Container Apps を実装する](/training/modules/implement-azure-container-apps/)。Azure Kubernetes Service 上で動作するサーバーレス プラットフォームで、Azure Container Apps を使ってマイクロサービスとコンテナー化されたアプリをデプロイ・管理する方法を学びます。

- [Docker コンテナーの概要](/training/modules/intro-to-docker-containers/)。コンテナー化プラットフォームとして Docker コンテナーを使う利点を学びます。Docker プラットフォームが提供するインフラについても説明します。
