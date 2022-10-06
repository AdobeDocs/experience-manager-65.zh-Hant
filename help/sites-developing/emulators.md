---
title: 模擬器
seo-title: Emulators
description: AEM可讓作者在模擬一般使用者將檢視頁面之環境的模擬器中檢視頁面
seo-description: AEM enables authors to view a page in an emulator that simulates the environment in which an end-user will view the page
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# 模擬器{#emulators}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

Adobe Experience Manager(AEM)可讓作者在模擬一般使用者將檢視頁面的環境（例如行動裝置或電子郵件用戶端）中，檢視模擬器中的頁面。

AEM模擬器架構：

* 在模擬的使用者介面(UI)中提供內容編寫，例如行動裝置或電子郵件用戶端（用來編寫電子報）。
* 根據模擬的UI調整頁面內容。
* 允許建立自定義模擬器。

>[!CAUTION]
>
>只有傳統UI才支援此功能。

## 模擬器特性 {#emulators-characteristics}

模擬器：

* 以ExtJS為基礎。
* 在頁面DOM上運作。
* 其外觀會透過CSS進行規範。
* 支援外掛程式（例如行動裝置旋轉外掛程式）。
* 僅對作者作用中。
* 其基本元件位於 `/libs/wcm/emulator/components/base`.

### 模擬器如何轉換內容 {#how-the-emulator-transforms-the-content}

模擬器的運作方式是將HTML內容包裝到模擬器DIV中。 例如，下列html程式碼：

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

在模擬器啟動後，會轉換為下列html程式碼：

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

* 具有id的div `cq-emulator` 將模擬器整體保持在

* 具有id的div `cq-emulator-content` 代表頁面內容所在裝置的檢視區/畫面/內容區域。

新的CSS類還分配給新的模擬器div:它們表示當前模擬器的名稱。

模擬器的插件可以進一步擴展已分配的CSS類的清單，如旋轉插件的示例所示，根據當前設備旋轉插入「垂直」或「水準」類。

這樣，可以通過具有與模擬器div的ID和CSS類對應的CSS類來控制模擬器的完整外觀。

>[!NOTE]
>
>建議專案HTML以單一div包裝內文，如上例所示。 如果內文內容包含多個標籤，可能會產生無法預測的結果。

### 行動模擬器 {#mobile-emulators}

現有的移動模擬器：

* 位於/libs/wcm/mobile/components/emulators之下。
* 可透過JSON servlet取得：

   http://localhost:4502/bin/wcm/mobile/emulators.json

頁面元件需仰賴行動頁面元件時( `/libs/wcm/mobile/components/page`)，則模擬器功能會透過下列機制自動整合至頁面中：

* 行動頁面元件 `head.jsp` 包括設備組的關聯模擬器init元件（僅在製作模式中），以及設備組通過以下方式呈現CSS:

   `deviceGroup.drawHead(pageContext);`

* 方法 `DeviceGroup.drawHead(pageContext)` 包括模擬器的init元件，即調用 `init.html.jsp` 模擬器元件。 如果模擬器元件沒有自己的元件 `init.html.jsp` 並依賴行動基本模擬器( `wcm/mobile/components/emulators/base)`，則會呼叫行動基本模擬器的init指令碼( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`)。

* 行動基本模擬器的init指令碼透過Javascript定義：

   * 為頁面定義的所有模擬器的配置(emulatorConfigs)
   * 模擬器管理器通過以下方式整合了頁面中模擬器的功能：

      `emulatorMgr.launch(config)`;

      模擬器管理器由以下項定義：

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### 建立自訂行動模擬器 {#creating-a-custom-mobile-emulator}

若要建立自訂行動模擬器：

1. 在下 `/apps/myapp/components/emulators` 建立元件 `myemulator` （節點類型） `cq:Component`)。

1. 設定 `sling:resourceSuperType` 屬性 `/libs/wcm/mobile/components/emulators/base`

1. 使用類別定義CSS用戶端程式庫 `cq.wcm.mobile.emulator` 模擬器外觀：name = `css`，節點類型= `cq:ClientLibrary`

   例如，您可以參照節點 `/libs/wcm/mobile/components/emulators/iPhone/css`

1. 如有需要，請定義JS用戶端資料庫，例如定義特定外掛程式：name = js,node type = cq:ClientLibrary

   例如，您可以參照節點 `/libs/wcm/mobile/components/emulators/base/js`

1. 如果模擬器支援由外掛程式定義的特定功能（如觸控式捲動），請在模擬器下方建立設定節點：name = `cq:emulatorConfig`，節點類型= `nt:unstructured` 並新增定義外掛程式的屬性：

   * 名稱= `canRotate`，類型= `Boolean`，值= `true`:以包含旋轉功能。

   * 名稱= `touchScrolling`，類型= `Boolean`，值= `true`:以包含觸控捲動功能。
   您可以定義自己的外掛程式，以新增更多功能。
