---
title: 與Adobe Target整合的先決條件
seo-title: 與Adobe Target整合的先決條件
description: 瞭解與Adobe Target整合的必要條件。
seo-description: 瞭解與Adobe Target整合的必要條件。
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---


# 與Adobe Target整合的先決條件{#prerequisites-for-integrating-with-adobe-target}

在[整合AEM和Adobe Target時，您必須向Adobe Target註冊、設定複製代理，以及在發佈節點上保護活動設定。](/help/sites-administering/target.md)

## 向Adobe Target註冊{#registering-with-adobe-target}

若要將AEM與Adobe Target整合，您必須擁有有效的Adobe Target帳戶。 此帳戶至少必須具有&#x200B;**approver**&#x200B;級別權限。 當您向Adobe Target註冊時，會收到用戶端代碼。 您需要用戶端程式碼和Adobe Target登入名稱及密碼，才能將AEM連接至Adobe Target。

「用戶端代碼」會在呼叫Adobe Target伺服器時識別Adobe Target客戶帳戶。

>[!NOTE]
>
>您的帳戶也必須由Target團隊啟用，才能使用整合。
>
>如果不是這樣，請聯絡[Adobe客戶服務](https://docs.adobe.com/content/help/en/target/using/cmp-resources-and-contact-information.html)。

## 啟用目標複製代理{#enabling-the-target-replication-agent}

必須在作者實例上啟用Test和Target [複製代理](/help/sites-deploying/replication.md)。 請注意，如果您使用[nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent)執行模式來安裝AEM，此複製代理預設不會啟用。 有關保護生產環境的詳細資訊，請參閱[安全檢查清單](/help/sites-administering/security-checklist.md)。

1. 在AEM首頁上，按一下或點選「工具&#x200B;**** > **部署** > **複製**」。
1. 按一下或按一下「**Agents On Author**」。
1. 按一下或點選&#x200B;**Test and Target(test and target)**&#x200B;複製代理，然後按一下或點選&#x200B;**Edit**。
1. 選擇「Enabled（啟用）」選項，然後按一下或點選&#x200B;**OK**。

   >[!NOTE]
   >
   >配置Test和Target複製代理時，在&#x200B;**Transport**&#x200B;頁籤中，URI預設設定為&#x200B;**tnt:///**。 請勿將此URI替換為&#x200B;**https://admin.testandtarget.omniture.com**。
   >
   >請注意，如果您嘗試使用&#x200B;**tnt:///**&#x200B;測試連線，則會擲回錯誤。 這是預期行為，因為此URI僅供內部使用，不應與&#x200B;**測試連接**&#x200B;一起使用。

## 保護活動設定節點{#securing-the-activity-settings-node}的安全

您必須保護發佈例項上的活動設定節點&#x200B;**cq:ActivitySettings**，讓一般使用者無法存取。 處理Adobe Target活動同步的服務只能訪問活動設定節點。

**cq:ActivitySettings**&#x200B;節點可在`/content/campaigns/*nameofbrand*`* *下的CRXDE lite中使用，在activity jcr:content node;* *例如`/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`下。 此節點僅在您定位元件後建立。

**cq:ActivitySettings**&#x200B;節點位於活動的jcr:content下，受以下ACL的保護：

* 拒絕所有人
* 允許jcr:read,rep:write for &quot;target-activity-authors&quot;（author是此群組的成員，立即可用）
* 允許jcr:read,rep:write for &quot;targetservice&quot;

這些設定可確保普通用戶沒有對節點屬性的訪問權限。 對作者和發佈使用相同的ACL。 如需詳細資訊，請參閱[使用者管理與安全性](/help/sites-administering/security.md)。

## 設定AEM Link Externalizer {#configuring-the-aem-link-externalizer}

在Adobe Target中編輯活動時，URL會指向&#x200B;**localhost**，除非您變更AEM作者節點上的URL。 如果您想要匯出的內容指向特定的&#x200B;*publish*&#x200B;網域，可以設定「AEM Link Externalizer」。

>[!NOTE]
>
>另請參閱[添加雲配置](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)。

若要設定AEM外部化：

>[!NOTE]
>
>如需詳細資訊，請參閱[將URL外部化](/help/sites-developing/externalizer.md)。

1. 導覽至位於&#x200B;**https://&lt;server>的OSGi Web控制台：&lt;port>/system/console/configMgr.**
1. 尋找&#x200B;**Day CQ Link Externalizer**，並輸入作者節點的網域。

   ![chlimage_1-120](assets/aem-externalizer-01.png)

