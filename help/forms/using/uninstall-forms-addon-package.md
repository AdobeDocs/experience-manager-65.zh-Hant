---
title: 本文包括使用CRX封裝管理員解除安裝Forms附加元件套件的指示。
description: 瞭解使用CRX封裝管理員解除安裝Forms附加元件套件的步驟。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 2755e414ea23ebc1472e9c08d832eca93f28311b
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---


# 從AEM執行個體解除安裝AEM Forms附加元件套件

本文概述從AEM Forms SDK執行個體正確解除安裝AEM Forms附加元件套件所需的步驟。 請依照這些步驟操作，以確保移除Forms附加元件套件，防止您的AEM環境發生潛在問題。

## 先決條件

請務必進行備份，以避免任何資料遺失。

## 若要解除安裝AEM Forms附加元件套件

若要解除安裝AEM Forms附加元件套件，請執行以下步驟：

1. **解除安裝AEM Forms附加元件套件：**
   1. 導覽至 `http://[host]:[port]/crx/de/index.jsp`.
   1. 找到並解除安裝 `AEM Forms add-on package`.

   ![解除安裝套裝](/help/forms/using/assets/uninstall-aem-forms-package.png)

1. **從CRXDE刪除原生資料夾：**
   1. 導覽至 `http://[host]:[port]/crx/de/index.jsp`.
   1. 前往 `/libs/fd/native/install` 並刪除 `native` CRXDE中的資料夾。

      ![從CRX/de刪除原生節點](/help/forms/using/assets/native-install-folder-crxde.png)
   1. 儲存變更。

1. **停止AEM Forms SDK：**
   1. 使用「Ctrl + C」命令停止AEM Forms SDK執行個體。

1. **檢查crx-quickstart資料夾中的基礎和安裝資料夾**
   1. 瀏覽至 `..author\crx-quickstart` AEM Forms SDK例項中的資料夾。
   1. 搜尋名為的資料夾 `bedrock` 和 `install`.
如果找到，請確定它們已從 `crx-quickstart` AEM Forms SDK例項中的資料夾。

   >[!NOTE]
   >
   > 此 `bedrock` 當您重新啟動AEM Forms SDK執行個體時，資料夾會再次自動建立。

1. **重新啟動AEM執行個體：**
   1. 完成所有先前的步驟後， [重新啟動AEM Forms SDK執行個體](/help/forms/using/restart-aem-sdk.md).




