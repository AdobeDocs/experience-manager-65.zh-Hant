---
title: 將體驗片段匯出到 Adobe Target
seo-title: Exporting Experience Fragments to Adobe Target
description: 將體驗片段匯出到 Adobe Target
seo-description: Exporting Experience Fragments to Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
source-git-commit: 88763b318e25efb16f61bc16530082877392c588
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 1%

---

# 將體驗片段匯出到 Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>本頁面的某些功能需要應用AEM 6.5.3.0（或更新版本）。
>
>6.5.3.0:
>
>* **Externalizer域** 現在可以選取。
   >  **注意：** 外部化程式網域僅與傳送至Target的體驗片段內容相關，而與檢視選件內容等中繼資料無關。
>
>6.5.2.0:
>
>* 體驗片段可匯出至：
   >
   >   * 預設工作區。
   >   * 在雲端設定中指定的已命名工作區。
   >   * **注意：** 匯出至特定工作區需有Adobe Target Premium。
>
>* AEM必須 [使用IMS與Adobe Target整合](/help/sites-administering/integration-target-ims.md).
>
>AEM 6.5.0.0和6.5.1.0:
>
>* AEM體驗片段會匯出至Adobe Target的預設工作區。
>* AEM必鬚根據 [與Adobe Target整合](/help/sites-administering/target.md).


您可以匯出 [體驗片段](/help/sites-authoring/experience-fragments.md)，在Adobe Experience Manager(AEM)中建立，到Adobe Target(Target)。 然後可在Target活動中作為選件，以大規模測試並個人化體驗。

有三種格式選項可用來匯出體驗片段至Adobe Target:

* HTML（預設）:支援網頁和混合式內容傳送
* JSON:支援無頭內容傳送
* HTML 和 JSON

AEM體驗片段可匯出至Adobe Target中的預設工作區，或匯出至Adobe Target的使用者定義工作區。 這是使用Adobe Developer Console完成，AEM必須 [使用IMS與Adobe Target整合](/help/sites-administering/integration-target-ims.md).

>[!NOTE]
>
>Adobe Target工作區不存在於Adobe Target本身。 這些範本會在Adobe IMS(Identity Management系統)中定義和管理，然後透過Adobe Developer主控台的整合，選取以用於各種解決方案。

>[!NOTE]
>
>Adobe Target工作區可用來允許組織（群組）的成員僅建立和管理此組織的選件和活動；而不授予其他使用者存取權。 例如，全球關注的特定國家組織。

>[!NOTE]
>
>如需詳細資訊，另請參閱：
>
>* [Adobe Target開發](https://www.adobe.io/apis/experiencecloud/target.html)
>* [核心元件 — 體驗片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)
>


## 必備條件 {#prerequisites}

>[!CAUTION]
>
>本頁面的某些功能需要應用AEM 6.5.3.0。

需要執行各種動作：

1. 你必須 [使用IMS將AEM與Adobe Target整合](/help/sites-administering/integration-target-ims.md).
2. 體驗片段會從AEM製作例項匯出，因此您需要 [設定AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) 在製作例項上，以確保體驗片段內的任何參考會外部化以用於網頁傳送。

   >[!NOTE]
   >
   >對於預設未涵蓋的連結重寫， [體驗片段連結重寫器提供者](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) 的URL區段。 借此，您可針對執行個體開發自訂規則。

## 新增雲端設定 {#add-the-cloud-configuration}

匯出片段之前，您需要新增 **雲端設定** for **Adobe Target** 至片段或資料夾。 這也可讓您：

* 指定要用於匯出的格式選項
* 選擇目標工作區作為目標
* 選取外部化程式網域，以重新寫入體驗片段中的參考（選用）

您可以在 **頁面屬性** 所需資料夾和/或片段；將視需要繼承規範。

1. 導覽至 **體驗片段** 控制台。

1. 開啟 **頁面屬性** ，以取得適當的資料夾或片段。

   >[!NOTE]
   >
   >如果您將雲端設定新增至體驗片段上層資料夾，設定會由所有子項繼承。
   >
   >
   >如果您將雲端設定新增至體驗片段本身，則設定會由所有變數繼承。

1. 選取 **Cloud Services** 標籤。

1. 在 **Cloud Service配置**，選取 **Adobe Target** 從下拉式清單中。

   >[!NOTE]
   >
   >體驗片段選件的JSON格式可自訂。 若要這麼做，請定義客戶體驗片段元件，然後註解如何在元件Sling模型中匯出其屬性。
   >
   >請參閱核心元件：
   >
   >[核心元件 — 體驗片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)

   在 **Adobe Target** 選擇：

   * 適當的配置
   * 所需格式選項
   * Adobe Target工作區
   * 如有必要 — externalizer域

   >[!CAUTION]
   >
   >外部化程式域是可選的。
   >
   >當您希望匯出的內容指向特定 *發佈* 網域。 如需更多詳細資訊，請參閱 [設定AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer).
   >
   >另請注意，外部化程式網域僅與傳送至Target的體驗片段內容相關，而與檢視選件內容等中繼資料無關。

   例如，對於資料夾：

   ![資料夾 — Cloud Services](assets/xf-target-integration-01.png "資料夾 — Cloud Services")

1. **儲存並關閉**.

## 將體驗片段匯出至Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>若為媒體資產（例如影像），則只會將參考匯出至Target。 資產本身會保存在AEM Assets中，並從AEM發佈例項傳送。
>
>因此，匯出至Target之前，必須先發佈體驗片段及所有相關資產。

若要將體驗片段從AEM匯出至Target（指定雲端設定後）:

1. 導覽至體驗片段主控台。
1. 選取您要匯出至目標的體驗片段。

   >[!NOTE]
   >
   >必須是體驗片段Web變數。

1. 點選/按一下 **匯出至Adobe Target**.

   >[!NOTE]
   >
   >如果體驗片段已匯出，請選取 **Adobe Target中的更新**.

1. 點選/按一下 **不發佈即可匯出** 或 **發佈** 視需要。

   >[!NOTE]
   >
   >選取 **發佈** 會立即發佈體驗片段並傳送至Target。

1. 點選/按一下 **確定** 在確認對話方塊中。

   您的體驗片段現在應位於Target中。

   >[!NOTE]
   >
   >[各種詳細資訊](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) 的 **清單檢視** 控制台和 **屬性**.

   >[!NOTE]
   >
   >在Adobe Target中檢視體驗片段時， *上次修改* 顯示的日期是片段上次在AEM中修改的日期，而非片段上次匯出至Adobe Target的日期。

>[!NOTE]
>
>或者，您也可以使用 [頁面資訊](/help/sites-authoring/author-environment-tools.md#page-information) 功能表。

## 在Adobe Target中使用您的體驗片段 {#using-your-experience-fragments-in-adobe-target}

執行先前的工作後，體驗片段會顯示在Target的「選件」頁面上。 請看 [特定Target檔案](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) 了解你能在那裡實現什麼。

>[!NOTE]
>
>在Adobe Target中檢視體驗片段時， *上次修改* 顯示的日期是片段上次在AEM中修改的日期，而非片段上次匯出至Adobe Target的日期。

## 刪除已匯出至Adobe Target的體驗片段 {#deleting-an-experience-fragment-already-exported-to-adobe-target}

刪除已匯出至Target的體驗片段，如果該片段已用於Target中的選件，則可能會造成問題。 刪除片段會導致選件無法使用，因為AEM正在傳送片段內容。

要避免這種情況：

* 如果活動中目前未使用體驗片段，AEM可讓使用者刪除片段，而不含警告訊息。
* 如果Target中的活動目前正在使用體驗片段，則會出現錯誤訊息，警告AEM使用者刪除片段對活動可能造成的後果。

   AEM中的錯誤訊息並未禁止使用者（強制）刪除體驗片段。 如果刪除體驗片段：

   * 具有AEM體驗片段的Target選件可能會顯示不適當的行為

      * 由於體驗片段HTML推送至Target，選件可能仍會呈現
      * 如果參考的資產也在AEM中刪除，體驗片段中的任何參考可能也無法正常運作。
   * 當然，由於體驗片段已不存在，因此無法對體驗片段進行任何進一步修改。



## 從匯出至Target的體驗片段中移除ClientLib {#removing-clientlibs-from-fragments-exported-target}

體驗片段包含完整的html標籤和所有必要的用戶端程式庫(CSS/JS)，以便呈現片段完全等同於由體驗片段內容作者建立的片段。 這是按部就班的。

在AEM傳送的頁面上搭配使用體驗片段選件與Adobe Target時，目標頁面已包含所有必要的用戶端資料庫。 此外，體驗片段選件中不需要多餘的html(請參閱 [考量事項](#considerations))。

以下是體驗片段選件中html的偽範例：

```html
<!DOCTYPE>
<html>
   <head>
      <title>…</title>
      <!-- all of the client libraries (css/js) -->
      …
   </head>
   <body>
        <!--/* Actual XF Offer content would appear here... */-->
   </body>
</html>
```

在高階上，當AEM將體驗片段匯出至Adobe Target時，會使用數個其他Sling選取器執行此操作。 例如，匯出的體驗片段URL可能如下所示(注意 `nocloudconfigs.atoffer`):

* http://www.your-aem-instance.com/content/experience-fragments/my-offers/my-xf-offer.nocloudconfigs.atoffer.html

此 `nocloudconfigs` 選取器是透過使用HTL來定義，可透過從複製來覆蓋：

* /libs/cq/experience-fragments/components/xfpage/nocloudconfigs.html

此 `atoffer` 選取器實際會套用後處理，使用 [Sling重寫器](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html). 可以用於刪除客戶端庫。

### 範例 {#example}

為此，我們將說明如何使用 `nocloudconfigs`.

>[!NOTE]
>
>請參閱 [可編輯的範本](/help/sites-developing/templates.md#editable-templates) 以取得詳細資訊。

#### 覆蓋 {#overlays}

在此特定範例中， [覆蓋](/help/sites-developing/overlays.md) 包含將刪除客戶端庫 *和* 無關的html。 假設您已建立體驗片段範本類型。 需要從 `/libs/cq/experience-fragments/components/xfpage/` 包括：

* `nocloudconfigs.html`
* `head.nocloudconfigs.html`
* `body.nocloudconfigs.html`

#### 範本類型覆蓋圖 {#template-type-overlays}

在此範例中，我們將使用下列結構：

![範本類型覆蓋圖](assets/xf-target-integration-02.png "範本類型覆蓋圖")

這些檔案的內容如下：

* `body.nocloudconfigs.html`

   ![body.nocloudconfigs.html](assets/xf-target-integration-03.png "body.nocloudconfigs.html")

* `head.nocloudconfigs.html`

   ![head.nocloudconfigs.html](assets/xf-target-integration-04.png "head.nocloudconfigs.html")

* `nocloudconfigs.html`

   ![nocloudconfigs.html](assets/xf-target-integration-05.png "nocloudconfigs.html")

>[!NOTE]
>
>使用 `data-sly-unwrap` 移除您需要的body標籤 `nocloudconfigs.html`.

### 考量事項 {#considerations}

如果您需要使用Adobe Target中的體驗片段選件來支援AEM網站和非AEM網站，則需要建立兩個體驗片段（兩種不同的範本類型）:

* 具有覆蓋以移除clientlibs/額外html的

* 沒有覆蓋，因此包含必要的clientlib