---
title: 配置共用隊列
seo-title: Configure shared queues
description: 了解如何在OSGi上使用以Forms為中心的AEM Forms工作流程的共用佇列。
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

# 共用並請求對用戶收件箱項的訪問 {#share-and-request-access}

佇列是使用者AEM收件匣中的項目清單。 這些項目可以指派給使用者，或是指派給使用者所屬群組的項目。 您可以存取收件匣以檢視收件匣項目並採取動作。 例如，與另一個使用者共用項目。

您也可以與其他使用者共用您的收件匣項目。 一旦其他用戶可以訪問您的收件箱項目，該用戶就可以對共用項目聲明並採取相應操作。 同樣地，您也可以向其他使用者申請「收件匣」項目的存取權。

## 先決條件 {#pre-requisites}

登入的使用者必須是 `workflow-users` 群組。 使用者只能向登入使用者具有已啟用公開設定檔之使用者的讀取權限或僅向使用者，共用項目或要求存取項目。

## 將收件箱的單個或所有項目與其他用戶共用

AEM收件匣可讓您與其他使用者共用收件匣中的單一或所有項目。

### 共用所有收件匣項目

執行下列步驟以與其他使用者共用收件匣中的所有項目：

1. 登入您的AEM例項。 點選 ![收件匣](assets/bell.svg) 圖示和點選 **[!UICONTROL 查看全部]**. 收件匣項目清單隨即出現。
1. 點選 ![檢視選取器](assets/viewlist.svg) 或 ![檢視選取器](assets/calendar.svg) 表徵圖 **[!UICONTROL 建立]** 按鈕和點選 **[!UICONTROL 設定]**. 設定對話方塊隨即出現。
1. 開啟 **[!UICONTROL 共用]** 頁簽。
1. 在 **[!UICONTROL 授予收件匣項目的存取權]** 文字方塊和點選 **[!UICONTROL 授予]**. 重複此步驟以新增更多使用者。 所有可存取您項目的使用者都會顯示在 **使用者名稱** 區段。
1. 點選 **[!UICONTROL 儲存]**.

>[!NOTE]
>
>(僅限以Forms為中心的工作流程項目)啟用 **[允許受託人透過收件匣共用來共用](aem-forms-workflow-step-reference.md)** 選項 **分配任務** 步驟。 只有已啟用上述選項的項目才會顯示給其他使用者。

### 共用個別項目

執行下列步驟以與其他用戶共用收件箱項：

1. 登入您的AEM例項。 點選 ![收件匣](assets/bell.svg) 圖示和點選 **[!UICONTROL 查看全部]**. 收件匣項目清單隨即出現。
1. 選取項目並點選 **[!UICONTROL 共用]**. 對話方塊隨即顯示。
1. 在「新增使用者以共用此項目」文字方塊中輸入使用者的名稱，然後點選 **[!UICONTROL 新增]**. 重複此步驟以新增更多使用者。 所有可存取您項目的使用者都會顯示在 **[!UICONTROL 使用者名稱]** 區段。
1. 點選 **[!UICONTROL 儲存]**.


>[!NOTE]
>
>(僅限以Forms為中心的工作流程項目)啟用 **[允許受託人在收件匣中明確共用](aem-forms-workflow-step-reference.md)** 選項 **分配任務** 步驟。 只有已啟用上述選項的項目才會顯示給其他使用者。

## 請求對收件箱項的訪問 {#request-access}

您可以請求對其他用戶的收件箱項的訪問。 授予存取權後，您就可以檢視、申請和對共用項目採取適當動作。 執行以下步驟以請求訪問其他用戶的收件箱項：

1. 登入您的AEM例項。 點選 ![檢視選取器](assets/bell.svg) 圖示和點選 **[!UICONTROL 查看全部]**.
1. 點選 ![檢視選取器](assets/viewlist.svg) 或 ![檢視選取器](assets/calendar.svg) 表徵圖 **[!UICONTROL 建立]** 按鈕和點選 **[!UICONTROL 設定]**. 設定對話方塊隨即出現。
1. 在 **[!UICONTROL 請求訪問用戶的收件箱項]** 文字方塊和點選 **[!UICONTROL 要求]**. 系統會傳送要求給使用者，而要求的狀態會根據使用者的名稱顯示。 重複此步驟以新增更多使用者。
1. 點選 **[!UICONTROL 儲存]**. 請求會以收件匣項目的形式傳送給使用者。 使用者可以選取項目，點選「核准」或「拒絕」以授與或拒絕存取權。


## 其他用戶共用的聲明項 {#claim-items}

只有在您聲明共用項目後，才能開始使用該項目。 它可防止多個使用者處理單一項目。 執行以下步驟來申請項目：

1. 登入您的AEM例項。 點選收件匣 ![收件匣](assets/bell.svg) 圖示和點選 **[!UICONTROL 查看全部]**.
1. 點選 ![僅內容](assets/railleft.svg) 圖示來開啟篩選器選取器。
1. 點選 **[!UICONTROL 選擇受託人]** 下拉式清單，檢視並選取已與您共用其收件匣項目的使用者。
1. 選取項目並點選 **[!UICONTROL 索賠]**. 項目會新增至您的收件匣。

## 釋放申請的項目 {#release-items}

只有在您聲明共用項目後，才能處理該項目。 其他使用者無法查看或處理您申請的項目。 如果無法繼續處理某個項目，則可將其釋放回池。   在您釋放項目後，其他人可以聲明並處理該項目：

執行下列步驟以發行項目：

1. 登入您的AEM例項。 點選收件匣 ![收件匣](assets/bell.svg) 圖示和點選 **[!UICONTROL 查看全部]**. 收件匣項目清單隨即出現。
1. 選取要釋放的項目，然後點選 **[!UICONTROL UnClaim]**. 項將添加回池。 其他人現在可以申請項目。

## 限制 {#limitations}

* 不支援與群組共用項目。
* 不支援共用項目任務。
