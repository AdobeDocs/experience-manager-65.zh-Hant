---
title: 最適化範本演算
seo-title: 最適化範本演算
description: 'null'
seo-description: 'null'
uuid: 97226ae1-e42a-40ae-a5e0-886cd77559d8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f5cb0e98-0d6e-4f14-9b94-df1a9d8cbe5b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---


# 最適化範本演算{#adaptive-template-rendering}

自適應範本演算提供管理含變化之頁面的方式。 這項功能原本適用於為行動裝置提供各種HTML輸出（例如功能手機與智慧型手機），當體驗必須傳送至需要不同標籤或HTML輸出的各種裝置時，這項功能十分有用。

## 概覽 {#overview}

範本通常以回應式格線為基礎，而根據這些範本建立的頁面則完全回應，可自動調整至用戶端裝置的檢視區。 使用頁面編輯器中的「模擬器」工具列，作者可將版面定位至特定裝置。

您也可以設定範本，以支援自適應轉換。 當裝置群組已正確設定時，當在模擬器模式中選取裝置時，頁面會在URL中以不同的選擇器呈現。 使用選取器，可透過URL直接呼叫特定頁面演算。

設定裝置群組時請記住：

* 每個設備必須至少位於一個設備組中。
* 一個設備可以是多個設備組。
* 由於裝置可以位於多個裝置群組中，因此可以結合選擇器。
* 選擇器的組合會由上到下評估，因為它們保存在儲存庫中。

>[!NOTE]
>
>裝置群組&#x200B;**回應式裝置**&#x200B;將不會有選擇器，因為已辨識為支援回應式設計的裝置會假設不需要最適化版面

## 設定 {#configuration}

可為現有設備組或您自己建立的[組配置自適應渲染選擇器。](/help/sites-developing/mobile.md#device-groups)

在此範例中，我們將設定現有的裝置群組&#x200B;**智慧型手機**，在We.Retail的&#x200B;**體驗頁面**&#x200B;範本中提供最適化演算選擇器。

1. 在`http://localhost:4502/miscadmin#/etc/mobile/groups`中編輯需要自適應選擇器的設備組

   設定&#x200B;**禁用模擬器**&#x200B;選項並保存。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 選擇器將可用於&#x200B;**Blackberry**&#x200B;和&#x200B;**iPhone 4**，前提是在以下步驟中將設備組&#x200B;**智慧電話**&#x200B;添加到模板和頁結構中。

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. 使用CRX DE Lite，將設備組添加到模板結構上的多值字串屬性`cq:deviceGroups`中，以允許在模板上使用設備組。

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   例如，如果我們要添加智慧電話設備組：

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. 使用CRX DE Lite，將裝置群組新增至網站結構上的多值字串屬性`cq:deviceGroups`，讓裝置群組可用於您的網站。

   `/content/<your-site>/jcr:content`

   例如，如果我們要允許&#x200B;**智慧電話**&#x200B;設備組：

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

現在，當在頁面編輯器中使用[emulator](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints)（例如[修改版面](/help/sites-authoring/responsive-layout.md)時）並選擇已設定裝置群組的裝置時，頁面會以選擇器呈現為URL的一部分。

在我們的範例中，當根據&#x200B;**Experience Page**&#x200B;範本編輯頁面，並在模擬器中選擇iPhone 4時，會將頁面呈現為包含選擇器的`arctic-surfing-in-lofoten.smart.html`而非`arctic-surfing-in-lofoten.html`

您也可以使用此選擇器直接呼叫頁面。

![chlimage_1-161](assets/chlimage_1-161.png)

