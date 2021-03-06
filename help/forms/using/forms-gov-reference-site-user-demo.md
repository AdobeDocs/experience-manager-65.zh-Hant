---
title: We.Gov和We.Finance參考網站逐步說明
seo-title: We.Gov和We.Finance參考網站逐步說明
description: 使用虛構的使用者和群組，使用We.Gov和We.Finance示範套件執行AEM Forms工作。
seo-description: 使用虛構的使用者和群組，使用We.Gov和We.Finance示範套件執行AEM Forms工作。
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
exl-id: 288d5459-bc69-4328-b6c9-4b4960bf4977
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 0%

---

# We.Gov和We.Finance參考網站逐步說明{#we-gov-reference-site-walkthrough}

## 先決條件{#pre-requisites}

按照[設定和配置We.Gov和We.Finance引用站點](../../forms/using/forms-install-configure-gov-reference-site.md)中所述設定引用站點。

## 用戶動態{#user-story}

* AEM Forms

   * 自動表單轉換
   * 製作
   * 表單資料模型/資料來源

* AEM Forms

   * 資料擷取
   * （可選）資料整合(MS Dynamics)
   * （選用）Adobe Sign

* 工作流程
* 電子郵件通知
* （可選）客戶通訊

   * Print Channel
   * Web Channel

* Adobe Analytics
* 資料來源整合

### 虛構的使用者和群組{#fictitious-users-and-groups}

We.Gov示範套件隨附下列內建的虛構使用者：

* **阿雅·譚**:有資格獲得政府機構服務的公民

![虛構使用者](/help/forms/using/assets/aya_tan_new.png)

* **喬治·朗**:We.Gov機構業務分析員

![虛構使用者](/help/forms/using/assets/george_lang.png)

* **卡米拉·桑托斯**:We.Gov代理CX銷售機會

![虛構使用者](/help/forms/using/assets/camila_santos.png)

也包括下列群組：

* **We.Gov Forms使用者**

   * 喬治·朗（成員）
   * 卡米拉·桑托斯（成員）

* **We.Gov用戶**

   * 喬治·朗（成員）
   * 卡米拉·桑托斯（成員）
   * 譚雅（成員）

### 示範概述術語圖例{#demo-overview-terms-legend}

1. **模擬**:AEM示範中已定義的使用者和群組。
1. **按鈕**:用於導航的彩色矩形或帶圓圈箭頭。
1. **按一下**:執行使用者動態中的動作。
1. **連結**:位於We.Gov網站的主功能表頂端。
1. **使用者指示**:瀏覽使用者動態時要遵循的數值步驟集。
1. **Forms Portal**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **行動檢視**:We.Gov使用者使用重新調整瀏覽器大小來複製行動檢視。
1. **案頭視圖**:We.gov使用者可在筆記型電腦或桌上型電腦上觀看示範。
1. **螢幕前表單**:在We.Gov網站首頁的表單。
1. **適用性表單**:We.gov演示的註冊申請表。

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **AdobeWe.Gov站點**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Adobe收件匣**:位於AEM後端的 [頂](assets/bell.svg) 端功能表列Bell圖示。

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **電子郵件用戶端**:檢視電子郵件的慣用方式(Gmail、Outlook)
1. **CTA**:行動要求
1. **導覽**:在瀏覽器頁面上找到特定參考點。
1. **AFC**:automated forms conversion

## automated forms conversion（卡米拉）{#automated-forms-conversion}

**本節**:Camila CX Lead現有的基於PDF的表單用於基於紙面的流程。作為現代化努力的一部分，她想要使用此PDF表單自動建立新的現代最適化Forms。

### automated forms conversion- We.Gov(Camila){#automated-forms-conversion-wegov}

1. 導覽至&#x200B;*https://&lt;aemserver>:&lt;port>/aem/start.html*

1. 登入方式：
   * **使用者**:卡米拉·桑托斯
   * **密碼**:密碼
1. 從首頁選擇「Forms > Forms與檔案> AEM Forms We.gov Forms > AFC」。
1. 卡米拉將PDF上傳至AEM Forms。

   ![上傳表單](assets/aftia-upload-form.jpg)

1. 然後，Camilla會選取PDF表單並按一下&#x200B;**開始自動轉換**&#x200B;以開始轉換程式。 如果您已轉換表單，則可能需要按一下「**覆寫轉換**」。

   >[!NOTE]
   >
   >請注意，AFC中的設定是為一般使用者預先設定的，因此不應加以變更。

   * **可選**:如果您希望使用「可訪問的超海洋」主題，只需按一下「指定最適化表單」主題，然後選擇出現在選項清單中的「可訪問 — 超海洋」主題。

   ![開始轉換](assets/aftia-start-conversion.jpg)

   ![超海洋主題](assets/aftia-upload-conversion-settings.jpg)

   轉換期間會顯示完成百分比狀態。 在狀態顯示&#x200B;**Converted**&#x200B;後，按一下&#x200B;**output**&#x200B;資料夾，選擇最適化表單，然後按一下&#x200B;**Edit**&#x200B;以開啟轉換的表單。

1. 然後，卡米拉會檢閱表單，並確認所有欄位皆存在

   ![檢閱轉換](assets/aftia-review-conversion.jpg)

1. 然後卡米拉開始編輯表單。 她會選取「根面板」>「編輯」（扳手）>從「面板配置」下拉式選單中選取「頂端的索引標籤」>選取「核取方塊」。

   ![查看屬性](assets/aftia-review-properties.jpg)

1. 然後，Camilla會新增所有必要的CSS和欄位變更，以產生最終產品。

   ![新增CSS](assets/aftia-add-css.jpg)

### 表單資料模型與資料來源(Camila){#data-sources}

**本節**:轉換完檔案並製作最適化表單後，Camila就需要將最適化表單連結至資料來源。

1. Camila會以在[Automated forms conversion- We.Gov](#automated-forms-conversion-wegov)中轉換的表單開啟「屬性」。

1. 然後，Camila從下拉清單中選擇表單模型>選擇表單資料模型>從選項清單中選擇We.gov註冊FDM。

1. 按一下「儲存並關閉」按鈕。

   ![FDM選取](assets/aftia-select-fdm.jpg)

1. 卡米拉按一下&#x200B;**output**&#x200B;資料夾，選取最適化表單，然後按一下&#x200B;**Edit**&#x200B;以開啟完成的We.Gov表單。
1. Camila選取最適化表單欄位，然後按一下「設定」圖示](assets/configure-icon.svg)。 ![她使用&#x200B;**Bind Reference**&#x200B;欄位建立與表單資料模型實體的綁定。 她會對最適化表單中的所有欄位重複此步驟。

### 表單協助工具測試(Camila){#form-accessibility-testing}

Camila也會驗證建立的內容是否已正確建立，且可依照公司標準完全存取。

1. 卡米拉按一下&#x200B;**output**&#x200B;資料夾，選取最適化表單，然後按一下&#x200B;**預覽**&#x200B;以開啟完成的We.Gov表單。

1. 開啟Chrome開發人員工具中的稽核標籤。

1. 執行協助工具檢查，以驗證最適化表單。

   ![協助工具檢查](assets/aftia-accessibility.jpg)

## 適用性表單行動檢視示範(Aya){#mobile-view-demo}

**必須在演示之前執行此部分。**

**使用者指示：**

1. 導覽至：*https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. 登入方式：

   1. **使用者**:aya.tan
   1. **密碼**:密碼

1. 重新調整瀏覽器視窗大小，或使用瀏覽器的模擬器來複製行動裝置大小。

### We.Gov網站(Aya){#aya-user-story-we-gov-website}

![虛構使用者](/help/forms/using/assets/aya_tan_new-1.png)

**本節**:阿亞是公民。她從一位朋友那裡得知，她可能有資格從政府機構獲得服務。 Aya從手機瀏覽到We.Gov網站，了解有關她有資格獲得的服務的更多資訊。

### We.Gov預屏(Aya){#aya-user-story-we-gov-pre-screener}

Aya在手機上填寫了一份簡短的最適化表格，以確認自己是否有資格。

**使用者指示：**

1. 在每個下拉式清單欄位中進行選取。

   >[!NOTE]
   >
   >如果使用者每年的收入超過$200,000，則不符合資格。

1. 按一下「**我是否符合資格？」**” 按鈕.
1. 按一下「**Apply Now**」按鈕繼續。

   ![立即應用連結](/help/forms/using/assets/apply_now_link.png)

### We.Gov適用性表單(Aya){#aya-user-story-we-gov-adaptive-form}

Aya發現她符合資格，並開始填寫她的申請，以在自己的移動設備上請求服務。

Aya需要在家中查看一些文檔，然後才能完成服務請求申請。 她會儲存應用程式，並從行動裝置退出。

**使用者指示：**

1. 填寫基本資訊欄位，以下是必填欄位和下拉式清單：

   1. 基本資訊

      1. 名字
      1. 姓氏
      1. DOB
      1. 電子郵件

1. 使用下列&#x200B;**動態邏輯**&#x200B;使用&#x200B;**系列狀態**&#x200B;下拉式清單演示動態功能：

   1. **單一**:顯示近鄰面板
   1. **已婚**:顯示婚內撫養人面板
   1. **離婚**:顯示近鄰面板
   1. **喪偶**:顯示近鄰面板
   1. **你有孩子嗎？**:（是/否）顯示子依存面板的單選按鈕。

      1. （新增/移除）按鈕，新增/移除多個子相依面板。

1. 按一下灰色菜單欄中的右箭頭。
1. 按一下底部的「儲存」按鈕。

   ![適用性表單詳細資訊](/help/forms/using/assets/adaptive_form.png)

## 案頭示範{#desktop-demo}

**本節：** 回到家後，Aya找到她需要的資訊，並從案頭恢復應用程式。Aya導航到線上表單門戶以恢復其應用。 透過一些簡單的自訂功能，代理商也可以自動產生連結並透過電子郵件傳回，以繼續應用程式。

### 持續適用性表單(Aya){#aya-user-story-continued-adaptive-form}

**使用者指示：**

1. 導覽至&#x200B;*https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. 在導航欄中，選擇「**Online Services**」。
1. 從「Forms草案」面板中，選擇現有的「健康福利登記申請」。

   ![健康福利的註冊申請](/help/forms/using/assets/enrollment_application.png)

   外觀和感覺都一樣，她不需要重新輸入任何資料。

   **使用者指示：**

1. 按一下右鍵「社交圈CTA」以移至下一個區段。

   ![Right circle CTA](/help/forms/using/assets/right_circle_cta_new.png)

   表單會填入到Aya最後一個入口的點。 Aya已輸入了她的所有資訊，並準備提交。

   ![提交最適化表單](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >當Aya填寫電話號碼欄位時，她必須以連續的11位數字填寫，不帶破折號、空格或連字型大小。

   提交Aya後，會收到「感謝」頁面。 （可選）她還會收到一封電子郵件，可以開啟它以電子方式與Adobe Sign簽署記錄檔案。

### 可選：Adobe Sign(Aya){#adobe-sign}

**使用者指示：**

1. 導覽至您的電子郵件用戶端，然後尋找Adobe Sign電子郵件。
1. 按一下連結至Adobe Sign。

   ![Adobe簽署連結](/help/forms/using/assets/adobe_sign_link.png)

**使用者指示：**

1. 選中「**I agree**」框。
1. 按一下「**Accept**」。
1. 滾動到已審閱文檔的底部。
1. 按一下醒目提示的黃色標籤以簽署檔案。

   ![簽署文](/help/forms/using/assets/sign_document_new.png) ![檔簽署測試文檔](/help/forms/using/assets/sign_test_document.png)

## 政府代理人（喬治）{#government-agent-george}

![喬治](/help/forms/using/assets/george_lang-1.png)

**本節：** George是政府機構Aya的業務分析員，向請求服務。George有一個儀表板，在該儀表板中，他可以查看已指派給他進行審核的所有服務請求應用程式。

### AEM收件匣(George){#george-user-story-aem-inbox}

**使用者指示：**

1. 導覽至&#x200B;*https://&lt;aemserver>:&lt;port>/aem/start.html*
1. 按一下用戶表徵圖（右上角），並使用「**登出**」，或「**模擬為**」菜單選項（如果您當前與管理用戶登錄）。

   1. 登入方式：

      1. **使用者：** george.lang
      1. **密碼：** 密碼
   1. 或模擬：

      1. 在「**模擬為**」欄位中鍵入「**George**」。

      1. 按一下「確定」進行模擬。


1. 從右上角按一下通知（鈴聲）圖示。
1. 按一下「**View All**」以導覽至收件匣。
1. 從收件箱中，開啟最新的「**Health Benefits Application Review**」任務。

   ![健康優勢應用程式審核](/help/forms/using/assets/health_benefits.png)

### 可選：AEM收件匣與MS Dynamics(George){#george-user-story-aem-inbox-and-ms-dynamics}

由於資料整合和自動化工作流程，Aya的應用程式以及在提交資料時自動產生的CRM記錄都會出現。

**使用者指示：**

1. 開啟並檢查唯讀最適化表單。
1. 按一下「**開啟MS Dynamics**」按鈕，在新窗口中開啟MS Dynamics記錄。
1. 在CRM中，您可以看到所有資訊皆可更新

   1. （可選）直接在Dynamics中新增一些審核附註。

1. 關閉並返回AEM收件匣。

   ![MS Dynamics記錄](/help/forms/using/assets/ms_dynamics.png)

### 返回AEM收件匣(George){#george-user-story-back-to-aem-inbox}

George批准Aya的應用程式，由於現有的自動化工作流程，確認電子郵件也會發送到Aya。

**使用者指示：**

1. 導覽至左上角，然後按一下「**Approve**」以核准應用程式。
1. 在強制回應視窗中，您可以留下CX銷售線索的訊息。
1. 按一下「完成」。
1. （公民角色）開啟您的電子郵件用戶端以檢視傳送至Aya的電子郵件。

   ![查看發送到Aya的電子郵件](/help/forms/using/assets/email_client.png)

## CX銷售線(Camila){#cx-lead-camila}

![卡米拉（CX銷售線）](/help/forms/using/assets/camila_santos-1.png)

**本節：** Camila the CX Lead與Aya建立歡迎電話，以說明如何使用她獲得批准的政府服務。

### （可選）AEM收件匣和MS Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**使用者指示：**

1. 導覽至&#x200B;*https://&lt;aemserver>:&lt;port>/aem/start.html*
1. 按一下用戶表徵圖（右上角），並使用「**登出**」，或「**模擬為**」菜單選項（如果您當前與管理用戶登錄）。

   1. 登入方式：

      1. **使用者**:卡米拉·桑托斯
      1. **密碼**:密碼
   1. 或模擬：

      1. 在「**模擬為**」欄位中鍵入「**Camila**」。

      1. 按一下「確定」進行模擬。


1. 從右上角按一下通知（鈴聲）圖示。
1. 按一下「**View All**」以導覽至收件匣。
1. 從收件箱中，開啟最新的「**新聯繫人批准**」任務。

![新聯繫人批准](/help/forms/using/assets/new_contact_approval.png)

**（選用）使用指示：**

1. 開啟並檢查唯讀最適化表單。
1. 按一下「**開啟MS Dynamics**」按鈕，在新窗口中開啟MS Dynamics記錄。
1. 在CRM中，您可以看到所有資訊皆可更新

   1. （可選）直接在Dynamics中新增呼叫活動。
   1. 開啟「**Activities**」區段。
   1. 按一下「**新電話呼叫**」選項。
   1. 添加電話呼叫詳細資訊。
   1. 儲存並關閉視窗。

1. 返回AEM，導覽至左上角，然後按一下「**Submit**」以提交申請。
1. 在強制回應視窗中，您可以留出訊息。
1. 按一下「完成」。

   ![活動頁](/help/forms/using/assets/activities_tab.png) ![簽確認新聯繫人](/help/forms/using/assets/confirm_new_contact.png)

## （可選）歡迎套件公民(Aya){#welcome-kit-citizen-aya}

**此小節：** Aya收到一封電子郵件，其中包含一個互動式通訊的連結，可總結其優點，並包含要填寫的表單欄位。附上PDF優勢聲明並連結至郵件中的互動式通信信函（主題/品牌與互動式通信相同）。

### 電子郵件客戶端通知(Aya){#aya-user-story-email-client}

**使用者指示：**

1. 找到並開啟Welcome Kit電子郵件。
1. 捲動至頁面底部的PDF附件。
1. 按一下以開啟PDF附件。
1. 在電子郵件客戶端中向上滾動，然後按一下「**聯機查看歡迎套件**」。

   1. 這將開啟同一文檔的Web通道版本。

1. 直接參考PDF:

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. 直接參考IC:

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![歡迎好處手](/help/forms/using/assets/welcome_benefits_handbook.png) ![冊互動式通信連結](/help/forms/using/assets/interactive_communication.png)

## 續約提醒公民(Aya){#renewal-reminder-citizen-aya}

**本節：** Camila也會在一年後排程通訊提醒。（自動化/執行和電子郵件的工作流程步驟）。

### 電子郵件客戶端通知(Aya){#aya-user-story-email-client-updated}

**使用者指示：**

1. 導覽至您的電子郵件用戶端。
1. 找到並開啟續訂提醒電子郵件。
1. 按一下「**提交新應用程式**」按鈕以開啟最適化表單。

   1. 此區段刻意保留為空白，以支援階段2中的資料預填。

   ![續訂提醒電子郵件](/help/forms/using/assets/renewal_reminder_email.png)

## （可選）表單資料模型(Camila){#form-data-model}

**本節**:Camila會導覽至AEM Forms資料整合，您可在此執行快速測試，以確認透過表單資料模型整合傳送至外部資料來源的資訊確實存在。

### 表單資料模型(Camila){#form-data-model-camila}

**本節**:Camila導航到「資料源」頁，以驗證伺服器已在Derby資料庫中複製的資料。

1. 使用者體驗完成且使用者提交完成後，Camila會導覽至AEM Forms中的「資料來源」標籤(**Forms** > **資料整合**)

1. 然後，Camila將選擇AEM Forms **We.gov FDM**，然後編輯&#x200B;**We.gov註冊FDM**。

1. 然後，Camila選擇要測試的&#x200B;**Contact** > **Read Service**。

   ![聯繫人閱讀服務](assets/aftia-contact-read-service.jpg)

1. 然後，Camila會為測試服務提供連絡人id，然後按一下「測試」按鈕。 例如1或2，如果您提交了表單。 如果您尚未提交表單，則不會傳回任何資料。

   ![聯繫人閱讀服務](assets/aftia-test-service.jpg)

1. 然後，Camila可驗證資料是否已成功插入資料源。

   * Derby DS中的資料類似於以下格式：

   ```xml
      [
         {
         "ADDRESS_COUNTRY": "USA",
         "LAST_NAME": "Tan",
         "ADDRESS_CITY": "New York",
         "FIRST_NAME": "Aya",
         "ADDRESS_STATE": "AL",
         "ADDRESS_LINE1": "123 Street crescent",
         "GENDER_CODE": "2",
         "ADDRESS_LINE2": "123 Street crescent",
         "ADDRESS_POSTAL_CODE": "90210",
         "BIRTH_DATE": "1991-12-12",
         "CONTACT_ID": 1,
         "MIDDLE_NAME": "M",
         "HAS_CHILDREN_CODE": "0"
         }
   ]
   ```

## （選用）Analytics(Camila){#analytics-cx-lead-camila}

**本節：** Camila會導覽至控制面板，可在控制面板中查看代理KPI的各個部分，例如開始填寫服務請求表並放棄的公民百分比、從請求提交到批准/拒絕回應的平均時間長度，以及她傳送給公民的福利手冊的參與統計資料。

### Adobe Analytics Sites報表(Camila){#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. 導覽至&#x200B;*https://&lt;aemserver>:&lt;port>/sites.html/content*
1. 選取「**AEM Forms We.Gov網站**」以檢視網站頁面。
1. 選取其中一個網站頁面（例如首頁），然後選擇「**Analytics &amp; Recommendations**」。

   ![Analytics和建議](/help/forms/using/assets/analytics_recommendation.jpg)

1. 在本頁，您會看到從Adobe Analytics擷取的與AEM Sites頁面相關的資訊(注意：設計後，此資訊會從Adobe Analytics定期重新整理，且不會即時顯示)。

   ![Adobe Analytics關鍵量度](/help/forms/using/assets/analytics_key_metrics.jpg)

1. 返回頁面檢視頁面（在步驟3存取），您也可以變更顯示設定以檢視「**清單檢視**」中的項目，以檢視頁面檢視資訊。
1. 找到「**View**」下拉菜單，然後選擇「**List View**」。

   ![「檢視」下拉式選單中的清單檢視](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. 從相同的菜單中，選擇「**View Setting**」，並從「**Analytics**」部分中選擇要顯示的列。

   ![設定欄的顯示](/help/forms/using/assets/view_setting_analytics.jpg)

1. 按一下「**Update**」以使新列可用。

   ![讓新欄可供使用](/help/forms/using/assets/new_columns_available.jpg)

### Adobe Analytics Forms報導（卡米拉）{#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. 導航到

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. 選擇「**健康福利登記申請**」最適化表單，並選擇「**Analytics報表**」選項。

   ![健康福利的註冊申請](/help/forms/using/assets/analytics_report_benefits.jpg)

1. 等候頁面載入，並檢視Analytics報表資料。

   ![Analytics報表資料](/help/forms/using/assets/analytics_report_data_updated.jpg)
