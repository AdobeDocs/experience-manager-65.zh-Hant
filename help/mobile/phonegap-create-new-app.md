---
title: 使用建立嚮導建立新的AEM Mobile應用
seo-title: Creating a new AEM Mobile app using create wizard
description: AEM Mobile應用基於一個定義頁面結構和屬性的藍圖。 按照此頁瞭解如何基於應用模板建立新應用。
seo-description: AEM Mobile apps are based on a blueprint that defines a page structure and properties. Follow this page to learn about how to create a new app based on an app template.
uuid: c2bd63a5-3dff-4a72-b1fb-0c776e0afa33
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 27605eb7-59b2-42d4-8cc5-02cfa52b4491
exl-id: be093025-b19f-4499-a7b5-aae5ab74f966
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 1%

---

# 使用建立嚮導建立新的AEM Mobile應用{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

AEM Mobile應用基於一個定義頁面結構和屬性的藍圖。 可以配置以下應用程式屬性：

* **標題：** 應用程式標題。
* **目標路徑：** 儲存應用程式的儲存庫中的位置。 保留預設值以基於應用名稱建立路徑。

* **名稱：** 預設值是刪除空格字元的Title屬性的值。 名稱在中用AEM於引用應用程式，例如，用於表示應用程式的儲存庫節點。
* **描述：** 應用程式的說明。
* **伺服器URL:** 為應用程式提供空中傳輸(OTA)內容更新的URL。 預設值是用於建立應用程式（從外部化程式服務獲取）的實例的發佈伺服器URL。 注意，這必須是發佈伺服器實例，而不是需要身份驗證的作者。

您還可以提供要用作應用程式縮略圖的影像檔案，選擇要使用的PhoneGap Build配置，以及選擇要使用的Mobile App分析配置。 此影像僅用作縮略圖，用於在Experience Manager中的移動應用控制台中表示您的移動應用程式。

存在用於構建雲服務和將Adobe移動服務SDK插件整合到應用的其他（可選）頁籤。

* 生成：按一下「管理配置」，然後在此處設定build.phonegap.com構建服務。 然後，您將能夠從下拉清單中選擇新建立的PhoneGap構建雲服務。
* 分析：按一下管理配置並設定 [Adobe移動服務SDK](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) 雲服務。 然後，您將能夠從下拉清單中選擇新建立的移動服務，以整合到您的移動應用。

## 使用應用模板 {#using-app-templates}

應用程式模板提供了一種利用開發人員建立的現有設計的簡便方法，這些設計用於在中建立新應AEM用。

什麼是應用模板？ 將其視為表示應用的基線或基礎的頁面模板和元件的集合。
在基於另一個應用的模板建立新應用時，您將得到一個應用，該應用的起始點代表從中建立該應用的應用。

您必須擁有現有的移動應用模板（或安裝了應用模板的應用）才能使用此功能。

最新的AEMApps示例包包括帶應用模板的Geometrixx應用的更新版本。 或者，您可以安裝 [簡易套件](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) 也提供了模板。

基於應用模板建立新應用的步驟：

1. 導航到AEM Mobile應用目錄：&lt;*伺服器URL*>aem/apps.html/內容/移動應用
1. 選擇 **建立** 然後選擇 **應用** 如下所示

![chlimage_1-158](assets/chlimage_1-158.png)

選擇由開發人員提供給您的應用AEM模板。 請參閱 [AEM Mobile應用的結構](/help/mobile/phonegap-structure-an-app.md) 開發人員幫助。

![chlimage_1-159](assets/chlimage_1-159.png)

根據需要填寫新應用的詳細資訊，包括可選地更改其縮略圖。 這些值稍後可以從 **管理應用** 平鋪。

![chlimage_1-160](assets/chlimage_1-160.png)

## 後續步驟 {#the-next-steps}

請參閱以下資源以瞭解有關其他創作角色的詳細資訊：

* [管理應用程式磁貼](/help/mobile/phonegap-app-details-tile.md)
* [編輯應用元資料](/help/mobile/phonegap-editmetadata.md)
* [應用定義](/help/mobile/phonegap-app-definitions.md)
* [導入現有混合應用](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## 其他資源 {#additional-resources}

要瞭解管理員和開發人員的角色和職責，請參閱以下資源：

* [Adobe PhoneGap企業AEM發展](/help/mobile/developing-in-phonegap.md)
* [為Adobe PhoneGap企業管理內AEM容](/help/mobile/administer-phonegap.md)
