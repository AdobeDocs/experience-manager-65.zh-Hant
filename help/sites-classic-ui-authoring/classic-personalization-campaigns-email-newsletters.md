---
title: 將電子郵件發佈給電子郵件服務供應商
seo-title: 將電子郵件發佈給電子郵件服務供應商
description: 您可以將電子報發佈至電子郵件服務，例如ExactTarget和Silverpop Engage。
seo-description: 您可以將電子報發佈至電子郵件服務，例如ExactTarget和Silverpop Engage。
uuid: 1a7adcfe-8e52-49f4-9a00-99ac99881225
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: b9618913-5433-4baf-9ff6-490a26860505
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# 將電子郵件發佈給電子郵件服務供應商{#publishing-an-email-to-email-service-providers}

您可以將電子報發佈至電子郵件服務，例如ExactTarget和Silverpop Engage。 本檔案說明如何設定AEM，以發佈電子報至這些電子郵件服務。

>[!NOTE]
>
>您必須先設定服務提供者，才能建立和發佈電子郵件。 如需詳 [細資訊，請參](/help/sites-administering/exacttarget.md) 閱設定ExactTarget [和](/help/sites-administering/silverpop.md) 設定Silverpop Engage。

若要將電子郵件發佈至電子郵件服務供應商，您必須執行下列步驟：

1. 建立電子郵件。
1. 將電子郵件服務設定套用至電子郵件。
1. 發佈電子郵件。

>[!NOTE]
>
>如果您更新電子郵件提供者、進行飛行測試或傳送電子報，如果電子報未先發佈至「發佈」例項或「發佈」例項不可用，這些作業就會失敗。 請確定要發佈您的電子報，並確定「發佈」執行個體已啟動並執行。

## 建立電子郵件 {#creating-an-email}

您想要發佈至電子郵件服務的電子郵件或電子報，可使用 **Geometrixx Newsletter範本在促銷活動下建立** 。 您也可以使用 **Geometrixx Outdoors E-Mail範本** 。 如需以 **Geometrixx Outdoors E-Mail範本為基礎的範例電子郵件／電子報** ，請參閱 `https://<hostname>:<port>/cf#/content/campaigns/geometrixx-outdoors/e-mails.html`。

要建立發佈到已配置電子郵件服務的新電子郵件，請執行以下操作：

1. 先前往「 **網站** 」，再 **前往「促銷活動**」。 選擇促銷活動。
1. 按一 **下「新增** 」以開啟「 **建立頁面** 」視窗。
1. 輸入標題、名稱，並從可用範本清 **單中選取Geometrixx** Newsletter範本。
1. 按一下&#x200B;**「建立」**。
1. 開啟建立的電子郵件。
1. 切換至設計模式，以選取您要在sidekick中顯示的元件。
1. 切換至編輯模式，開始將內容(文字、影像 [、電子郵件工具](#adding-exacttarget-email-tools-to-your-email)[、個人化變數](#adding-text-and-personalization-tool-to-your-e-mail)，等等)新增至您的電子郵件。

### 將ExactTarget電子郵件工具新增至您的電子郵件 {#adding-exacttarget-email-tools-to-your-email}

>[!NOTE]
>
>此部分是ExactTarget服務的特定部分。

ExactTarget **的「電子郵件工具** 」元件可為您的電子郵件／電子報新增更多電子郵件功能。

1. 開啟要發佈至ExactTarget的電子郵件。
1. 使用sidekick將元件 **ET —— 電子郵件工具** (Email Tools)新增至您的頁面。 在「編輯」模式下開啟元件。

   ![chlimage_1](assets/chlimage_1.gif)

1. 從「選項」菜單中選 **擇一個選** 項：

<table>
 <tbody>
  <tr>
   <td>郵寄地址 (必要)</td>
   <td>此元件將組織的實際郵寄地址插入您的電子郵件中。</td>
  </tr>
  <tr>
   <td>設定檔中心 (必要)</td>
   <td>描述檔中心是一個網頁，用戶可以在其中輸入和維護您保存的個人資訊。</td>
  </tr>
  <tr>
   <td>以網頁的形式檢視電子郵件</td>
   <td>此元件可讓使用者將電子郵件檢視為網頁。</td>
  </tr>
  <tr>
   <td>隱私權原則</td>
   <td>此元件會在電子郵件中插入您隱私權政策的連結。<br /> </td>
  </tr>
  <tr>
   <td>取消訂閱中心</td>
   <td>將選項提供給使用者以取消訂閱您的郵件清單。</td>
  </tr>
  <tr>
   <td>訂閱中心</td>
   <td>訂閱中心是一個網頁，訂閱者可以控制從您組織收到的訊息。</td>
  </tr>
  <tr>
   <td>追蹤電子郵件開啟次數</td>
   <td>允許您使用ExactTarget追蹤功能的隱藏元件。<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>只有 **將ExactTarget設定套用至電子郵件時，才會填入「選項** 」下拉式功能表。 如需詳 [細資訊，請參閱套用電子郵件服務設定](#applying-e-mail-service-configuration-to-e-mail-settings) 「電子郵件設定」。

1. 將電子郵件發佈至ExactTarget。

   包含電子郵件工具的電子郵件可供設定的ExactTarget帳戶使用。

>[!NOTE]
>
>* 只有當使用「簡單傳送」或「引導傳送」（而非「測試傳送」）傳送電子郵件時，電子郵件工具中的URL才會以 **其實際值取代（在收到的電子郵件中）**********。
   >
   >
* 需要兩種電子郵件工具：實 **體郵寄地址（必要）****和描述檔中心（必要）**。 當電子郵件發佈至ExactTarget時，這兩個電子郵件工具預設會新增至每封郵件的底部。
>



### 將文字和個人化工具新增至您的電子郵件 {#adding-text-and-personalization-tool-to-your-e-mail}

您可以將「文字與個人化」元件新增至頁面， **以在電子郵件中新增個人化欄位** :

1. 開啟要發佈至電子郵件服務的電子郵件。
1. 若要從電子郵件服務啟用個人化欄位，請在設定電子郵件服務時新增架構設定。 如需詳 [細資訊，請參閱設定Silverpop](/help/sites-administering/silverpop.md) Engage [](/help/sites-administering/exacttarget.md) 和設定完全目標。
1. 從sidekick新增 **元件「文字與個人化** 」。 此元件是電子報群組的一部分。 在編輯模式中開啟此元件。

   ![chlimage_1-110](assets/chlimage_1-110a.png)

1. 從下拉式選單中選取欄位，然後按一下「插入」，將必要的個人化欄位新增至 **文字**。
1. 按一 **下「確定** 」以完成。

## 將電子郵件服務配置應用於電子郵件設定 {#applying-e-mail-service-configuration-to-e-mail-settings}

要將電子郵件服務配置應用於電子報，請執行以下操作：

1. 建立電子郵件服務配置。
1. 開啟您的電子郵件／電子報。
1. 按一下「設定」或按一下側 **點中的「頁面屬性」** ，以開 **啟電子郵件／電子報設定** 。
1. 按一 **下「雲端服務** 」標 **簽中的「新增服務** 」。 您會看到服務清單。 從下拉式清單的清單 **中，選取您所需的設定- ExactTarget** 或 **Silverpop** 。

   ![chlimage_1-5](assets/chlimage_1-5a.jpeg)

1. 按一下 **確定**。

## 將電子郵件發佈至電子郵件服務 {#publishing-emails-to-email-service}

電子郵件／電子報可依照下列步驟發佈至您的電子郵件服務：

1. 開啟電子郵件。
1. 發佈電子郵件之前，請確定您已將正確的設定套用至電子郵件。
1. 按一 **下「發佈**」。 這會開啟「 **將電子報發佈至電子郵件服務供應商** 」視窗。
1. 填寫電子報 **名稱欄位** 。 電子郵件／電子報會以此名稱發佈給電子郵件服務供應商。 如果未提供電子郵件名稱，則會使用AEM中電子報的頁面名稱來發佈電子郵件。
1. 按一 **下「發佈**」。

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

   如果成功，AEM會確認您可以在ExactTarget或Silverpop Engage中檢視電子郵件。

   如果是ExactTarget，則可按一下「檢視已發佈的電子郵件」來檢 **視已發佈的電子郵件**。 這會直接帶您前往ExactTarget([https://members.exacttarget.com/](https://members.exacttarget.com/))中發佈的電子報。

>[!NOTE]
>
>如果以與已發佈之電子郵件／電子報相同的名稱發佈電子郵件／電子報，則不會取代先前的電子郵件／電子報。 而是以相同名稱建立新的電子郵件／電子報（但是，兩個電子報的ID不同）。
>
>將電子郵件／電子報發佈至電子郵件服務供應商也會將電子郵件／電子報發佈至AEM發佈例項。


### 更新已發佈的電子郵件 {#updating-a-published-e-mail}

「發 **布** 」對話方塊上的「更新」按鈕可讓您更新已發佈至電子郵件服務供應商的電子報。 如果電子報尚未發佈，且按一下「 **更新** 」按鈕，則 **不會顯示「電子報** 」訊息。

若要更新已發佈的電子郵件：

1. 開啟先前已發佈給電子郵件服務供應商的電子郵件／電子報，在您變更電子郵件／電子報後，您要重新發佈該電子郵件服務供應商。
1. 按一 **下「發佈**」。 將顯 **示「將電子報發佈至電子郵件服務供應商** 」視窗。 按一 **下更新**。

   若要檢查ExactTarget上的電子郵件／電子報是否已更新，請按一下「檢視已發 **布的電子郵件**」。 這會帶您前往ExactTarget中已發佈的電子郵件。

   若要檢查Silverpop電子郵件服務上的電子郵件／電子報是否已更新，請造訪Silverpop Engage網站。

