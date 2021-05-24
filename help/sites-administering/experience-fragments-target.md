---
title: 將體驗片段匯出至Adobe Target
seo-title: 將體驗片段匯出至Adobe Target
description: 將體驗片段匯出至Adobe Target
seo-description: 將體驗片段匯出至Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 0%

---

# 將體驗片段匯出至Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>本頁面的某些功能需要應用AEM 6.5.3.0。
>
>6.5.3.0
>
>* **現在** 已選取Externalizer Domainscan。
   >  **注意：** 外部化程式網域僅與傳送至Target的體驗片段內容相關，而與檢視選件內容等中繼資料無關。
>
>
6.5.2.0:
>
>* 體驗片段可匯出至：
   >
   >   
   * 預設工作區。
   >   * 在雲端設定中指定的已命名工作區。
   >   * **注意：** 匯出至特定工作區需有Adobe Target Premium。
>
>* AEM必須與Adobe Target整合，使用Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md)。[

>
>

AEM 6.5.0.0和6.5.1.0:
>
>* AEM體驗片段會匯出至Adobe Target的預設工作區。
>* AEM必鬚根據[與Adobe Target整合](/help/sites-administering/target.md)下的指示與Adobe Target整合。


您可以將在Adobe Experience Manager(AEM)中建立的[體驗片段](/help/sites-authoring/experience-fragments.md)匯出至Adobe Target(Target)。 然後可在Target活動中作為選件，以大規模測試並個人化體驗。

有三種格式選項可用來匯出體驗片段至Adobe Target:

* HTML（預設）:支援網頁和混合式內容傳送
* JSON:支援無頭內容傳送
* HTML 和 JSON

AEM體驗片段可匯出至Adobe Target中的預設工作區，或匯出至Adobe Target的使用者定義工作區。 這是透過Adobe I/O完成，AEM必須針對此項目使用Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md)與Adobe Target整合。[

>[!NOTE]
>
>Adobe Target工作區不存在於Adobe Target本身。 這些範本會在AdobeIMS(Identity Management系統)中定義和管理，然後透過Adobe I/O整合在解決方案中選取以用途。

>[!NOTE]
>
>Adobe Target工作區可用來允許組織（群組）的成員僅建立和管理此組織的選件和活動；而不授予其他使用者存取權。 例如，全球關注的特定國家組織。

>[!NOTE]
>
>如需詳細資訊，另請參閱：
>
>* [Adobe Target開發](https://www.adobe.io/apis/experiencecloud/target.html)
>* [核心元件 — 體驗片段](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

>



## 必備條件 {#prerequisites}

>[!CAUTION]
>
>本頁面的某些功能需要應用AEM 6.5.3.0。

需要執行各種動作：

1. 您必須使用Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md)將AEM與Adobe Target整合。[
2. 體驗片段會從AEM製作例項匯出，因此您需要在製作例項上[設定AEM連結外部化程式](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)，以確保體驗片段內的任何參照會外部化，以便進行Web傳送。

   >[!NOTE]
   >
   >對於預設未涵蓋的連結重寫，可使用[體驗片段連結重寫器提供者](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html)。 借此，您可針對執行個體開發自訂規則。

## 添加雲配置{#add-the-cloud-configuration}

匯出片段之前，您需要將&#x200B;**Adobe Target**&#x200B;的&#x200B;**雲端設定**&#x200B;新增至片段或資料夾。 這也可讓您：

* 指定要用於匯出的格式選項
* 選擇目標工作區作為目標
* 選取外部化程式網域，以重新寫入體驗片段中的參考（選用）

可在所需資料夾和/或片段的&#x200B;**頁面屬性**&#x200B;中選取所需選項；將視需要繼承規範。

1. 導覽至&#x200B;**體驗片段**&#x200B;主控台。

1. 開啟&#x200B;**頁面屬性**&#x200B;以取得適當的資料夾或片段。

   >[!NOTE]
   >
   >如果您將雲端設定新增至體驗片段上層資料夾，設定會由所有子項繼承。
   >
   >
   >如果您將雲端設定新增至體驗片段本身，則設定會由所有變數繼承。

1. 選擇&#x200B;**Cloud Services**&#x200B;頁簽。

1. 在&#x200B;**Cloud Service配置**&#x200B;下，從下拉清單中選擇&#x200B;**Adobe Target**。

   >[!NOTE]
   >
   >體驗片段選件的JSON格式可自訂。 若要這麼做，請定義客戶體驗片段元件，然後註解如何在元件Sling模型中匯出其屬性。
   >
   >請參閱核心元件：
   >
   >[核心元件 — 體驗片段](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   在&#x200B;**Adobe Target**&#x200B;下，選擇：

   * 適當的配置
   * 所需格式選項
   * Adobe Target工作區
   * 如有必要 — externalizer域

   >[!CAUTION]
   >
   >外部化程式域是可選的。
   >
   > 當您希望匯出的內容指向特定&#x200B;*publish*&#x200B;網域時，會設定AEM外部化程式。 如需更多詳細資訊，請參閱[設定AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)。
   >
   > 另請注意，外部化程式網域僅與傳送至Target的體驗片段內容相關，而與檢視選件內容等中繼資料無關。

   例如，對於資料夾：

   ![資料夾 — 雲端服](assets/xf-target-integration-01.png "務資料夾 — Cloud Services")

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

1. 點選/按一下「**匯出至Adobe Target**」。

   >[!NOTE]
   >
   >如果體驗片段已匯出，請選取「在Adobe Target **中更新」 。**

1. 視需要點選/按一下「匯出」，而不發佈&#x200B;**或「**&#x200B;發佈&#x200B;**」。**

   >[!NOTE]
   >
   >選取&#x200B;**Publish**&#x200B;會立即發佈體驗片段並將其傳送至Target。

1. 在確認對話方塊中，點選/按一下&#x200B;**確定**。

   您的體驗片段現在應位於Target中。

   >[!NOTE]
   >
   >[您可](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) 以在主控台的「清單檢視」和「 **屬** 性」中查看匯出的各 **種詳細資訊**。

   >[!NOTE]
   >
   >在Adobe Target中檢視體驗片段時，所看到的&#x200B;*上次修改*&#x200B;日期為AEM中上次修改片段的日期，而非上次匯出至Adobe Target的日期。

>[!NOTE]
>
>或者，您也可以使用[Page Information](/help/sites-authoring/author-environment-tools.md#page-information)菜單中的可比命令從頁面編輯器執行導出。

## 在Adobe Target中使用體驗片段{#using-your-experience-fragments-in-adobe-target}

執行先前的工作後，體驗片段會顯示在Target的「選件」頁面上。 請查看[特定Target檔案](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html)，了解您可在其中達成什麼目標。

>[!NOTE]
>
>在Adobe Target中檢視體驗片段時，所看到的&#x200B;*上次修改*&#x200B;日期為AEM中上次修改片段的日期，而非上次匯出至Adobe Target的日期。

## 刪除已匯出至Adobe Target的體驗片段{#deleting-an-experience-fragment-already-exported-to-adobe-target}

刪除已匯出至Target的體驗片段，如果該片段已用於Target中的選件，則可能會造成問題。 刪除片段會導致選件無法使用，因為AEM正在傳送片段內容。

要避免這種情況：

* 如果活動中目前未使用體驗片段，AEM可讓使用者刪除片段，而不含警告訊息。
* 如果Target中的活動目前正在使用體驗片段，則會出現錯誤訊息，警告AEM使用者刪除片段對活動可能造成的後果。

   AEM中的錯誤訊息並未禁止使用者（強制）刪除體驗片段。 如果刪除體驗片段：

   * 具有AEM體驗片段的Target選件可能會顯示不適當的行為

      * 由於體驗片段HTML已推送至Target，選件可能仍會呈現
      * 如果參考的資產也在AEM中刪除，體驗片段中的任何參考可能也無法正常運作。
   * 當然，由於體驗片段已不存在，因此無法對體驗片段進行任何進一步修改。
