---
title: 最適化範本演算
description: 瞭解Adobe Experience Manager中的調適型範本演算。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 2%

---

# 最適化範本演算{#adaptive-template-rendering}

最適化範本演算提供管理變異頁面的方法。 此功能原本很適合用於為行動裝置提供各種HTML輸出（例如功能手機與智慧型手機），但在需要將體驗提供給需要不同標籤或HTML輸出的各種裝置時，此功能會很有用。

## 概觀 {#overview}

範本是圍繞回應式格線建立，根據這些範本建立的頁面會完全回應式，並自動調整至使用者端裝置的檢視區。 作者可使用頁面編輯器中的模擬器工具列，將配置鎖定在特定裝置。

也可以設定範本以支援最適化轉譯。 若裝置群組已正確設定，則在模擬器模式下選取裝置時，頁面會以URL中的不同選取器呈現。 使用選取器，可以透過URL直接呼叫特定頁面呈現。

設定裝置群組時請記住：

* 每個裝置至少必須位於一個裝置群組中。
* 一個裝置可以位於多個裝置群組中。
* 由於裝置可以位於多個裝置群組中，因此可組合選取器。
* 系統會從上到下評估選取器組合，因為系統會將它們儲存在存放庫中。

>[!NOTE]
>
>裝置群組**回應式裝置永遠沒有選擇器，因為系統假設被辨識為支援回應式設計的裝置不需要最適化配置

## 設定 {#configuration}

您可以為現有的裝置群組或您自己建立的[群組設定最適化演算選取器。](/help/sites-developing/mobile.md#device-groups)

在此範例中，您即將設定現有的裝置群組&#x200B;**智慧型手機**，使其具備最適化轉譯選擇器，作為We.Retail中&#x200B;**體驗頁面**&#x200B;範本的一部分。

1. 在`http://localhost:4502/miscadmin#/etc/mobile/groups`中編輯需要最適化選擇器的裝置群組

   設定選項&#x200B;**停用模擬器**&#x200B;並儲存。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 選取器可用於&#x200B;**BlackBerry®**&#x200B;和&#x200B;**iPhone 4**，前提是裝置群組&#x200B;**智慧型手機**&#x200B;已新增至範本和頁面結構，請依下列步驟執行。

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. 使用CRXDE Lite，將裝置群組新增至範本結構上的多值字串屬性`cq:deviceGroups`，讓裝置群組可用於範本。

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   例如，如果您要新增Smartphone裝置群組：

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. 使用CRXDE Lite，將裝置群組新增至網站結構上的多值字串屬性`cq:deviceGroups`，允許裝置群組在您的網站上使用。

   `/content/<your-site>/jcr:content`

   例如，如果您要允許&#x200B;**智慧型手機**&#x200B;裝置群組：

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

現在，在頁面編輯器中使用[模擬器](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints)時（例如[修改版面](/help/sites-authoring/responsive-layout.md)），當您選擇已設定裝置群組的裝置時，頁面會在URL中透過選取器呈現。

在此範例中，當根據&#x200B;**體驗頁面**&#x200B;範本編輯頁面，並在模擬器中選擇iPhone 4時，包含選取器的頁面呈現為`arctic-surfing-in-lofoten.smart.html`，而不是`arctic-surfing-in-lofoten.html`

也可以使用此選取器直接呼叫頁面。

![chlimage_1-161](assets/chlimage_1-161.png)
