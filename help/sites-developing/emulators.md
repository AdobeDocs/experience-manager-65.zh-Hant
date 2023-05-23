---
title: 模擬器
seo-title: Emulators
description: AEM使作者能夠在模擬最終用戶將在其中查看頁面的環境的模擬器中查看頁面
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
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

Adobe Experience Manager(AEM)使作者能夠在模擬器中查看頁面，該模擬器模擬最終用戶將在其中查看頁面的環境，例如在移動設備或電子郵件客戶端中。

模擬AEM器框架：

* 在模擬用戶介面(UI)（例如移動設備或電子郵件客戶端）中提供內容創作（用於編寫新聞稿）。
* 根據模擬的UI調整頁面內容。
* 允許建立自定義模擬器。

>[!CAUTION]
>
>此功能僅在經典UI中受支援。

## 模擬器特性 {#emulators-characteristics}

模擬器：

* 基於ExtJS。
* 在頁面DOM上操作。
* 其外觀通過CSS進行調節。
* 支援插件（例如移動設備旋轉插件）。
* 僅對作者處於活動狀態。
* 其基本部件在 `/libs/wcm/emulator/components/base`。

### 模擬器如何轉換內容 {#how-the-emulator-transforms-the-content}

模擬器工作方式是將HTML體內容包裝到模擬器DIV中。 例如，以下html代碼：

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

在模擬器啟動後轉換為以下html代碼：

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

添加了兩個div標籤：

* id為的div `cq-emulator` 將模擬器作為一個整體

* id為的div `cq-emulator-content` 表示設備的視區/螢幕/內容區域，頁面內容位於該區域。

新的CSS類也分配給新的模擬器目錄：它們表示當前模擬器的名稱。

模擬器的插件可以進一步擴展已分配的CSS類清單，如旋轉插件的示例，根據當前設備旋轉插入「垂直」或「水準」類。

這樣，通過使CSS類與模擬器ID和CSS類對應，可以控制模擬器的完整外觀。

>[!NOTE]
>
>建議項目HTML將正文內容包裝在單個div中，如上例所示。 如果正文內容包含多個標籤，則可能會產生不可預知的結果。

### 移動模擬器 {#mobile-emulators}

現有的移動模擬器：

* 位於/libs/wcm/mobile/components/emulators下。
* 可通過JSON servlet獲得，地址為：

   http://localhost:4502/bin/wcm/mobile/emulators.json

當頁面元件依賴於移動頁面元件( `/libs/wcm/mobile/components/page`)，模擬器功能通過以下機制自動整合到頁面中：

* 移動頁面元件 `head.jsp` 包括設備組的關聯模擬器init元件（僅在作者模式下）和設備組的呈現CSS，通過：

   `deviceGroup.drawHead(pageContext);`

* 方法 `DeviceGroup.drawHead(pageContext)` 包括模擬器的init元件，即調用 `init.html.jsp` 模擬器元件。 如果模擬器元件沒有其自己的 `init.html.jsp` 並依賴移動基本模擬器( `wcm/mobile/components/emulators/base)`，調用mobile base模擬器的init指令碼( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`)。

* 移動基本模擬器的init指令碼通過Javascript定義：

   * 為頁定義的所有模擬器的配置(emulatorConfigs)
   * 通過以下方式將模擬器功能整合到頁面中的模擬器管理器：

      `emulatorMgr.launch(config)`;

      模擬器管理器由以下定義：

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### 建立自定義移動模擬器 {#creating-a-custom-mobile-emulator}

要建立自定義移動模擬器：

1. 下 `/apps/myapp/components/emulators` 建立元件 `myemulator` （節點類型） `cq:Component`)。

1. 設定 `sling:resourceSuperType` 屬性 `/libs/wcm/mobile/components/emulators/base`

1. 定義具有類別的CSS客戶端庫 `cq.wcm.mobile.emulator` 模擬器外觀：名稱= `css`，節點類型= `cq:ClientLibrary`

   例如，可以引用節點 `/libs/wcm/mobile/components/emulators/iPhone/css`

1. 如果需要，定義JS客戶端庫，例如定義特定插件：名稱= js，節點類型= cq:ClientLibrary

   例如，可以引用節點 `/libs/wcm/mobile/components/emulators/base/js`

1. 如果模擬器支援由插件定義的特定功能（如觸摸滾動），請在模擬器下面建立一個配置節點：名稱= `cq:emulatorConfig`，節點類型= `nt:unstructured` 並添加定義插件的屬性：

   * 名稱= `canRotate`，類型= `Boolean`，值= `true`:包含旋轉功能。

   * 名稱= `touchScrolling`，類型= `Boolean`，值= `true`:包括觸摸滾動功能。
   可以通過定義自己的插件來添加更多功能。
