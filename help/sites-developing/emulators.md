---
title: 模擬器
seo-title: 模擬器
description: AEM可讓作者在模擬一般使用者將檢視頁面的環境的模擬器中檢視頁面
seo-description: AEM可讓作者在模擬一般使用者將檢視頁面的環境的模擬器中檢視頁面
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 模擬器{#emulators}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

Adobe Experience Manager(AEM)可讓作者在模擬一般使用者將檢視頁面的環境的模擬器中檢視頁面，例如在行動裝置或電子郵件用戶端中。

AEM模擬器架構：

* 在模擬使用者介面(UI)中提供內容製作，例如行動裝置或電子郵件用戶端（用來製作電子報）。
* 根據模擬的UI調整頁面內容。
* 允許建立自定義模擬器。

>[!CAUTION]
>
>此功能僅在Classic UI中受支援。

## 模擬器特性 {#emulators-characteristics}

模擬器：

* 以ExtJS為基礎。
* 在頁面DOM上運作。
* 它的外觀是透過CSS來調整。
* 支援外掛程式（例如行動裝置旋轉外掛程式）。
* 僅在作者上作用中。
* 其基本元件為 `/libs/wcm/emulator/components/base`。

### 模擬器如何轉換內容 {#how-the-emulator-transforms-the-content}

模擬器可將HTML內容包裝到模擬器DIV中。 例如，下列html程式碼：

```xml
<body>
<div id="wrapper" class="page mobilecontentpage ">
    <div class="topnav mobiletopnav">
    ...
    </div>
    ...
</div>
</body>
```

在模擬器啟動後，會轉換成下列html程式碼：

```xml
<body>
 <div id="cq-emulator-toolbar">
 ...
 </div>
 <div id="cq-emulator-wrapper">
  <div id="cq-emulator-device">
   <div class=" android vertical" id="cq-emulator">
    ...
    <div class=" android vertical" id="cq-emulator-content">
     ...
     <div id="wrapper" class="page mobilecontentpage">
     ...
     </div>
     ...
    </div>
   </div>
  </div>
 </div>
 ...
</body>
```

已新增兩個div標籤：

* div的ID可 `cq-emulator` 將模擬器整體保留

* div的ID `cq-emulator-content` 代表裝置的檢視區／螢幕／內容區域，頁面內容位於此區域。

新的CSS類別也會指派給新的模擬器div:它們表示當前模擬器的名稱。

模擬器的外掛程式可進一步擴充指派的CSS類別清單，如旋轉外掛程式的範例，視目前裝置旋轉而插入「垂直」或「水準」類別。

這樣，通過使CSS類與模擬器div的ID和CSS類相對應，可以控制模擬器的完整外觀。

>[!NOTE]
>
>建議專案HTML將內文內容包住在單一div中，就像上述範例中一樣。 如果內文內容包含多個標籤，可能會產生無法預測的結果。

### 行動模擬器 {#mobile-emulators}

現有的行動模擬器：

* 位於/libs/wcm/mobile/components/emulators下方。
* 可透過JSON servlet取得，網址為：

   http://localhost:4502/bin/wcm/mobile/emulators.json

當頁面元件依賴行動頁面元件( `/libs/wcm/mobile/components/page`)時，模擬器功能會透過下列機制自動整合在頁面中：

* 行動頁面元 `head.jsp` 件包含裝置群組的相關模擬器init元件（僅在作者模式中）和裝置群組的轉換CSS:

   `deviceGroup.drawHead(pageContext);`

* 該方 `DeviceGroup.drawHead(pageContext)` 法包括模擬器的init元件，即調用 `init.html.jsp` 模擬器元件。 如果模擬器元件沒有自己的模 `init.html.jsp` 擬器，並且依賴於移動基本模擬器( `wcm/mobile/components/emulators/base)`，則調用移動基本模擬器的init指令碼( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`)。

* 行動基本模擬器的init指令碼是透過Javascript定義：

   * 為該頁定義的所有模擬器的配置(emulatorConfigs)
   * 模擬器管理器通過以下方式將模擬器功能整合到頁面中：

      `emulatorMgr.launch(config)`;

      模擬器管理器由：

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### 建立自訂行動模擬器 {#creating-a-custom-mobile-emulator}

若要建立自訂的行動模擬器：

1. 以下 `/apps/myapp/components/emulators` 建立元件 `myemulator` (節點類型： `cq:Component`)。

1. 將屬 `sling:resourceSuperType` 性設為 `/libs/wcm/mobile/components/emulators/base`

1. 定義CSS用戶端程式庫，其中包含模 `cq.wcm.mobile.emulator` 擬器外觀的類別：name = `css`, node type = `cq:ClientLibrary`

   例如，您可以參考節點 `/libs/wcm/mobile/components/emulators/iPhone/css`

1. 如有需要，請定義JS用戶端程式庫，例如定義特定外掛程式：name = js,node type = cq:ClientLibrary

   例如，您可以參考節點 `/libs/wcm/mobile/components/emulators/base/js`

1. 如果模擬器支援外掛程式定義的特定功能（如觸控捲動），請在模擬器下建立設定節點：name = `cq:emulatorConfig`, node type = `nt:unstructured` and add the property that defines plugin:

   * 名稱= `canRotate`，類型= `Boolean`，值= `true`:以包含旋轉功能。

   * 名稱= `touchScrolling`，類型= `Boolean`，值= `true`:加入觸控捲動功能。
   您可定義自己的外掛程式，以新增更多功能。

