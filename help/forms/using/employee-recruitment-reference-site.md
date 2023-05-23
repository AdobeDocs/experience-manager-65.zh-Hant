---
title: 員工招聘參考站點巡查
seo-title: Employee recruitment
description: AEM Forms參考網站展示了組織如何使用AEM Forms功能來實施員工招聘工作流。
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

# 員工招聘參考站點巡查 {#employee-recruitment-reference-site-walkthrough}

## 概觀 {#overview}

We.Finance是一個組織，允許候選人通過參考網站門戶申請就業。 該組織還使用門戶來管理候選人的面試安排、入圍和內部溝通。 該站點管理以下內容：

* 搜索和申請工作的候選人
* 候選人的篩選和入圍
* 面試流程
* 候選人詳細資訊的集合
* 候選背景檢查
* 向選定候選人推出聘用

>[!NOTE]
>
>We.Finance和We.Gov參考站點都提供員工招聘使用案例。 演示中使用的示例、影像和說明使用We.Finance參考站點。 但是，您也可以使用We.Gov運行這些使用案例並查看項目。 為此，請替換 **我們金融** 與 **韋戈夫** 的子菜單。

### 涉及的工作流模型 {#workflow-models-involved}

員工招聘使用案例包括兩個工作流：

* 面試前 — 我們為員工招聘工作流融資
* 面試後 — 我們為員工招聘後面試工作流提供資金

這些工作流是在中創AEM建的，可在以下位置找到：

`https://[authorHost]:[authorPort]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models/`

#### 我們為員工招聘工作流提供融資 {#we-finance-employee-recruiting-workflow}

以下是本文檔中遵循的「我們財務員工招聘」工作流模型。

![員工招聘工作流](assets/we-finance-employee-recruiting-workflow.png)

#### 我們為員工招聘後面試工作流提供資金 {#we-finance-employee-recruiting-post-interview-workflow}

以下是本文檔中遵循的「我們財務員工後面試招聘」工作流模型。

![我們財務 — 員工 — 招聘 — 面試 — 工作流](assets/we-finance-employee-recruiting-post-interview-workflow.png)

### 人物 {#personas}

該方案涉及以下角色：

* 莎拉·羅斯，該組織的應聘者
* 招聘人員約翰·雅各布斯
* 格洛麗亞·里奧斯，招聘經理
* 無名氏，人力資源部

## 莎拉申請一份工作 {#sarah-applies-for-a-job}

莎拉·羅絲正在組織里尋找工作機會。 她訪問了他們的門戶網站，並瀏覽了「職業生涯」頁面上列出的職位空缺。 她找到了一份匹配的工作清單，並申請了。

![首頁](assets/home-page.png)

We.Finance首頁

![職業版](assets/career-page.png)

We.Finance職業頁

Sarah按一下Apply on a job posting（在職務發佈時應用）。 將開啟作業申請表。 她填寫申請中的所有詳細資訊並提交。

![作業申請表](assets/job-application-form.png)

### 它的工作原理 {#how-it-works}

We.Finance首頁和職業版是AEM Sites頁。 職業生涯頁面嵌入了適應性表單，該表單使用可重複面板來使用服務獲取職位空缺並在頁面上列出這些職位空缺。 可以在以下位置查看自適應表單 `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/recruitment/jobs.html`。

### 親眼看看 {#see-it-yourself}

轉到 `https://[publishHost]:[publishPort]/content/we-finance/global/en.html` 按一下 **[!UICONTROL 職業]**。 按一下 **[!UICONTROL 搜索]** 填充作業清單，然後按一下 **[!UICONTROL 應用]** 找份工作。 在表單中填寫詳細資訊並提交申請。

確保在應用程式中指定有效的電子郵件ID，因為通過此步驟的任何通信都將發送到指定的電子郵件ID。

## 約翰·雅各布斯入圍了莎拉·羅絲的招聘經理招聘簡介 {#john-jacobs-shortlists-sarah-rose-s-profile-for-the-hiring-manager-s-screening}

組織接收Sarah提交的工作申請。 招聘人員約翰·雅各布斯被派去審核莎拉的檔案。 他在收件箱中查看任AEM務，查找與作業要求匹配的配置檔案，然後按一下「快捷方式清單」。 莎拉的檔案被轉給招聘經理格洛麗亞·里奧斯，由她審批。

![jjacobs收件箱–1](assets/jjacobs-inbox-1.png)

約翰的收件箱AEM

![候選人候選名單](assets/candidate-shortlist.png)

約翰·雅各布斯入圍了莎拉·羅絲的招聘經理招聘簡介

**它的工作原理**

「作業申請」表單中的提交操作會觸發一個工作流，該工作流在John Jacob收件箱中建立一個任務以篩選應用程式。 當John查看並列出應用程式的快捷方式時，工作流會在聘用經理Gloria的收件箱中建立一個任務。

### 親眼看看 {#see-it-yourself-1}

轉到 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`使用jjacobs/password作為John Jacobs的用戶名/密碼登錄。 開啟「候選人配置檔案複查」任務，並列出申請人。

## 格洛麗亞審查申請並批准面試申請人 {#gloria-reviews-the-application-and-approves-the-applicant-for-an-interview}

招聘經理Gloria在收件箱中將入圍的個人資料作為一項任AEM務接收。 她審核了，並批准了候選人莎拉·羅斯的面試。

![榮耀收件箱](assets/gloriainbox.png)

格洛麗亞的收AEM件箱

![華麗的日程面談](assets/gloriaschedulesinterview.png)

格洛麗亞批准莎拉·羅絲接受採訪

**它的工作原理**

當Gloria批准面試候選人時，工作流會在John Doe的收件箱中建立一個任務AEM,John Doe是We.Finance的招聘人員。

### 親眼看看 {#see-it-yourself-2}

轉到 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 使用jjacobs/password作為John Jacobs的用戶名/密碼登錄。 開啟「候選人配置檔案複查」任務，並列出申請人。

轉到 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 並使用grios/password作為Gloria Rios的用戶名/密碼登錄。 開啟「候選人配置檔案複查」任務，然後按一下「計畫面試」。

## 無名氏安排一個 {#john-doe-schedules-an-interview}

John Doe在收件箱中接收安排面試的任務。 John Doe選擇並開啟任務，並將面試日期、時間、地點以及負責面試的HR人員確定為John Jacob。 John Doe按一下「發送邀請電子郵件」。 向薩拉發送一封電子郵件，並為招聘經理格洛麗亞分配一項任務，以面試薩拉。

![約翰·雅各布納](assets/johnjacobsaeminbox.png)

無名氏收件箱AEM

![約翰·杜斯切杜訪談](assets/johndoescheduleinterview.png)

無名氏安排面試時間，把細節發給莎拉·羅絲

## 莎拉·羅絲收到一封帶面試時間表的電子郵件 {#sarah-rose-receives-the-email-with-interview-schedule}

莎拉·羅絲收到這封電子郵件，內容包括面試時間表、地點和其他細節。 她按一下「接受」，表示她對面試日程和地點沒有問題。 根據確切的資訊，莎拉參加了面試。

![沙羅斯受訪者郵件](assets/sarahroseinterviewemail.png)

莎拉·羅絲收到面試日程

## 面試結束後，招聘經理候選人莎拉·羅斯 {#after-the-interviews-the-hiring-manager-shortlists-sarah-rose}

在Sarah Rose完成訪談並清除訪談後，招聘經理Gloria Rios會從收件箱中開啟「候選人選擇」任務，然後按一下「選擇」。 Gloria Rios的決定被轉交人力資源部人員John Doe，供進一步處理。

![格洛里辛波克斯](assets/gloriariosinboxoffer.png)

格洛麗亞的收AEM件箱

![新選人](assets/gloriariosselectcandidate.png)

格洛麗亞·里奧斯在面試後選擇莎拉·羅斯

## John Doe請求更多資訊 {#john-doe-requests-more-information}

在要求候選人加入組織之前，需要檢查她的背景。 John Doe開啟並查看選定申請人的詳細資訊，發現她的一些就業和教育詳細資訊尚未填寫。 無名氏點擊需要更多資訊。

![約翰·道因博](assets/johndoeinbox.png) ![約翰·尼德莫雷資訊](assets/johndoeneedmoreinformation.png)

無名氏要求莎拉·羅絲提供更多關於她的教育和工作經驗的資訊

## 莎拉·羅斯收到一封電子郵件，要求進一步 {#sarah-rose-receives-an-email-requesting-further-information}

Sarah Rose收到一封電子郵件，通知她處理她的就業申請需要進一步的資訊。 該電子郵件包括到表單的連結，用於填寫所需資訊。

![沙羅·史密莫勒細節](assets/sarahroseemailmoredetails.png)

Sarah Rose收到一封電子郵件，通知需要進一步的資訊才能處理她的就業申請

Sarah按一下電子郵件中的「提供詳細資訊」連結。 將出現一個窗體。 Sarah按John Doe的要求填寫所需的教育和雇傭詳細資訊，然後按一下「提交」。

![additionalinformation1](assets/additionalinformation1.png)

Sarah通過按一下電子郵件中的連結開啟附加資訊表單

![additionalinformation2](assets/additionalinformation2.png)

Sarah按John Doe的要求填寫其他資訊，然後按一下「提交」

## John Doe查看所選候選人配置檔案，瞭解提供的其他資訊 {#john-doe-reviews-the-selected-candidate-profile-for-the-additional-information-provided}

John Doe選擇候選審閱請求並開啟它。 無名氏發現莎拉已經按要求填寫了所有資訊。 審閱應用程式後，John Doe按一下「批准」。 經無名氏批准，對莎拉·羅斯進行背景調查的請求被轉給約翰·雅各布斯。

![約翰多附加資訊收件箱](assets/johndoeadditionainformationinbox.png)

無名氏收件箱AEM

![johndoeadditionalinformationreviewcopy（約翰多附加資訊審閱副本）](assets/johndoeadditionalinformationreview-copy.png)

John Doe查看Sarah提供的其他資訊並批准

## 約翰·雅各布斯收到背景調查請求 {#john-jacobs-receives-a-background-check-request}

約翰·雅各布斯在收件箱裡看到了背景檢查請求。 約翰·雅各布斯開啟了這項任務，並回顧了莎拉·羅絲提供的資訊。 在執行背景檢查後，John Jacobs按一下「Go Aew」（繼續）以表示背景檢查已成功。

![約翰·卡布斯背景棋](assets/johnjacobsbackgroundcheckinbox.png)

約翰·雅各布斯的收AEM件箱

![約翰·雅各布斯背後對決](assets/johnjacobsbackgroundcheckgoahead.png)

在執行背景檢查後，John Jacobs按一下Go Aeak（繼續）

## 無名氏把加入信寄給莎拉·羅絲 {#john-doe-sends-out-the-joining-letter-to-sarah-rose}

John Doe收到收件箱中AEM的發送加入信的請求。 John開啟請求並查看詳細資訊。 John Doe附加連接信函PDF，然後按一下「附加併發送連接信函」。

![約翰松信箱](assets/johndoejoiningletterinbox.png)

無名氏收件箱AEM

![約翰德加入信函附件](assets/johndoejoiningletterattachandsend.png)

無名氏將加入信寄出

## 莎拉·羅斯收到並簽署加入信 {#sarah-rose-receives-and-signs-the-joining-letter}

莎拉·羅斯收到簽名的加入信。 Sarah按一下這裡查看並簽署加入信。 連接字母PDF開啟，並帶有用於簽署文檔的欄位。

![沙拉氏連體信件](assets/sarahrosejoiningletteremail.png)

莎拉·羅斯收到了加入信

Sarah可以選擇輸入、使用繪圖進行手寫、插入簽名影像或使用手機的觸摸屏繪製簽名。 Sarah以她的名字鍵入，按一下「按一下以簽名」，然後下載加入信的簽名副本。

![莎拉羅斯連字元](assets/sarahrosejoininglettersign.png)

薩拉在名字中鍵入來簽署加入信

![sarahrosejoininglettersign2](assets/sarahrosejoininglettersign2.png)

Sarah按一下「按一下以簽名」以完成對加入信的簽名
