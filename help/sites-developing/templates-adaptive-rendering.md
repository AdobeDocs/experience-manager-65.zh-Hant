---
title: 自適應模板渲染
seo-title: Adaptive Template Rendering
description: 自適應模板渲染
seo-description: null
uuid: 97226ae1-e42a-40ae-a5e0-886cd77559d8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f5cb0e98-0d6e-4f14-9b94-df1a9d8cbe5b
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# 自適應模板渲染{#adaptive-template-rendering}

自適應模板渲染提供了一種管理具有變體的頁面的方法。 該功能最初可用於為移動設備（例如功能電話與智慧電話）提供各種HTML輸出，當需要不同標籤或HTML輸出的不同設備必須提供體驗時，該功能非常有用。

## 概觀 {#overview}

模板通常圍繞響應的網格構建，並且基於這些模板建立的頁面是完全響應的，自動地調整到客戶端設備的視區。 使用頁面編輯器中的「模擬器」工具欄，作者可以將佈局目標定向到特定設備。

還可以設定模板以支援自適應渲染。 正確配置設備組後，在模擬器模式下選擇設備時，將使用URL中的其他選擇器呈現該頁。 使用選擇器，可以通過URL直接調用特定頁面呈現。

設定設備組時請記住：

* 每個設備必須至少位於一個設備組中。
* 一個設備可以位於多個設備組中。
* 由於設備可以位於多個設備組中，因此可以組合選擇器。
* 選擇器組合會由上到下計算，因為它們會保留在儲存庫中。

>[!NOTE]
>
>設備組 **響應設備** 永遠不會擁有選擇器，因為被認為支援響應設計的設備被認為不需要自適應佈局

## 設定 {#configuration}

可以為現有設備組或配置自適應呈現選擇器 [你自己建立的群。](/help/sites-developing/mobile.md#device-groups)

在本示例中，我們將配置現有設備組 **智慧手機** 將自適應渲染選擇器作為 **體驗頁** We.Retail中的模板。

1. 編輯在中需要自適應選擇器的設備組 `http://localhost:4502/miscadmin#/etc/mobile/groups`

   設定選項 **禁用模擬器** 然後保存。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 選擇器將可用於 **黑莓** 和 **iPhone4** 提供了設備組 **智慧手機** 將添加到模板和頁面結構中。

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. 使用CRX DE Lite，通過將設備組添加到多值字串屬性，允許在模板上使用設備組 `cq:deviceGroups` 的上界。

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   例如，如果要添加Smart Phone設備組：

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. 使用CRX DE Lite，通過將設備組添加到多值字串屬性中，允許在站點上使用設備組 `cq:deviceGroups` 你的網站結構。

   `/content/<your-site>/jcr:content`

   例如，如果我們希望 **智慧手機** 設備組：

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

現在使用 [模擬器](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) 在頁面編輯器中(例如 [修改佈局](/help/sites-authoring/responsive-layout.md))，然後您選擇已配置設備組的設備，將使用選擇器作為URL的一部分來呈現該頁。

在本例中，當根據 **體驗頁** 模板，在模擬器中選擇iPhone4，將顯示該頁，其中選擇器作為 `arctic-surfing-in-lofoten.smart.html` 而不是 `arctic-surfing-in-lofoten.html`

也可以使用此選擇器直接調用該頁。

![chlimage_1-161](assets/chlimage_1-161.png)
