---
title: 最適化範本轉譯
seo-title: 最適化範本轉譯
description: 最適化範本轉譯
seo-description: 'null'
uuid: 97226ae1-e42a-40ae-a5e0-886cd77559d8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f5cb0e98-0d6e-4f14-9b94-df1a9d8cbe5b
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# 適用性範本轉譯{#adaptive-template-rendering}

最適化範本轉譯提供管理含有變異之頁面的方法。 此功能原本可用來為行動裝置傳送各種HTML輸出（例如功能電話與智慧電話），但當體驗必須傳送至需要不同標籤或HTML輸出的各種裝置時，此功能就十分實用。

## 概覽 {#overview}

範本通常以回應式格線為基礎建置，而根據這些範本建立的頁面完全回應，會自動調整至用戶端裝置的檢視區。 使用頁面編輯器中的「模擬器」工具列，作者可以將佈局目標定位到特定設備。

您也可以設定範本以支援最適化轉譯。 在模擬器模式中選取裝置時，正確設定裝置群組時，頁面會以URL中的不同選取器呈現。 使用選取器可以透過URL直接呼叫特定頁面呈現。

設定裝置群組時請記住：

* 每個設備必須至少位於一個設備組中。
* 一個設備可以位於多個設備組中。
* 因為裝置可以位於多個裝置群組中，所以可以結合選取器。
* 選取器組合會由上到下評估，因為它們會保存在存放庫中。

>[!NOTE]
>
>裝置群組&#x200B;**回應式裝置**&#x200B;永遠不會有選取器，因為已識別為支援回應式設計的裝置假設不需要最適化版面

## 設定 {#configuration}

可針對現有裝置群組或您自行建立的[群組，設定最適化轉譯選取器。](/help/sites-developing/mobile.md#device-groups)

在此範例中，我們將設定現有裝置群組&#x200B;**智慧型電話**，以在We.Retail的&#x200B;**體驗頁面**&#x200B;範本中提供最適化轉譯選取器。

1. 編輯`http://localhost:4502/miscadmin#/etc/mobile/groups`中需要自適應選擇器的設備組

   設定選項&#x200B;**禁用模擬器**&#x200B;並保存。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 如果以下步驟將設備組&#x200B;**智慧手機**&#x200B;添加到模板和頁面結構中，則此選擇器將可用於&#x200B;**Blackberry**&#x200B;和&#x200B;**iPhone 4**。

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. 使用CRX DE Lite，將裝置群組新增至範本結構上的多值字串屬性`cq:deviceGroups`，以允許在範本上使用裝置群組。

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   例如，如果要添加智慧電話設備組：

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. 使用CRX DE Lite，將裝置群組新增至網站結構上的多值字串屬性`cq:deviceGroups`，以允許在您的網站上使用裝置群組。

   `/content/<your-site>/jcr:content`

   例如，如果要允許&#x200B;**智慧電話**&#x200B;設備組：

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

現在，在頁面編輯器中使用[emulator](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints)時（例如當[修改版面](/help/sites-authoring/responsive-layout.md)時），當您選擇已設定裝置群組的裝置時，頁面會呈現為URL中的選取器。

在我們的範例中，根據&#x200B;**體驗頁面**&#x200B;範本編輯頁面，並在模擬器中選擇iPhone 4時，會將頁面呈現為`arctic-surfing-in-lofoten.smart.html`，而非`arctic-surfing-in-lofoten.html`選取器

也可以使用此選取器直接呼叫頁面。

![chlimage_1-161](assets/chlimage_1-161.png)
