---
title: 設定用於Acrobat Reader DC擴充功能的認證
description: 瞭解如何設定憑證以與Acrobat Reader DC擴充功能搭配使用。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e8015d59-7587-46dc-a672-e0f1108102ad
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# 設定用於Acrobat Reader DC擴充功能的認證{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

若要套用使用許可權至PDF檔案，請使用Acrobat Reader DC擴充功能的有效認證來設定AEM表單。 可能在安裝AEM表單期間已設定認證。 如果您在執行Configuration Manager時未設定Acrobat Reader DC Extensions認證，或者如果您需要匯入新的或取代認證，可以使用「信任存放區管理」頁面進行設定。

如果您使用評估認證，請在移至生產環境時，以生產認證取代。 若要更新過期的或評估認證，請先刪除舊的Acrobat Reader DC擴充功能認證。

如需取得認證的相關資訊，請參閱[準備安裝AEM表單（單一伺服器）](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf)。

信任存放區可能包含多個Acrobat Reader DC擴充功能認證。 指定其中一個認證作為預設Reader延伸模組認證。 當Workbench使用者無法判斷要在流程建立期間使用哪個認證時，就會使用預設認證。 這些規則套用至預設認證：

* 如果您匯入Acrobat Reader DC擴充功能認證，但信任存放區不含其他Acrobat Reader DC擴充功能認證，系統就會將其設為預設值。
* 如果您匯入Acrobat Reader DC擴充功能認證，並選取「預設」選項，則會從現有的預設認證中移除預設型別。 匯入的認證會成為預設值。
* 您無法刪除預設的Acrobat Reader DC擴充功能認證。 若要刪除預設的認證，請先將另一個認證設定為預設值。 此規則的例外是，如果只有一個認證，則即使預設為認證，您也可以將其刪除。
* 您無法更新預設的Acrobat Reader DC擴充功能認證。

>[!NOTE]
>
>您也可以以程式設計方式匯入和刪除認證。 (請參閱[使用AEM表單進行程式設計](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hant)。)

## 匯入Acrobat Reader DC擴充功能認證 {#import-a-acrobat-reader-dc-extensions-credential}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「本機認證」。
1. 按一下匯入，然後在「信任存放區型別」下方選取「Acrobat Reader DC擴充功能認證」。
1. （選用）若要指出此認證是搭配Acrobat Reader DC擴充功能使用的預設認證，請選取「預設」。
1. 在「別名」方塊中，輸入認證的識別碼。 此識別碼會用作Acrobat Reader DC擴充功能中認證的顯示名稱。 此別名也會用來透過AEM表單SDK以程式設計方式存取認證。

   >[!NOTE]
   >
   >別名會自動轉換為大寫以供顯示。 您在程式中參考別名時，別名名稱不區分大小寫。

1. 按一下選擇檔案來尋找證明資料，輸入證明資料的密碼，然後按一下確定。

   如果出現錯誤訊息「由於檔案格式不正確或密碼不正確而無法匯入認證」，請確認密碼有效。

## 移除Acrobat Reader DC擴充功能認證 {#remove-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「本機認證」。
1. 選取認證並按一下刪除。

## 取代Acrobat Reader DC擴充功能認證 {#replace-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「本機認證」。
1. 記下現有認證的別名，然後選取並按一下刪除。
1. 使用完全相同的別名匯入新的認證。
