---
title: We.Gov參考網站逐步說明
seo-title: We.Gov參考網站逐步說明
description: 使用虛構的使用者和群組，使用We.Gov示範套件來執行AEM Forms工作。
seo-description: 使用虛構的使用者和群組，使用We.Gov示範套件來執行AEM Forms工作。
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# We.Gov參考網站逐步說明{#we-gov-reference-site-walkthrough}

## 先決條件 {#pre-requisites}

依照設定和設定We.Gov參考網 [站中所述設定參考網站](../../forms/using/forms-install-configure-gov-reference-site.md)。

## 使用者動態 {#user-story}

* AEM Forms

   * 資料擷取
   * 資料整合(MS Dynamics)
   * Adobe Sign

* 工作流程
* 客戶溝通

   * Print Channel
   * Web Channel

* Adobe Analytics

### Fictitious users and groups {#fictitious-users-and-groups}

We.Gov示範套件隨附下列內建虛擬使用者：

* **譚雅**:符合政府機關服務資格的公民

![虛擬使用者](/help/forms/using/assets/aya_tan_new.png)

* **喬治·朗**:We.Gov機構商業分析師

![虛擬使用者](/help/forms/using/assets/george_lang.png)

* **卡米拉·桑托斯**:We.Gov Agency CX領導

![虛擬使用者](/help/forms/using/assets/camila_santos.png)

也包含下列群組：

* **We.Gov Forms使用者**

   * 喬治·朗（成員）
   * 卡米拉·桑托斯（成員）

* **We.Gov使用者**

   * 喬治·朗（成員）
   * 卡米拉·桑托斯（成員）
   * 譚雅雅（會員）

### 示範概觀詞語圖例 {#demo-overview-terms-legend}

1. **模擬**:在AEM展示中定義的使用者與群組。
1. **按鈕**:彩色矩形或環繞的箭頭，以進行導覽。
1. **按一下**:執行使用者動態中的動作。
1. **連結**:位於We.Gov網站主功能表頂端。
1. **使用者指示**:瀏覽使用者動態時要遵循的一組數值步驟。
1. **表單入口網站**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **Mobile View**:We.Gov使用者可使用重新調整大小的瀏覽器來複製行動檢視。
1. **案頭檢視**:We.gov使用者可在膝上型電腦或桌上型電腦上檢視示範。
1. **預螢幕擷取表單**:We.Gov網站首頁的表格。
1. **最適化表單**:We.gov示範的註冊申請表。

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Adobe We.Gov網站**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Adobe收件匣**:位於AEM後端的 [頂端功能表列] 「Bell」圖示。

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **電子郵件客戶**:檢視電子郵件的偏好方式(Gmail、Outlook)
1. **CTA**:行動要求
1. **導覽**:在瀏覽器頁面上找到特定的參考點。

## 行動裝置檢視示範 {#mobile-view-demo}

**本節必須在演示之前執行。**

**使用者指示：**

1. 導覽至： *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. 登入方式：

   1. **使用者**:aya.tan
   1. **密碼**:密碼

1. 重新調整瀏覽器視窗大小或使用瀏覽器模擬器來複製行動裝置大小。

### Aya User Story（We.Gov網站） {#aya-user-story-we-gov-website}

![虛擬使用者](/help/forms/using/assets/aya_tan_new-1.png)

**本節**:阿亞是公民。 她從朋友那裡得知，她可能符合從政府機關獲得服務的資格。 Aya從手機瀏覽到We.Gov網站，進一步瞭解她有資格獲得的服務。

### Aya User Story（We.Gov預檢程式） {#aya-user-story-we-gov-pre-screener}

Aya在手機上填寫簡短的調適性表格，回答幾個問題以確認她是否符合資格。

**使用者指示：**

1. 在每個下拉式欄位中進行選取。

   1. 注意：如果使用者每年的收入超過$200,000，則無法享有此優惠。

1. 按一下「我&#x200B;**是否符合資格？**” 按鈕.
1. 按一下「**立即套用**」按鈕繼續。

   ![立即套用連結](/help/forms/using/assets/apply_now_link.png)

### Aya使用者動態（We.Gov調適性表單） {#aya-user-story-we-gov-adaptive-form}

Aya發現她符合資格，並開始填寫申請表，要求在行動裝置上提供服務。

Aya需要先在家中審閱一些檔案，才能完成服務請求申請。 她儲存並退出應用程式。

**使用者指示：**

1. 填寫「基本資訊」欄位，以下是必填欄位和下拉式清單：

   1. 基本資訊

      1. 名字
      1. 中間名
      1. 姓氏
      1. 首選名稱
      1. DOB
      1. 性別
   1. 連絡人資訊

      1. 街道地址
      1. 城市
      1. 電話號碼
      1. 郵遞區號
      1. 電子郵件
      1. 狀態
   1. 軍事狀態

      1. 家庭狀態



1. 使用下列動 **態邏輯** ，使用「族狀態」下拉式清單來展 **示動態功能** :

   1. **單一**:顯示親屬面板旁邊
   1. **已婚**:顯示婚姻相關面板
   1. **離婚**:顯示親屬面板旁邊
   1. **寡居**:顯示親屬面板旁邊
   1. **你有孩子嗎？**:（是／否）選項按鈕以顯示子依存面板。

      1. （新增／移除）按鈕，以新增／移除多個子系相依面板。

1. 按一下灰色選單列中的向右箭頭。
1. 按一下底部的「儲存」按鈕。

   ![最適化表單詳細資訊](/help/forms/using/assets/adaptive_form.png)

## 案頭示範 {#desktop-demo}

**** 本節：回到家後，Aya找到了她需要的資訊，並從她的案頭恢復了申請。 Aya導覽至線上表單入口網站，以繼續申請。 透過一些簡單的自訂功能，機構也可以自動產生連結並以電子郵件傳送，以繼續執行應用程式。

### Aya使用者動態（續的最適化表單） {#aya-user-story-continued-adaptive-form}

**使用者指示：**

1. 導覽至 *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. 在導覽列中，按一下「線&#x200B;**上服務**」。
1. 從「草稿表單」面板中，選取現有的「健康福利註冊申請表」。

   ![健康福利註冊申請](/help/forms/using/assets/enrollment_application.png)

   外觀和感覺都一樣，她不需要重新輸入任何資料。

   **使用者指示：**

1. 按一下右鍵「社交圈CTA」，移至下一節。

   ![右圓CTA](/help/forms/using/assets/right_circle_cta_new.png)

   表單會填入到Aya最後一個登入點。 Aya已經輸入了她的所有資訊，準備提交。

   ![提交最適化表單](/help/forms/using/assets/submit_adaptive_form.png)

   送出Aya後，會收到她開啟並準備使用Adobe Sign進行電子簽署的電子郵件。

**使用者指示：**

1. 在提交後，將顯示感謝頁面。
1. 導覽至您的電子郵件用戶端並尋找Adobe Sign電子郵件。
1. 按一下Adobe Sign的連結。

   ![Adobe sign連結](/help/forms/using/assets/adobe_sign_link.png)

**使用者指示：**

1. 勾選「我&#x200B;**同意**」方塊。
1. 按一下「**接受**」。
1. 捲動至已審閱檔案的底部。
1. 按一下反白顯示的黃色標籤，以簽署檔案。

   ![簽署檔案](/help/forms/using/assets/sign_document_new.png)![簽署測試檔案](/help/forms/using/assets/sign_test_document.png)

## 政府機關代理人(George) {#government-agent-george}

![政府代理人喬治](/help/forms/using/assets/george_lang-1.png)

**** 本節：喬治是政府機關Aya的商業分析師，向Aya請求服務。 George有一個儀表板，他可以在其中查看所有指派給他進行審查的服務請求應用程式。

### George User Story（AEM收件匣） {#george-user-story-aem-inbox}

**使用者指示：**

1. 導覽至 *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. 按一下使用者圖示（右上角），並使用「登出」或「**Impersonate as******」功能表選項（如果您目前與管理使用者登入）。

   1. 登入方式：

      1. **** 使用者：george.lang
      1. **** 密碼：密碼
   1. 或模擬：

      1. 在「**Impersonate as**」(模&#x200B;**擬為**)欄位中輸入「George」。

      1. 按一下「確定」以模擬。


1. 從右上角按一下「通知（鈴鐺）」圖示。
1. 按一下「**全部檢視**」以導覽至「收件匣」。
1. 從「收件箱」中，開啟最新的「**Health Benefits Application Review**」（健康優勢應用程式審核）任務。

   ![Health Benefits Application Review](/help/forms/using/assets/health_benefits.png)

### George User Story（AEM收件匣和MS Dynamics） {#george-user-story-aem-inbox-and-ms-dynamics}

由於資料整合和自動化工作流程，Aya的應用程式會出現，而且會在提交資料時自動產生CRM記錄。

**使用者指示：**

1. 開啟並檢查唯讀最適化表單。
1. 按一下「**Open MS Dynamics**」（開啟MS Dynamics）按鈕，在新窗口中開啟MS Dynamics記錄。
1. 在CRM中，您可以看到所有資訊都可以更新

   1. （可選）直接在Dynamics中新增一些審核附註。

1. 關閉並返回AEM收件匣。

   ![MS Dynamics記錄](/help/forms/using/assets/ms_dynamics.png)

### George User Story（返回AEM收件箱） {#george-user-story-back-to-aem-inbox}

George核准Aya的應用程式，而且由於現有的自動化工作流程，確認電子郵件也會傳送至Aya。

**使用者指示：**

1. 導覽至左上角，然後按一下「**核准**」以核准應用程式。
1. 在該模型中，您可以留下一條CX銷售線索消息。
1. 按一下「完成」。
1. （公民角色）開啟您的電子郵件用戶端，以檢視傳送至Aya的電子郵件。

   ![檢視傳送至Aya的電子郵件](/help/forms/using/assets/email_client.png)

## CX銷售線索(Camila) {#cx-lead-camila}

![Camila（CX銷售線索）](/help/forms/using/assets/camila_santos-1.png)

**** 本節：CX Lead與Aya打了歡迎電話，以說明如何利用她獲得批准的政府服務。

### Camila使用者動態（AEM收件匣與MS Dynamics） {#camila-user-story-aem-inbox-ms-dynamics}

**使用者指示：**

1. 導覽至 *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. 按一下使用者圖示（右上角），並使用「登出」或「**Impersonate as******」功能表選項（如果您目前與管理使用者登入）。

   1. 登入方式：

      1. **使用者**:camila.santos
      1. **密碼**:密碼
   1. 或模擬：

      1. 在「**Impersonate as**」欄位中輸&#x200B;**入「Camila**」。

      1. 按一下「確定」以模擬。


1. 從右上角按一下「通知（鈴鐺）」圖示。
1. 按一下「**全部檢視**」以導覽至「收件匣」。
1. 從「收件箱」中，開啟最新的「**新聯繫人批准**」任務。

   ![新連絡人核准](/help/forms/using/assets/new_contact_approval.png)

   **使用者指示：**

1. 開啟並檢查唯讀最適化表單。
1. 按一下「**Open MS Dynamics**」（開啟MS Dynamics）按鈕，在新窗口中開啟MS Dynamics記錄。
1. 在CRM中，您可以看到所有資訊都可以更新

   1. （可選）直接在Dynamics中新增呼叫活動。
   1. 開啟「活&#x200B;**動**」區段。
   1. 按一下「新&#x200B;**電話呼叫**」選項。
   1. 添加電話呼叫詳細資訊。
   1. 保存並關閉窗口。

1. 返回AEM，導覽至左上角，然後按一下「**Submit**」以送出應用程式。
1. 在模型中，您可以留言。
1. 按一下「完成」。

   ![「活動」頁籤](/help/forms/using/assets/activities_tab.png) 「確 ![認新聯繫人」](/help/forms/using/assets/confirm_new_contact.png)

## 歡迎Kit公民(Aya) {#welcome-kit-citizen-aya}

**** 本節：Aya收到一封電子郵件，其中包含互動式通訊的連結，可摘要她的優點，並包含要填寫的表格欄位。 附上PDF優點陳述並連結至電子郵件中的互動式通訊信件（與互動式通訊具有相同的主題／品牌）。

### Aya使用者動態（電子郵件用戶端） {#aya-user-story-email-client}

**使用者指示：**

1. 找到並開啟歡迎套件電子郵件。
1. 捲動至頁面底部的PDF附件。
1. 按一下以開啟PDF附件。
1. 在電子郵件用戶端中捲動並按一下「線&#x200B;**上檢視歡迎套件**」。

   1. 這會開啟相同檔案的Web頻道版本。

1. 若要直接參考PDF:

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. 直接參考IC:

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![歡迎權益手冊](/help/forms/using/assets/welcome_benefits_handbook.png)![互動式通訊連結](/help/forms/using/assets/interactive_communication.png)

## 續約提醒公民(Aya) {#renewal-reminder-citizen-aya}

**** 本節：卡米拉還安排了一個通訊提醒，這樣一來，一年後。 （自動化／執行及以電子郵件傳送的工作流程步驟）。

### Aya使用者動態（電子郵件用戶端） {#aya-user-story-email-client-1}

**使用者指示：**

1. 導覽至您的電子郵件客戶端。
1. 找到並開啟續約提醒電子郵件。
1. 按一下「提&#x200B;**交新應用程式**」按鈕以開啟最適化表單。

   1. 此區段故意留空，以支援階段2中的資料預先填寫。
   ![續約提醒電子郵件](/help/forms/using/assets/renewal_reminder_email.png)

## Analytics CX銷售線索(Camila) {#analytics-cx-lead-camila}

**** 本節：Camila導覽至儀表板，可在其中查看機構KPI，例如開始填寫服務申請表並放棄的公民百分比、從申請提交到批准／拒絕回應的平均時間，以及她寄送給公民的福利手冊的參與統計資料。

### Camila評論網站報告(We.Gov Adobe Analytics) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. 導覽至 *https://&lt;aemserver>:&lt;port>/sites.html/content*
1. 選取「**AEM Forms We.Gov網站**」以檢視網站頁面。
1. 選取其中一個網站頁面（例如首頁），然後選擇「**Analytics &amp; Recommendations**」。

   ![分析與建議](/help/forms/using/assets/analytics_recommendation.jpg)

1. 在此頁面上，您會看到從Adobe Analytics擷取的與AEM Sites頁面相關的資訊(注意：設計時，會定期從Adobe Analytics重新整理此資訊，而不會即時顯示)。

   ![Adobe Analytics關鍵量度](/help/forms/using/assets/analytics_key_metrics.jpg)

1. 回到頁面檢視頁面（在步驟3.中存取），您也可以變更顯示設定，以檢視「清單檢視」中的項目，以檢&#x200B;**視頁面檢視**。
1. 找到「**View**」下拉式功能表，並選&#x200B;**取「List View**」。

   ![「檢視」下拉式選單中的清單檢視](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. 從相同功能表中，選取「**檢視設定**」，並從「**Analytics**」區段中選取您要顯示的欄。

   ![設定欄的顯示](/help/forms/using/assets/view_setting_analytics.jpg)

1. 按一下「**更新**」，讓新欄可供使用。

   ![讓新欄可供使用](/help/forms/using/assets/new_columns_available.jpg)

### Camila評論表單報表(We.Gov Adobe Analytics) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. 導航到

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. 選取「健康&#x200B;**福利的註冊申請**」調適性表單，並選取「**Analytics報表**」選項。

   ![健康福利註冊申請](/help/forms/using/assets/analytics_report_benefits.jpg)

1. 等待頁面載入，並檢視Analytics報表資料。

   ![Analytics報表資料](/help/forms/using/assets/analytics_report_data_updated.jpg)

