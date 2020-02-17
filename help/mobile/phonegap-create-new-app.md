---
title: 使用建立精靈建立新的AEM mobile應用程式
seo-title: 使用建立精靈建立新的AEM mobile應用程式
description: AEM mobile應用程式是以定義頁面結構和屬性的藍圖為基礎。 請依照本頁來瞭解如何根據應用程式範本建立新應用程式。
seo-description: AEM mobile應用程式是以定義頁面結構和屬性的藍圖為基礎。 請依照本頁來瞭解如何根據應用程式範本建立新應用程式。
uuid: c2bd63a5-3dff-4a72-b1fb-0c776e0afa33
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 27605eb7-59b2-42d4-8cc5-02cfa52b4491
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用建立精靈建立新的AEM mobile應用程式{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

AEM mobile應用程式是以定義頁面結構和屬性的藍圖為基礎。 您可以設定下列應用程式屬性：

* **** 標題：應用程式標題。
* **** 目標路徑：儲存應用程式的儲存庫中的位置。 保留預設值，以根據應用程式名稱建立路徑。

* **** 名稱：預設值是Title屬性的值，並刪除空格字元。 AEM中使用名稱來引用應用程式，例如代表應用程式的儲存庫節點。
* **** 說明：應用程式的說明。
* **** 伺服器URL:提供Over-the-Air(OTA)內容更新至應用程式的URL。 預設值是用來建立應用程式（取自外部化器服務）之例項的發佈伺服器URL。 請注意，此為發佈伺服器例項，而非需要驗證的作者。

您也可以提供影像檔案做為應用程式縮圖，選取要使用的PhoneGap Build設定，然後選取要使用的行動應用程式分析設定。 此影像僅用作縮圖，以在Experience Manager的行動應用程式主控台中呈現您的行動應用程式。

建立雲端服務並將Adobe Mobile Services SDK外掛程式整合至應用程式時，會有其他（和選用）標籤。

* 構建：按一下「管理設定」，並在此處設定build.phonegap.com組建服務。 然後，您就可以從下拉式清單中選取新建立的PhoneGap組建雲端服務。
* 分析：按一下「管理組態」，並設定 [您的Adobe Mobile Services SDK](https://marketing.adobe.com/developer/en_US/get-started/mobile/c-measuring-mobile-applications) cloud服務。 然後，您就可以從下拉式清單中，選取新建立的Mobile Service，以整合到您的行動應用程式中。

## 使用應用程式範本 {#using-app-templates}

應用程式範本提供簡單的方式，來運用開發人員建立的現有設計，以便在AEM中建立新應用程式。

什麼是應用程式範本？ 將它設想成代表應用程式基準或基礎的頁面範本和元件集合。
根據其他應用程式的範本建立新應用程式時，您會得到一個應用程式，其起點代表建立應用程式的應用程式。

您必須有現有的行動應用程式範本（或已安裝應用程式範本的應用程式），才能使用此功能。

最新的AEM Apps範例套件包含Geometrixx應用程式的更新版本及應用程式範本。 或者，您也可以安裝 [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) ，該StarterKit也提供範本。

根據應用程式範本建立新應用程式的步驟：

1. 導覽至AEM mobile應用程式目錄：&lt;*server-url*>aem/apps.html/content/mobileapps
1. 選取「 **建立** 」，然後選擇「 **應用程式** 」，如下所示

![chlimage_1-158](assets/chlimage_1-158.png)

選取AEM開發人員提供給您的應用程式範本。 請參 [閱「AEM Mobile應用程式的結構」](/help/mobile/phonegap-structure-an-app.md) ，以取得開發人員協助。

![chlimage_1-159](assets/chlimage_1-159.png)

視需要填寫新應用程式的詳細資訊，包括選擇性地變更其縮圖影像。 這些值稍後可從「管理應用程式」方 **塊中編輯** 。

![chlimage_1-160](assets/chlimage_1-160.png)

## 後續步驟 {#the-next-steps}

請參閱下列資源以進一步瞭解其他編寫角色：

* [管理應用程式圖格](/help/mobile/phonegap-app-details-tile.md)
* [編輯應用程式中繼資料](/help/mobile/phonegap-editmetadata.md)
* [應用程式定義](/help/mobile/phonegap-app-definitions.md)
* [匯入現有的混合應用程式](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## 其他資源 {#additional-resources}

要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [使用AEM為Adobe PhoneGap Enterprise進行開發](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)
