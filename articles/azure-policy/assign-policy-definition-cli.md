---
title: "Azure CLI を使用してポリシーの割り当てを作成し、Azure 環境内の準拠していないリソースを特定する | Microsoft Docs"
description: "PowerShell を使用して Azure Policy の割り当てを作成し、準拠していないリソースを特定します。"
services: azure-policy
keywords: 
author: bandersmsft
ms.author: banders
ms.date: 12/06/2017
ms.topic: quickstart
ms.service: azure-policy
ms.custom: mvc
ms.openlocfilehash: 88ceb47d46b66e716c6c263098d5b9458e4aff22
ms.sourcegitcommit: cc03e42cffdec775515f489fa8e02edd35fd83dc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2017
---
# <a name="create-a-policy-assignment-to-identify-non-compliant-resources-in-your-azure-environment-with-the-azure-cli"></a>Azure CLI を使用してポリシーの割り当てを作成し、Azure 環境内の準拠していないリソースを特定する

Azure のコンプライアンスを理解する第一歩は、自分の現在のリソースの状態を把握することです。 このクイックスタートでは、ポリシー割り当てを作成して、管理ディスクを使用していない仮想マシンを特定するプロセスについて順を追って説明します。

このプロセスを終了すると、管理ディスクを使用していない、つまり "*非準拠*" の仮想マシンを適切に特定できるようになります。

Azure サブスクリプションをお持ちでない場合は、開始する前に[無料](https://azure.microsoft.com/free/)アカウントを作成してください。

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

CLI をローカルにインストールして使用する場合、このクイック スタートを実施するには、Azure CLI バージョン 2.0.4 以降を実行している必要があります。 バージョンを確認するには、`az --version` を実行します。 インストールまたはアップグレードする必要がある場合は、「[Azure CLI 2.0 のインストール]( /cli/azure/install-azure-cli)」を参照してください。

## <a name="create-a-policy-assignment"></a>ポリシー割り当てを作成する

このクイックスタートでは、ポリシー割り当てを作成し、"管理ディスクのない仮想マシンを監査" 定義を割り当てます。 このポリシー定義で、ポリシー定義に設定されている条件に準拠していないリソースを特定します。

次の手順で新しいポリシー割り当てを作成します。

すべてのポリシー定義を表示し、"管理ディスクのない仮想マシンを監査" ポリシー定義を見つけます。

```azurecli
az policy definition list
```

Azure Policy には、使用できる組み込みのポリシー定義があらかじめ含まれています。 次のような組み込みのポリシー定義が表示されます。

- Enforce tag and its value (タグとその値を強制する)
- タグとその値を適用
- Require SQL Server Version 12.0 (SQL Server バージョン 12.0 が必要)

次に、以下の情報を入力し、次のコマンドを実行してポリシー定義を割り当てます。

- ポリシー割り当ての表示用の**名前**。 ここでは、"*管理ディスクのない仮想マシンを監査*" を使用しましょう。
- **ポリシー** - 割り当ての作成に使用している基のポリシー定義です。 ここでは、"*管理ディスクのない仮想マシンを監査*" というポリシー定義です
- **スコープ** - スコープによって、ポリシー割り当てを強制するリソースまたはリソースのグループが決まります。 サブスクリプションからリソース グループまで、適用対象は多岐にわたります。

  以前に登録したサブスクリプション (またはリソース グループ) を使います。 この例では、**bc75htn-a0fhsi-349b-56gh-4fghti-f84852** というサブスクリプション ID と、**FabrikamOMS** というリソース グループ名を使っています。 これらの値は、実際に使用するサブスクリプションの ID とリソース グループの名前に変更してください。

コマンドは次のようになります。

```azurecli
az policy assignment create --name Audit Virtual Machines without Managed Disks Assignment --policy Audit Virtual Machines without Managed Disks --scope /subscriptions/
bc75htn-a0fhsi-349b-56gh-4fghti-f84852/resourceGroups/FabrikamOMS
```

ポリシー割り当ては、特定のスコープ内で実行するように割り当てられたポリシーです。 このスコープは、管理グループからリソース グループの範囲になる可能性があります。

## <a name="identify-non-compliant-resources"></a>準拠していないリソースを特定する

この新しい割り当てに準拠していないリソースを表示するには:

1. Azure Policy ページに戻ります。
2. 左側のウィンドウで **[Compliance]\(コンプライアンス\)** を選択し、作成した**ポリシー割り当て**を検索します。

   ![ポリシーのコンプライアンス](media/assign-policy-definition/policy-compliance.png)

   この新しい割り当てに準拠していない既存のリソースがある場合、上図のように **[Non-compliant resources]\(準拠していないリソース\)** タブに表示されます。

## <a name="clean-up-resources"></a>リソースのクリーンアップ

このコレクションの他のガイドは、このクイックスタートに基づいています。 引き続きチュートリアルの作業を行う場合は、このクイックスタートで作成したリソースをクリーンアップしないでください。 続行する予定がない場合は、次のコマンドを実行して、作成した割り当てを削除してください。

```azurecli
az policy assignment delete –name  Assignment --scope /subscriptions/ bc75htn-a0fhsi-349b-56gh-4fghti-f84852 resourceGroups/ FabrikamOMS
```

## <a name="next-steps"></a>次のステップ

このクイックスタートでは、ポリシー定義を割り当てて、Azure 環境内で準拠していないリソースを特定しました。

ポリシーの割り当てについて詳しく学び、**今後**作成されるリソースが準拠していることを確認するには、チュートリアルを続行してください。

> [!div class="nextstepaction"]
> [ポリシーの作成と管理](./create-manage-policy.md)
