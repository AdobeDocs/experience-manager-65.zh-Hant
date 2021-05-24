---
title: 向電子郵件服務提供者發佈電子郵件
seo-title: 向電子郵件服務提供者發佈電子郵件
description: 您可以將電子報發佈至電子郵件服務，例如ExactTarget和Silverpop Engage。
seo-description: 您可以將電子報發佈至電子郵件服務，例如ExactTarget和Silverpop Engage。
uuid: 1a7adcfe-8e52-49f4-9a00-99ac99881225
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: b9618913-5433-4baf-9ff6-490a26860505
exl-id: c07692f7-3618-4e8c-96d7-4db09f2d9896
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 2%

---

# 將電子郵件發佈到電子郵件服務提供商{#publishing-an-email-to-email-service-providers}

您可以將電子報發佈至電子郵件服務，例如ExactTarget和Silverpop Engage。 本檔案說明如何設定AEM以發佈電子報給這些電子郵件服務。

>[!NOTE]
>
>您必須先設定服務提供者，才能建立和發佈電子郵件。 如需詳細資訊，請參閱[設定ExactTarget](/help/sites-administering/exacttarget.md)和[設定Silverpop參與](/help/sites-administering/silverpop.md) 。

若要將電子郵件發佈至電子郵件服務提供者，您必須執行下列步驟：

1. 建立電子郵件。
1. 將電子郵件服務設定套用至電子郵件。
1. 發佈電子郵件。

>[!NOTE]
>
>如果您更新電子郵件提供者、進行飛行測試或傳送電子報，如果電子報未先發佈至「發佈」執行個體，或者「發佈」執行個體無法使用，則這些操作會失敗。 請務必發佈電子報，並確認Publish執行個體已開啟並執行。

## 建立電子郵件{#creating-an-email}

您可使用&#x200B;**Geometrixx電子報**&#x200B;範本，在促銷活動下建立您要發佈至電子郵件服務的電子郵件或電子報。 您也可以使用&#x200B;**Geometrixx Outdoors電子郵件**&#x200B;範本。 **Geometrixx Outdoors電子郵件**&#x200B;範本的範例電子郵件/電子報可在`https://<hostname>:<port>/cf#/content/campaigns/geometrixx-outdoors/e-mails.html`取得。

要建立發佈到配置的電子郵件服務的新電子郵件，請執行以下操作：

1. 前往&#x200B;**Websites**，然後前往&#x200B;**Campaigns**。 選擇促銷活動。
1. 按一下&#x200B;**New**&#x200B;以開啟&#x200B;**Create Page**&#x200B;視窗。
1. 輸入標題、名稱，然後從可用模板清單中選擇&#x200B;**Geometrixx電子報**&#x200B;模板。
1. 按一下&#x200B;**建立**。
1. 開啟已建立的電子郵件。
1. 切換至設計模式，以選取您要在sidekick中顯示的元件。
1. 切換至編輯模式，開始將內容（文字、影像、[電子郵件工具](#adding-exacttarget-email-tools-to-your-email)、[個人化變數](#adding-text-and-personalization-tool-to-your-e-mail)等）新增至您的電子郵件。

### 將ExactTarget電子郵件工具新增至您的電子郵件{#adding-exacttarget-email-tools-to-your-email}

>[!NOTE]
>
>此區段專屬於ExactTarget服務。

ExactTarget的&#x200B;**電子郵件工具**&#x200B;元件可為您的電子郵件/電子報新增更多電子郵件功能。

1. 開啟要發佈至ExactTarget的電子郵件。
1. 使用sidekick將元件&#x200B;**ET — 電子郵件工具**&#x200B;新增至頁面。 在「編輯」模式中開啟元件。

   ![chlimage_1](assets/chlimage_1.gif)

1. 從&#x200B;**Options**&#x200B;菜單中選擇一個選項：

<table>
 <tbody>
  <tr>
   <td>郵寄地址 (必要)</td>
   <td>此元件會將貴組織的實際郵寄地址插入電子郵件中。</td>
  </tr>
  <tr>
   <td>設定檔中心 (必要)</td>
   <td>設定檔中心是一個網頁，訂閱者可在此輸入及維護您保留的關於他們的個人資訊。</td>
  </tr>
  <tr>
   <td>以網頁的形式檢視電子郵件</td>
   <td>此元件可讓使用者以網頁形式檢視電子郵件。</td>
  </tr>
  <tr>
   <td>隱私權原則</td>
   <td>此元件會在電子郵件中插入指向您的隱私策略的連結。<br /> </td>
  </tr>
  <tr>
   <td>取消訂閱中心</td>
   <td>為使用者提供從您的郵件清單取消訂閱的選項。</td>
  </tr>
  <tr>
   <td>訂閱中心</td>
   <td>訂閱中心是一個網頁，訂閱者可在其中控制他們從您的組織收到的訊息。</td>
  </tr>
  <tr>
   <td>追蹤電子郵件開啟次數</td>
   <td>允許您使用ExactTarget追蹤功能的隱藏元件。<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>只有在將ExactTarget設定套用至電子郵件時，才會填入&#x200B;**Options**&#x200B;下拉式選單。 如需詳細資訊，請參閱[將電子郵件服務組態套用至電子郵件設定](#applying-e-mail-service-configuration-to-e-mail-settings) 。

1. 將電子郵件發佈至ExactTarget。

   具有電子郵件工具的電子郵件可用於設定的ExactTarget帳戶。

>[!NOTE]
>
>* 只有當使用&#x200B;**Simple Send**&#x200B;或&#x200B;**Guided Send**&#x200B;但不使用&#x200B;**Test Send**&#x200B;傳送電子郵件時，電子郵件工具內的URL才會被其實際值取代。
   >
   >
* 需要兩種電子郵件工具：**實際郵寄地址（必要）**&#x200B;和&#x200B;**配置檔案中心（必要）**。 當電子郵件發佈至ExactTarget時，這兩個電子郵件工具會依預設新增至每封郵件的底部。

>



### 將文字和個人化工具新增至您的電子郵件{#adding-text-and-personalization-tool-to-your-e-mail}

您可以將&#x200B;**文字和個人化**&#x200B;元件新增至頁面，借此在電子郵件中新增個人化欄位：

1. 開啟要發佈到電子郵件服務的電子郵件。
1. 若要從電子郵件服務啟用個人化欄位，請在設定電子郵件服務時新增架構設定。 如需詳細資訊，請參閱[設定Silverpop參與](/help/sites-administering/silverpop.md)和[設定確切目標](/help/sites-administering/exacttarget.md)。
1. 從sidekick新增元件&#x200B;**Text &amp; Personalization**。 此元件是電子報群組的一部分。 在編輯模式中開啟此元件。

   ![chlimage_1-110](assets/chlimage_1-110a.png)

1. 從下拉式選單中選取欄位並按一下&#x200B;**插入**，將必要的個人化欄位新增至文字。
1. 按一下&#x200B;**OK**&#x200B;以完成。

## 將電子郵件服務配置應用於電子郵件設定{#applying-e-mail-service-configuration-to-e-mail-settings}

要將電子郵件服務配置應用於新聞稿，請執行以下操作：

1. 建立電子郵件服務配置。
1. 開啟您的電子郵件/電子報。
1. 按一下&#x200B;**Settings**&#x200B;或按一下sidekick中的&#x200B;**Page Properties ，開啟電子郵件/電子報設定。**
1. 在&#x200B;**Cloud Services**&#x200B;標籤中，按一下「**新增服務**」。 您會看到服務清單。 從下拉式清單的清單中選取您所需的設定 — **ExactTarget**&#x200B;或&#x200B;**Silverpop** - 。

   ![chlimage_1-5](assets/chlimage_1-5a.jpeg)

1. 按一下&#x200B;**「確定」**。

## 發佈電子郵件至電子郵件服務{#publishing-emails-to-email-service}

您可以依照下列步驟將電子郵件/電子報發佈至您的電子郵件服務：

1. 開啟電子郵件。
1. 發佈電子郵件之前，請確定您已將正確的設定套用至電子郵件。
1. 按一下&#x200B;**Publish**。 這將開啟&#x200B;**向電子郵件服務提供商**&#x200B;發佈新聞稿窗口。
1. 填寫&#x200B;**新聞稿名稱**&#x200B;欄位。 電子郵件/電子報會以此名稱發佈至電子郵件服務提供者。 如果未提供電子郵件名稱，則會使用AEM中電子報的頁面名稱來發佈電子郵件。
1. 按一下&#x200B;**Publish**。

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

   如果成功，AEM會確認您可以在ExactTarget或Silverpop Engage中檢視電子郵件。

   如果是ExactTarget，按一下「**檢視已發佈的電子郵件**」即可檢視已發佈的電子郵件。 這會直接帶您前往ExactTarget中已發佈的電子報([https://members.exacttarget.com/](https://members.exacttarget.com/))。

>[!NOTE]
>
>如果已發佈與已發佈的電子郵件/電子報同名的電子郵件/電子報，則不會取代先前的電子郵件/電子報。 而是會以相同名稱建立新的電子郵件/電子報（但兩個電子報的ID則不同）。
>
>將電子郵件/電子報發佈至電子郵件服務提供者，也會將電子郵件/電子報發佈至AEM發佈執行個體。


### 更新已發佈的電子郵件{#updating-a-published-e-mail}

「發佈」對話框上的&#x200B;**「更新」**&#x200B;按鈕允許您更新已發佈到電子郵件服務提供商的新聞稿。 如果尚未發佈新聞稿，且按一下&#x200B;**Update**&#x200B;按鈕，**Newsletter將不會發佈**&#x200B;訊息。

若要更新已發佈的電子郵件：

1. 開啟先前已發佈給電子郵件服務提供者的電子郵件/電子報，在您變更電子郵件/電子報後，請重新發佈該電子郵件服務提供者。
1. 按一下&#x200B;**Publish**。 隨即顯示「**向電子郵件服務提供者發佈電子報**」窗口。 按一下&#x200B;**更新**。

   若要檢查ExactTarget上是否更新了電子郵件/電子報，請按一下「**檢視已發佈的電子郵件**」。 這會將您帶往ExactTarget中已發佈的電子郵件。

   若要檢查Silverpop電子郵件服務上的電子郵件/電子報是否已更新，請造訪Silverpop Engage網站。
