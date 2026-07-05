# AZ-104 学習リポジトリ

Microsoft Learn の **AZ-104: Microsoft Azure Administrator** 認定資格に関する
公式ラーニングパス／モジュールのコンテンツを、次のステップで日本語訳するために
このリポジトリへコピーしたものです。

- 出典: [MicrosoftDocs/learn](https://github.com/MicrosoftDocs/learn)（`learn-pr/paths/az-104-*` および対応モジュール）
- ライセンス: [CC BY 4.0](https://github.com/MicrosoftDocs/learn/blob/main/LICENSE)（Microsoft のコンテンツライセンスに従います）
- 取得日: 2026-07-05
- 原文言語: 英語（原文のまま `.md` / `.yml` で保存。翻訳は次工程で実施予定）

## ディレクトリ構成

`AZ-104/` 以下に、公式の6つのラーニングパスをそれぞれ番号付きフォルダとして配置しています。
各パスフォルダには `_path.yml`（ラーニングパスのメタデータ）と、
含まれるモジュールのフォルダ（`index.yml` + `includes/*.md`）を格納しています。

```
AZ-104/
  01-prerequisites/            AZ-104: Prerequisites for Azure administrators
  02-compute/                  AZ-104: Deploy and manage Azure compute resources
  03-identities-governance/    AZ-104: Manage identities and governance in Azure
  04-storage/                  AZ-104: Implement and manage storage in Azure
  05-virtual-networks/         AZ-104: Configure and manage virtual networks for Azure administrators
  06-monitor-backup/           AZ-104: Monitor and back up Azure resources
```

### 各モジュールのフォルダ構成

```
<module-name>/
  index.yml         モジュールのメタデータ(タイトル、概要、ユニット一覧など)
  includes/
    1-introduction.md
    2-....md
    ...
    N-summary(-resources).md
```

## 収録モジュール一覧

### 01-prerequisites: AZ-104: Prerequisites for Azure administrators
- `intro-to-azure-cloud-shell` - Introduction to Azure Cloud Shell
- `create-azure-resource-manager-template-vs-code` - Deploy Azure infrastructure by using JSON ARM templates

### 02-compute: AZ-104: Deploy and manage Azure compute resources
- `intro-to-azure-virtual-machines` - Introduction to Azure virtual machines
- `configure-virtual-machine-availability` - Configure virtual machine availability
- `configure-app-service-plans` - Configure Azure App Service plans
- `configure-azure-app-services` - Configure Azure App Service
- `configure-azure-container-instances` - Configure Azure Container Instances

### 03-identities-governance: AZ-104: Manage identities and governance in Azure
- `understand-azure-active-directory` - Understand Microsoft Entra ID
- `describe-core-architectural-components-of-azure` - Describe the core architectural components of Azure
- `secure-azure-resources-with-rbac` - Secure your Azure resources with Azure role-based access control (Azure RBAC)
- `allow-users-reset-their-password` - Allow users to reset their password with Microsoft Entra self-service password reset
- **未収録（下記「収録できなかったモジュール」参照）**: Create, configure, and manage identities / Azure Policy initiatives

### 04-storage: AZ-104: Implement and manage storage in Azure
- `configure-storage-accounts` - Configure storage accounts
- `configure-blob-storage` - Configure Azure Blob Storage
- `configure-storage-security` - Configure Azure Storage security
- `configure-azure-files-file-sync` - Configure Azure Files

### 05-virtual-networks: AZ-104: Configure and manage virtual networks for Azure administrators
- `configure-virtual-networks` - Configure virtual networks
- `configure-network-security-groups` - Configure network security groups
- `host-domain-azure-dns` - Host your domain on Azure DNS
- `configure-vnet-peering` - Configure Azure Virtual Network peering
- `control-network-traffic-flow-with-routes` - Manage and control traffic flow in your Azure deployment with routes
- `intro-to-azure-load-balancer` - Introduction to Azure Load Balancer
- `intro-to-azure-application-gateway` - Introduction to Azure Application Gateway
- `intro-to-azure-network-watcher` - Introduction to Azure Network Watcher

### 06-monitor-backup: AZ-104: Monitor and back up Azure resources
- `intro-to-azure-backup` - Introduction to Azure Backup
- `protect-virtual-machines-with-azure-backup` - Protect your virtual machines by using Azure Backup
- `monitor-azure-vm-using-diagnostic-data` - Monitor your Azure virtual machines with Azure Monitor

## 収録できなかったモジュール

ネットワーク経由でのソース特定が困難だったため、以下の2モジュール（いずれも
「03-identities-governance」パス内）は自動収集の対象から漏れています。
次工程で翻訳作業を行う際は、下記リンク先から手動で内容を補ってください。

- Create, configure, and manage identities
  https://learn.microsoft.com/en-us/training/modules/create-configure-manage-identities/
- Azure Policy initiatives
  https://learn.microsoft.com/en-us/training/modules/sovereignty-policy-initiatives/

## 今後の予定

このリポジトリのコンテンツ（`index.yml` の `title` / `summary` / `abstract` と、
`includes/*.md` 本文）を日本語に翻訳する作業を次のステップで行います。
