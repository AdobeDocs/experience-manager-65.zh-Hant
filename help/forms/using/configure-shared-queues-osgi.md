---
title: 配置共用隊列
seo-title: Configure shared queues
description: 瞭解如何在OSGi上將共用隊列用於以Forms為中心的AEM Forms工作流。
seo-description: Learn how to use shared queues for Forms-centric workflows on AEM Forms on OSGi.
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 72cd0594-8b5e-4d14-bc6f-bca26bae50f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# 共用並請求訪問用戶的收件箱項 {#share-and-request-access}

隊列是用戶收件箱AEM中項的清單。 這些項目可以分配給用戶，也可以是分配給用戶所屬的組的項目。 您可以訪問「收件箱」，查看收件箱項並對其執行操作。 例如，與另一用戶共用項目。

您還可以與其他用戶共用收件箱項目。 一旦其他用戶有權訪問您的收件箱項目，用戶就可以聲明共用項目並採取相應的措施。 同樣，您也可以從其他用戶請求訪問收件箱項。

## 先決條件 {#pre-requisites}

登錄用戶必須是 `workflow-users` 組。 用戶只能共用項目或請求僅從登錄用戶對啟用了公共配置檔案的用戶具有讀取權限的用戶或僅從啟用公共配置檔案的用戶訪問項目。

## 與其他用戶共用收件箱中的單個或所有項目

AEM收件箱允許您與其他用戶共用收件箱中的單個或所有項目。

### 共用所有收件箱項

執行以下步驟與其他用戶共用收件箱中的所有項目：

1. 登錄到實AEM例。 點擊 ![收件箱](assets/bell.svg) 表徵圖和點擊 **[!UICONTROL 全部查看]**。 將顯示收件箱項的清單。
1. 點擊 ![視圖選擇器](assets/viewlist.svg) 或 ![視圖選擇器](assets/calendar.svg) 表徵圖 **[!UICONTROL 建立]** 按鈕 **[!UICONTROL 設定]**。 將顯示「設定」對話框。
1. 開啟 **[!UICONTROL 共用]** 的子菜單。
1. 在 **[!UICONTROL 授予對收件箱項目的訪問權限]** 文本框和點擊 **[!UICONTROL 授予]**。 重複此步驟以添加更多用戶。 所有有權訪問您的項目的用戶都顯示在 **用戶名** 的子菜單。
1. 點擊 **[!UICONTROL 保存]**。

>[!NOTE]
>
>(僅適用於以Forms為中心的工作流項)啟用 **[允許受分配人通過收件箱共用共用](aem-forms-workflow-step-reference.md)** 選項 **分配任務** 的子菜單。 只有啟用了上述選項的項目才會顯示給其他用戶。

### 共用單個項目

執行以下步驟與其他用戶共用收件箱項：

1. 登錄到實AEM例。 點擊 ![收件箱](assets/bell.svg) 表徵圖和點擊 **[!UICONTROL 全部查看]**。 將顯示收件箱項的清單。
1. 選擇項目並點擊 **[!UICONTROL 共用]**。 對話方塊隨即顯示。
1. 在「添加用戶以共用此項目」文本框中輸入用戶的名稱，然後點擊 **[!UICONTROL 添加]**。 重複此步驟以添加更多用戶。 所有有權訪問您的項目的用戶都顯示在 **[!UICONTROL 用戶名]** 的子菜單。
1. 點擊 **[!UICONTROL 保存]**。


>[!NOTE]
>
>(僅適用於以Forms為中心的工作流項)啟用 **[允許受分配人在收件箱中顯式共用](aem-forms-workflow-step-reference.md)** 選項 **分配任務** 的子菜單。 只有啟用了上述選項的項目才會顯示給其他用戶。

## 請求訪問收件箱項 {#request-access}

您可以請求訪問其他用戶的收件箱項。 一旦授予訪問權限，您就可以查看、聲明共用項目並採取相應的操作。 執行以下步驟以請求訪問其他用戶的收件箱項：

1. 登錄到實AEM例。 點擊 ![視圖選擇器](assets/bell.svg) 表徵圖和點擊 **[!UICONTROL 全部查看]**。
1. 點擊 ![視圖選擇器](assets/viewlist.svg) 或 ![視圖選擇器](assets/calendar.svg) 表徵圖 **[!UICONTROL 建立]** 按鈕 **[!UICONTROL 設定]**。 將顯示「設定」對話框。
1. 在 **[!UICONTROL 請求訪問用戶的收件箱項]** 文本框和點擊 **[!UICONTROL 請求]**。 向用戶發送請求，並根據用戶的名稱顯示請求的狀態。 重複此步驟以添加更多用戶。
1. 點擊 **[!UICONTROL 保存]**。 該請求作為收件箱項目發送給用戶。 用戶可以選擇項目，然後點擊「批准」或「拒絕」以授予或拒絕訪問權限。


## 其他用戶共用的聲明項 {#claim-items}

只有在您聲明共用項目後，才可開始處理該項目。 它防止多個用戶處理單個項目。 執行以下步驟來聲明項目：

1. 登錄到實AEM例。 點擊收件箱 ![收件箱](assets/bell.svg) 表徵圖和點擊 **[!UICONTROL 全部查看]**。
1. 點擊 ![僅內容](assets/railleft.svg) 表徵圖以開啟篩選器選擇器。
1. 點擊 **[!UICONTROL 選擇受分配人]** 下拉框，查看並選擇與您共用收件箱項目的用戶。
1. 選擇項目並點擊 **[!UICONTROL 索賠]**。 該項目將添加到您的收件箱中。

## 釋放索賠項 {#release-items}

只有在您聲明共用項後，才能處理該項。 其他用戶無法查看或處理您聲明的項目。 如果無法繼續處理項目，可將其釋放回池。   釋放物料後，其他人可以聲明並處理物料：

執行以下步驟以釋放項目：

1. 登錄到實AEM例。 點擊收件箱 ![收件箱](assets/bell.svg) 表徵圖和點擊 **[!UICONTROL 全部查看]**。 將顯示收件箱項的清單。
1. 選擇要釋放的項，然後點擊 **[!UICONTROL 取消聲明]**。 該項將被添加回池。 其他人現在可以申請該項目。

## 限制 {#limitations}

* 不支援與組共用項。
* 不支援共用項目任務。
