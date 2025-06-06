---
title: 將體驗片段匯出到 Adobe Target
description: 瞭解如何將Adobe Experience Manager (AEM)體驗片段匯出至Adobe Target。
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: dcb55b3b185fe5dccf52377a12556e33d818e410
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 1%

---

# 將體驗片段匯出到 Adobe Target{#exporting-experience-fragments-to-adobe-target}

您可以將在Adobe Experience Manager (AEM)中建立的[體驗片段](/help/sites-authoring/experience-fragments.md)匯出至Adobe Target (Target)。 接著，可將這些選件做為Target活動中的選件，以大規模測試並個人化體驗。

有三個格式選項可用於將體驗片段匯出至Adobe Target：

* HTML（預設）：支援網頁和混合式內容傳遞
* JSON：支援Headless內容傳送
* HTML 和 JSON

AEM體驗片段可以匯出至Adobe Target中的預設工作區，或匯出至Adobe Target的使用者定義工作區。 這是使用Adobe Developer Console完成的，對此，AEM必須使用IMS[&#128279;](/help/sites-administering/setting-up-ims-integrations-for-aem.md)與Adobe Target 整合。

>[!NOTE]
>
>[IMS整合現在已設定為S2S OAuth](/help/sites-administering/setting-up-ims-integrations-for-aem.md)。
>
>先前是使用[JWT認證進行設定，而現在Adobe Developer Console](/help/sites-administering/jwt-credentials-deprecation-in-adobe-developer-console.md)已棄用。

>[!NOTE]
>
>Adobe Target本身並不存在Adobe Target工作區。 它們是在Adobe IMS (Identity Management系統)中定義和管理，然後使用Adobe Developer Console中的整合選取以供跨解決方案使用。

>[!NOTE]
>
>Adobe Target工作區可用來允許組織（群組）的成員僅針對此組織建立和管理優惠方案及活動，不將存取權授予其他使用者。 例如，全球關注的國家/地區特定組織。

>[!NOTE]
>
>如需進一步資訊，另請參閱：
>
>* [Adobe Target開發](https://developers.adobetarget.com/)
>* [核心元件 — 體驗片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/experience-fragment.html?lang=zh-Hant)
>

## 先決條件 {#prerequisites}

需要執行各種動作：

1. 您必須使用IMS[&#128279;](/help/sites-administering/setting-up-ims-integrations-for-aem.md) 整合AEM與Adobe Target。

   >[!NOTE]
   >
   >[IMS整合現在已設定為S2S OAut](/help/sites-administering/setting-up-ims-integrations-for-aem.md)。
   >
   >先前是使用[JWT認證進行設定，而現在Adobe Developer Console](/help/sites-administering/jwt-credentials-deprecation-in-adobe-developer-console.md)已棄用。

1. 體驗片段會從AEM編寫執行個體匯出，因此您必須在編寫執行個體上[設定AEM連結外部化程式](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)，以確保體驗片段中的任何參考都會外部化以供Web傳遞。

   >[!NOTE]
   >
   >對於預設未涵蓋的連結重寫，[體驗片段連結重寫器提供者](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html)可供使用。 如此一來，您就可以針對執行個體開發自訂規則。

## 新增雲端設定 {#add-the-cloud-configuration}

在匯出片段之前，您必須將&#x200B;**Adobe Target**&#x200B;的&#x200B;**雲端設定**&#x200B;新增到片段或資料夾。 這也可讓您：

* 指定要用於匯出的格式選項
* 選取Target工作區作為目的地
* 選取外部化器網域，以重寫體驗片段中的參照（選用）

可以在必要資料夾和/或片段的&#x200B;**頁面屬性**&#x200B;中選取必要選項；必要時將繼承規格。

1. 導覽至&#x200B;**體驗片段**&#x200B;主控台。

1. 開啟適當資料夾或片段的&#x200B;**頁面屬性**。

   >[!NOTE]
   >
   >如果您將雲端設定新增至體驗片段父資料夾，設定將由所有子系繼承。
   >
   >
   >如果您將雲端設定新增至體驗片段本身，該設定會由所有變數繼承。

1. 選取「**雲端服務**」標籤。

1. 在&#x200B;**Cloud Service設定**&#x200B;下，從下拉式清單中選取&#x200B;**Adobe Target**。

   >[!NOTE]
   >
   >可自訂體驗片段選件的JSON格式。 若要這麼做，請定義客戶體驗片段元件，然後註明如何在元件Sling模型中匯出其屬性。
   >
   >請參閱核心元件：
   >
   >[核心元件 — 體驗片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/experience-fragment.html?lang=zh-Hant)

   在&#x200B;**Adobe Target**&#x200B;下選取：

   * 適當的設定
   * 所需的格式選項
   * Adobe Target工作區
   * 如有必要 — Externalizer網域

   >[!CAUTION]
   >
   >Externalizer網域是選用的。
   >
   >當您想要匯出的內容指向特定的&#x200B;*發佈*&#x200B;網域時，會設定AEM Externalizer。 如需詳細資訊，請參閱[設定AEM連結外部器](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)。
   >
   >另請注意，外部化器網域僅與傳送至Target的體驗片段內容相關，與檢視選件內容之類的中繼資料無關。

   例如，針對資料夾：

   ![資料夾 — Cloud Service](assets/xf-target-integration-01.png "資料夾 — Cloud Service")

1. **儲存並關閉**。

## 將體驗片段匯出至Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>對於媒體資產（例如影像），只會將參考匯出至Target。 資產本身仍會儲存在AEM Assets中，並從AEM發佈例項傳送。
>
>因此，在匯出至Target之前，必須發佈包含所有相關資產的體驗片段。

若要將體驗片段從AEM匯出至Target （在指定雲端設定後）：

1. 導覽至體驗片段主控台。
1. 選取您要匯出至Target的體驗片段。

   >[!NOTE]
   >
   >它必須是體驗片段Web變數。

1. 按一下&#x200B;**匯出至Adobe Target**。

   >[!NOTE]
   >
   >如果體驗片段已匯出，請選取「在Adobe Target中更新」**&#x200B;**。

1. 視需要按一下&#x200B;**匯出而不發佈**&#x200B;或&#x200B;**Publish**。

   >[!NOTE]
   >
   >選取&#x200B;**Publish**&#x200B;會立即發佈體驗片段並將其傳送到Target。

1. 在確認對話方塊中按一下&#x200B;**確定**。

   您的體驗片段現在應該在Target中。

   >[!NOTE]
   >
   >[匯出的各種詳細資料](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment)可在主控台的&#x200B;**清單檢視**&#x200B;和&#x200B;**內容**&#x200B;中看見。

   >[!NOTE]
   >
   >在Adobe Target中檢視體驗片段時，看到的&#x200B;*上次修改*&#x200B;日期是上次在AEM中修改片段的日期，而非上次將片段匯出至Adobe Target的日期。

>[!NOTE]
>
>或者，您可以使用[頁面資訊](/help/sites-authoring/author-environment-tools.md#page-information)功能表中的類似命令，從頁面編輯器執行匯出。

## 在Adobe Target中使用您的體驗片段 {#using-your-experience-fragments-in-adobe-target}

執行先前的工作後，體驗片段會顯示在Adobe Target的「選件」頁面中。 檢視[特定Target檔案](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=zh-Hant)以瞭解您可以達成的目標。

>[!NOTE]
>
>在Adobe Target中檢視體驗片段時，看到的&#x200B;*上次修改*&#x200B;日期是上次在AEM中修改片段的日期，而非上次將片段匯出至Adobe Target的日期。

## 刪除已匯出至Adobe Target的體驗片段 {#deleting-an-experience-fragment-already-exported-to-adobe-target}

刪除已匯出至Target的體驗片段，如果片段已在Adobe Target的選件中使用，可能會造成問題。 刪除片段會導致選件無法使用，因為AEM正在傳遞片段內容。

若要避免此類情況：

* 如果體驗片段目前未用於活動中，AEM可讓使用者刪除片段而不顯示警告訊息。
* 如果Adobe Target中的活動使用體驗片段，則會出現錯誤訊息，警告AEM使用者刪除片段對活動可能造成的後果。

  AEM中的錯誤訊息不會禁止使用者（強制）刪除體驗片段。 如果刪除體驗片段：

   * 具有AEM體驗片段的Target選件可能會顯示不良行為

      * 由於體驗片段HTML已推送至Target，因此該選件很可能仍會呈現
      * 如果也在AEM中刪除了參照的資產，體驗片段中的任何參照都無法正常運作。

   * 由於體驗片段在AEM中不再存在，因此無法對體驗片段進行任何進一步的修改。


## 從匯出至Target的體驗片段中移除ClientLibs {#removing-clientlibs-from-fragments-exported-target}

體驗片段包含完整的html標籤和所有必要的使用者端資料庫(CSS/JS)，以便呈現與體驗片段內容作者建立的片段完全相同的片段。 這是客製化設計。

在AEM所傳送的頁面上搭配Adobe Target使用體驗片段選件時，「鎖定目標」頁面已包含所有必要的使用者端資料庫。 此外，體驗片段選件中也不需要多餘的html （請參閱[考量事項](#considerations)）。

以下是體驗片段選件中html的偽範例：

```html
<!DOCTYPE>
<html>
   <head>
      <title>…</title>
      <!-- all the client libraries (css/js) -->
      …
   </head>
   <body>
        <!--/* Actual XF Offer content would appear here... */-->
   </body>
</html>
```

概言之，當AEM將體驗片段匯出至Adobe Target時，它會使用數個額外的Sling選取器來執行此操作。 例如，匯出的體驗片段的URL可能如下所示（注意`nocloudconfigs.atoffer`）：

* http://www.your-aem-instance.com/content/experience-fragments/my-offers/my-xf-offer.nocloudconfigs.atoffer.html

`nocloudconfigs`選擇器是使用HTL定義的，而且可以從以下位置複製以覆蓋：

* /libs/cq/experience-fragments/components/xfpage/nocloudconfigs.html

`atoffer`選擇器已使用[Sling重寫程式](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html)套用後續處理。 兩者皆可用來移除使用者端程式庫。

### 範例 {#example}

在此說明如何使用`nocloudconfigs`執行此操作。

>[!NOTE]
>
>如需詳細資訊，請參閱[可編輯的範本](/help/sites-developing/templates.md#editable-templates)。

#### 覆蓋 {#overlays}

在此特定範例中，包含的[重疊](/help/sites-developing/overlays.md)將會移除使用者端資料庫&#x200B;*和*&#x200B;多餘的HTML。 我們假設您已建立體驗片段範本型別。 需要從`/libs/cq/experience-fragments/components/xfpage/`複製的必要檔案包括：

* `nocloudconfigs.html`
* `head.nocloudconfigs.html`
* `body.nocloudconfigs.html`

#### 範本型別覆蓋圖 {#template-type-overlays}

在此範例中，讓我們使用下列結構：

![範本型別覆蓋圖](assets/xf-target-integration-02.png "範本型別覆蓋圖")

這些檔案的內容如下：

* `body.nocloudconfigs.html`

  ![body.nocloudconfigs.html](assets/xf-target-integration-03.png "body.nocloudconfigs.html")

* `head.nocloudconfigs.html`

  ![head.nocloudconfigs.html](assets/xf-target-integration-04.png "head.nocloudconfigs.html")

* `nocloudconfigs.html`

  ![nocloudconfigs.html](assets/xf-target-integration-05.png "nocloudconfigs.html")

>[!NOTE]
>
>若要使用`data-sly-unwrap`移除內文標籤，您需要`nocloudconfigs.html`。

### 考量事項 {#considerations}

如果您需要使用Adobe Target中的體驗片段選件支援AEM網站和非AEM網站，您必須建立兩個體驗片段（兩種不同的範本型別）：

* 具有覆蓋以移除clientlibs/額外html的元件

* 沒有覆蓋的網域，因此包含必要的clientlibs