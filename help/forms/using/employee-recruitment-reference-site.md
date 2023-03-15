---
title: 員工招聘參考網站逐步說明
seo-title: Employee recruitment
description: AEM Forms參考網站會展示組織如何使用AEM Forms功能來實作員工招聘工作流程。
seo-description: AEM Forms reference site showcases how organizations can use AEM Forms features to implement employee recruitment workflow.
uuid: 27e456ba-3c08-4c43-ad54-1ba0070995ad
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f04b13e-ea40-4c86-9168-e020c52435a2
exl-id: bdfc0a20-1e98-47f9-a1d1-5af5b3ef15db
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 0%

---

# 員工招聘參考網站逐步說明 {#employee-recruitment-reference-site-walkthrough}

## 概觀 {#overview}

We.Finance是一個組織，允許候選人通過參考網站門戶申請就業。 該組織還使用門戶網站管理候選人的面試時間安排、入圍和內部溝通。 網站會管理下列項目：

* 尋找和申請工作的候選人
* 候選人的篩選和入圍
* 面試過程
* 候選詳細資訊的收集
* 候選背景檢查
* 將優惠方案轉出給選定的候選項

>[!NOTE]
>
>We.Finance和We.Gov參考站點均提供員工招聘使用案例。 逐步教學中使用的範例、影像和說明使用We.Finance參考網站。 不過，您也可以使用We.Gov執行這些使用案例並檢閱成品。 若要這麼做，請取代 **we-finance** with **we-gov** 填入。

### 涉及的工作流模型 {#workflow-models-involved}

員工招聘使用案例涉及兩個工作流：

* 面試前 — 我們為員工招聘工作流提供資金
* 面試後 — 我們為員工招聘員工面試後工作流

這些工作流程是在AEM中建立，可在下列網址找到：

`https://[authorHost]:[authorPort]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models/`

#### 我們為員工招聘工作流提供資金 {#we-finance-employee-recruiting-workflow}

以下是本文檔中遵循的「We Finance員工招聘」工作流模型。

![we-finance-employee-recliating-workflow](assets/we-finance-employee-recruiting-workflow.png)

#### 我們為員工招聘招聘後面試工作流提供資金 {#we-finance-employee-recruiting-post-interview-workflow}

以下是本文檔中遵循的「我們財務員工離職面試錄用」工作流模型。

![我們 — 財務 — 員工 — 招聘 — 面試 — 工作流](assets/we-finance-employee-recruiting-post-interview-workflow.png)

### 角色 {#personas}

此情境包含下列角色：

* 薩拉·羅斯，該組織的求職者
* 招聘人員約翰·雅可布
* 招聘經理格洛麗亞·里奧斯
* 無名氏，人力資源部

## 莎拉申請工作 {#sarah-applies-for-a-job}

莎拉·羅絲正在組織里尋找工作機會。 她訪問了他們的門戶網站，並探索了「職業」頁面上列出的職位空缺。 她找到了相符的工作清單，並申請了。

![首頁](assets/home-page.png)

We.Finance首頁

![職業頁面](assets/career-page.png)

We.財務職業頁面

Sarah按一下「在工作貼文上應用」。 作業申請表開啟。 她填寫了申請中的所有細節，並提交了。

![job-application-form](assets/job-application-form.png)

### 運作方式 {#how-it-works}

We.Finance首頁和職業頁面是AEM Sites頁面。 職業頁面內嵌最適化表單，使用可重複的面板來使用服務擷取工作空缺，並在頁面上列出。 您可以在 `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/recruitment/jobs.html`.

### 你自己看 {#see-it-yourself}

前往 `https://[publishHost]:[publishPort]/content/we-finance/global/en.html` 按一下 **[!UICONTROL 職業]**. 按一下 **[!UICONTROL 搜尋]** 填入作業清單，然後按一下 **[!UICONTROL 套用]** 找份工作。 填寫表格的詳細資訊並提交申請。

請確定您在應用程式中指定有效的電子郵件ID，因為透過此逐步說明進行的任何通訊都會傳送至指定的電子郵件ID。

## 約翰·雅可布入圍了莎拉·羅絲的招聘經理篩選簡介 {#john-jacobs-shortlists-sarah-rose-s-profile-for-the-hiring-manager-s-screening}

組織收到Sarah提交的工作申請。 招聘人員約翰·雅各布斯被指派去審核莎拉的個人檔案。 他在「AEM收件匣」中檢閱工作、找到符合工作需求的設定檔，然後按一下「入選名單」。 莎拉的個人資料被轉給招聘經理格洛麗亞·里奧斯，請她批准。

![jacobs-inbox-1](assets/jjacobs-inbox-1.png)

John的AEM收件匣

![候選者名單](assets/candidate-shortlist.png)

約翰·雅可布入圍了莎拉·羅絲的招聘經理篩選簡介

**運作方式**

「作業應用程式」表單中的提交操作會觸發工作流，該工作流在John Jacob的收件箱中建立任務以篩選應用程式。 當John審核並列入應用程式的入選名單時，工作流將在招聘經理Gloria的收件箱中建立任務。

### 你自己看 {#see-it-yourself-1}

前往 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`並使用jacobs/password作為John Jacobs的用戶名/密碼登錄。 開啟「候選人配置檔案複查」任務並填寫申請人的短名單。

## 格洛麗亞審查了申請並批准了面試申請人 {#gloria-reviews-the-application-and-approves-the-applicant-for-an-interview}

招聘經理Gloria在AEM收件箱中收到入圍的配置檔案，作為一項任務。 她審核了這份檔案，並批准了面試的候選人莎拉·羅斯。

![glorifinbox](assets/gloriainbox.png)

Gloria的AEM收件匣

![美事訪談](assets/gloriaschedulesinterview.png)

格洛麗亞批准莎拉·羅斯接受採訪

**運作方式**

當Gloria批准面試候選人時，工作流會在John Doe的AEM收件匣中建立任務，John Doe是We.Finance的招聘人員。

### 你自己看 {#see-it-yourself-2}

前往 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 並使用jacobs/password作為John Jacobs的用戶名/密碼登錄。 開啟「候選人配置檔案複查」任務並填寫申請人的短名單。

前往 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 並使用grios/password作為Gloria Rios的用戶名/密碼登錄。 開啟「候選配置檔案審閱」任務，然後按一下「計畫面試」。

## 無名氏安排了一次採訪 {#john-doe-schedules-an-interview}

John Doe在收件匣中接收排程面試的任務。 John Doe選擇並開啟任務，並將面試日期、時間、地點和負責面試的人力資源人員定為John Jacob。 John Doe按一下「發送邀請電子郵件」。 我們會向莎拉發送一封電子郵件，並為招聘經理格洛麗亞指派一項任務，以採訪莎拉。

![johnjacobeaminbox](assets/johnjacobsaeminbox.png)

John Doe的AEM收件匣

![約翰·杜斯·杜達訪談](assets/johndoescheduleinterview.png)

無名氏安排了面試時間，並將細節發送給莎拉·羅斯

## 莎拉·羅絲收到的郵件有面試時間表 {#sarah-rose-receives-the-email-with-interview-schedule}

莎拉·羅絲收到的電子郵件包括面試時間表、地點和其他細節。 她按一下「接受」，表示她對面試日程和地點沒問題。 在精確資訊的指導下，莎拉去面試了。

![薩拉赫羅塞普馬爾](assets/sarahroseinterviewemail.png)

莎拉·羅絲接受了採訪

## 採訪結束後，招聘經理的入圍者莎拉·羅斯 {#after-the-interviews-the-hiring-manager-shortlists-sarah-rose}

在莎拉·羅絲完成面試並清除面試後，招聘經理格洛麗亞·里奧斯從收件箱中開啟「候選人選擇」任務，然後按一下「選擇」。 Gloria Rios的決定被傳達給人力資源部人員John Doe，以供進一步處理。

![格洛里亞辛波](assets/gloriariosinboxoffer.png)

Gloria的AEM收件匣

![格洛里亞羅塞克](assets/gloriariosselectcandidate.png)

格洛麗亞·里奧斯在採訪後選擇莎拉·羅斯

## John Doe要求更多資訊 {#john-doe-requests-more-information}

在請求候選人加入該組織之前，需要檢查她的背景。 John Doe開啟並審查了選定申請人的詳細資訊，發現她的一些就業和教育細節尚未填寫。 無名氏點按需要更多資訊。

![johndoinbox](assets/johndoeinbox.png) ![johneneedmore資訊](assets/johndoeneedmoreinformation.png)

John Doe向Sarah Rose索取更多有關她的教育和工作經驗的資訊

## 莎拉·羅絲收到一封電子郵件，要求進一步的資訊 {#sarah-rose-receives-an-email-requesting-further-information}

Sarah Rose收到一封電子郵件，通知她需要進一步的資訊來處理她的就業申請。 電子郵件包含表單的連結，以填寫所需資訊。

![sarahroseemailmoredetails](assets/sarahroseemailmoredetails.png)

Sarah Rose收到一封電子郵件，通知需要進一步資訊來處理她的就業申請

Sarah按一下電子郵件中的「提供詳細資訊」連結。 表單隨即出現。 Sarah按照John Doe的要求填寫所需的教育和就業詳細資訊，並按一下「提交」。

![additionalinformation1](assets/additionalinformation1.png)

Sarah按一下電子郵件中的連結以開啟其他資訊表單

![additionalinformation2](assets/additionalinformation2.png)

Sarah會按照John Doe的要求填充其他資訊，然後按一下「提交」

## John Doe會查看所選候選配置檔案，以獲取提供的附加資訊 {#john-doe-reviews-the-selected-candidate-profile-for-the-additional-information-provided}

John Doe會選取候選審核請求並開啟它。 無名氏發現莎拉已按要求填寫了所有資訊。 檢閱應用程式後，John Doe按一下「核准」。 經無名氏批准，對莎拉·羅絲進行背景調查的請求將轉發給約翰·雅可布。

![johndoadditionalinformationinbox](assets/johndoeadditionainformationinbox.png)

John Doe的AEM收件匣

![johndoadditionalinformationreview-copy](assets/johndoeadditionalinformationreview-copy.png)

John Doe審核了Sarah提供的附加資訊並批准了該資訊

## 約翰·雅各布收到背景檢查請求 {#john-jacobs-receives-a-background-check-request}

約翰·雅可布在收件匣中看到背景檢查請求。 約翰·雅可布開啟了工作，並回顧了莎拉·羅斯提供的資訊。 進行背景檢查後，John Jacobs按一下「繼續」以表示背景檢查已成功。

![johnobsbackgroundcheckbox](assets/johnjacobsbackgroundcheckinbox.png)

約翰·雅可布的AEM收件匣

![johnjacobsbackgroundcheckaed](assets/johnjacobsbackgroundcheckgoahead.png)

執行背景檢查後，John Jacobs點擊了Go Aeak

## 無名氏把加入信寄給莎拉·羅絲 {#john-doe-sends-out-the-joining-letter-to-sarah-rose}

John Doe收到其AEM收件匣中傳送加入信的請求。 John會開啟請求並檢視詳細資訊。 John Doe附加了加入信函PDF，然後按一下「附加併發送加入信函」。

![johnjoiningletterinbox](assets/johndoejoiningletterinbox.png)

John Doe的AEM收件匣

![johndojoiningletterattachandsend](assets/johndoejoiningletterattachandsend.png)

無名氏發出加入信供簽署

## 莎拉·羅絲收到並簽署了加入信 {#sarah-rose-receives-and-signs-the-joining-letter}

莎拉·羅絲收到了簽名的聯名信。 Sarah按一下這裡以檢閱並簽署加入信。 將開啟連接信函PDF，其中包含一個欄位以簽署文檔。

![sarahrosejoiningletteremail](assets/sarahrosejoiningletteremail.png)

莎拉·羅絲收到了簽名的聯名信

Sarah可以選擇輸入、使用Draw來手寫、插入簽名影像，或者使用手機的觸摸屏來繪製簽名。 Sarah在名稱中鍵入，按一下「按一下以簽名」，然後下載加入信函的簽名副本。

![sarahrosejoiningletter](assets/sarahrosejoininglettersign.png)

Sarah在她的名字上輸入，以簽署加入信

![sarahrosejoininglettersign2](assets/sarahrosejoininglettersign2.png)

Sarah按一下「按一下以簽署」以完成加入信的簽名
