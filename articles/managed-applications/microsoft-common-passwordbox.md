---
title: "Azure マネージ アプリケーションの PasswordBox UI 要素 | Microsoft Docs"
description: "Azure マネージ アプリケーションの Microsoft.Common.PasswordBox UI 要素について説明します。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/12/2017
ms.author: tomfitz
ms.openlocfilehash: 6d9f2b7cf56375d3a609cff20e928307c13bf2b8
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a>Microsoft.Common.PasswordBox UI 要素
パスワードの提供と確認に使用できるコントロールです。 この要素は、[Azure マネージ アプリケーションを作成する](publish-service-catalog-app.md)ときに使用します。

## <a name="ui-sample"></a>UI サンプル
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a>スキーマ
```json
{
  "name": "element1",
  "type": "Microsoft.Common.PasswordBox",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "",
    "validationMessage": ""
  },
  "options": {
    "hideConfirmation": false
  },
  "visible": true
}
```

## <a name="remarks"></a>解説
- この要素は `defaultValue` プロパティをサポートしていません。
- `constraints` の実装の詳細については、[Microsoft.Common.TextBox](microsoft-common-textbox.md) に関する記事を参照してください。
- `options.hideConfirmation` が **true** に設定されている場合、ユーザーのパスワードを確認するための 2 つ目のテキスト ボックスは表示されません。 既定値は **false** です。

## <a name="sample-output"></a>サンプル出力
```json
"p4ssw0rd"
```

## <a name="next-steps"></a>次のステップ
* マネージ アプリケーションの概要については、「[Azure マネージ アプリケーションの概要](overview.md)」を参照してください。
* UI 定義の作成の概要については、「[CreateUiDefinition の基本概念](create-uidefinition-overview.md)」を参照してください。
* UI 要素の共通プロパティの説明については、「[CreateUiDefinition の要素](create-uidefinition-elements.md)」を参照してください。
