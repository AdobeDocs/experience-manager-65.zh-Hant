---
title: 模擬器
description: AEM可讓作者在模擬一般使用者檢視頁面環境的模擬器中檢視頁面
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# 模擬器{#emulators}

{{ue-over-mobile}}

Adobe Experience Manager (AEM)可讓作者在模擬一般使用者檢視頁面環境的模擬器中，檢視頁面，例如在行動裝置或電子郵件使用者端中。

AEM模擬器架構：

* 在模擬使用者介面(UI)中提供內容製作，例如行動裝置或電子郵件使用者端（用於製作電子報）。
* 根據模擬的UI調整頁面內容。
* 允許建立自訂模擬器。

>[!CAUTION]
>
>此功能僅支援傳統UI。

## 模擬器特性 {#emulators-characteristics}

模擬器：

* 是以ExtJS為基礎。
* 在頁面DOM上運作。
* 其外觀會透過CSS受到規範。
* 支援外掛程式（例如行動裝置旋轉外掛程式）。
* 僅對作者有效。
* 其基底元件位於`/libs/wcm/emulator/components/base`。

### 模擬器如何轉換內容 {#how-the-emulator-transforms-the-content}

模擬器的運作方式是將HTML內文內容包裝到模擬器DIV中。 例如，下列html程式碼：

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

* ID為`cq-emulator`的div將模擬器作為整體保留，並且

* 識別碼為`cq-emulator-content`的div，代表頁面內容所在的裝置檢視區/畫面/內容區域。

新的CSS類別也會指派給新的模擬器div：它們代表目前模擬器的名稱。

模擬器的外掛程式可能會進一步擴充指派的CSS類別清單，如旋轉外掛程式的範例，根據目前的裝置旋轉插入「垂直」或「水準」類別。

如此一來，可藉由具有與模擬器div的ID和CSS類別相對應的CSS類別，來控制模擬器的完整外觀。

>[!NOTE]
>
>建議專案HTML將內文內容包裝在單一div中，就像上面的範例一樣。 如果內文內容包含多個標籤，可能會出現無法預測的結果。

### 行動模擬器 {#mobile-emulators}

現有的行動模擬器：

* 在/libs/wcm/mobile/components/emulator之下。
* 可透過JSON servlet在以下網址取得：

  http://localhost:4502/bin/wcm/mobile/emulators.json

當頁面元件需仰賴行動頁面元件( `/libs/wcm/mobile/components/page`)時，模擬器功能會透過下列機制自動整合到頁面中：

* 行動頁面元件`head.jsp`包含裝置群組相關的模擬器初始化元件（僅於作者模式下）以及裝置群組的轉譯CSS，透過：

  `deviceGroup.drawHead(pageContext);`

* 方法`DeviceGroup.drawHead(pageContext)`包含模擬器的init元件，也就是呼叫模擬器元件的`init.html.jsp`。 如果模擬器元件沒有自己的`init.html.jsp`且依賴行動基底模擬器( `wcm/mobile/components/emulators/base)`)，則行動基底模擬器的init指令碼稱為( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`)。

* 行動基本模擬器的初始指令碼透過JavaScript定義：

   * 為頁面定義的所有模擬器的設定(emulatorConfigs)
   * 模擬器管理員透過以下方式整合頁面中的模擬器功能：

     `emulatorMgr.launch(config)`；

     模擬器管理員的定義如下：

     `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### 建立自訂行動模擬器 {#creating-a-custom-mobile-emulator}

若要建立自訂行動模擬器：

1. 在`/apps/myapp/components/emulators`底下建立元件`myemulator` （節點型別： `cq:Component`）。

1. 將`sling:resourceSuperType`屬性設定為`/libs/wcm/mobile/components/emulators/base`

1. 為模擬器外觀定義類別為`cq.wcm.mobile.emulator`的CSS使用者端資料庫：名稱= `css`，節點型別= `cq:ClientLibrary`

   例如，您可以參照節點`/libs/wcm/mobile/components/emulators/iPhone/css`

1. 如有需要，請定義JS使用者端程式庫，以定義特定外掛程式：名稱= js，節點型別= cq：ClientLibrary

   例如，您可以參照節點`/libs/wcm/mobile/components/emulators/base/js`

1. 如果模擬器支援外掛程式定義的特定功能（例如觸控捲動），請在模擬器下方建立設定節點：名稱= `cq:emulatorConfig`、節點型別= `nt:unstructured`，然後新增定義外掛程式的屬性：

   * 名稱= `canRotate`，型別= `Boolean`，值= `true`：包含旋轉功能。

   * 名稱= `touchScrolling`，型別= `Boolean`，值= `true`：包含觸控捲動功能。

   您可以定義自己的外掛程式，以新增更多功能。
