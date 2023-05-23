---
title: 與Adobe Target整合的先決條件
seo-title: Prerequisites for Integrating with Adobe Target
description: 瞭解與Adobe Target整合的先決條件。
seo-description: Find out about the prerequisites for integrating with Adobe Target.
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---

# 與Adobe Target整合的先決條件{#prerequisites-for-integrating-with-adobe-target}

作為 [融AEM合Adobe Target](/help/sites-administering/target.md)，您需要向Adobe Target註冊，配置複製代理，並在發佈節點上安全活動設定。

## 註冊Adobe Target {#registering-with-adobe-target}

要與AEMAdobe Target整合，您必須擁有有效的Adobe Target帳戶。 此帳戶必須 **批准者** 至少級別權限。 在Adobe Target註冊時，您會收到客戶代碼。 您需要客戶端代碼和Adobe Target登錄名和密碼才能連AEM接到Adobe Target。

客戶端代碼在呼叫Adobe Target伺服器時標識Adobe Target客戶帳戶。

>[!NOTE]
>
>您的帳戶還必須由目標團隊啟用才能使用整合。
>
>如果不是，請聯繫 [Adobe客戶關懷](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html)。

## 啟用目標複製代理 {#enabling-the-target-replication-agent}

test和目標 [複製代理](/help/sites-deploying/replication.md) 必須在作者實例上啟用。 請注意，如果您使用 [諾薩姆](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) 運行安裝模AEM式。 有關保護生產環境的詳細資訊，請參閱 [安全核對表](/help/sites-administering/security-checklist.md)。

1. 在首頁AEM上，按一下或點擊 **工具** > **部署** > **複製**。
1. 按一下或點擊 **作者代理**。
1. 按一下或點擊 **Test和目標(test和目標)** 複製代理，然後按一下或點擊 **編輯**。
1. 選擇「Enabled（啟用）」選項，然後按一下或點擊 **確定**。

   >[!NOTE]
   >
   >配置Test和目標複製代理時， **運輸** 頁籤， URI預設設定為 **tnt:///**。 不要將此URI替換為 **https://admin.testandtarget.omniture.com**。
   >
   >請注意，如果您嘗試將連接test為 **tnt:///**，將引發錯誤。 這是預期行為，因為此URI僅供內部使用，不應與 **Test連接**。

## 保護活動設定節點 {#securing-the-activity-settings-node}

必須保護活動設定節點的安全 **cq：活動設定** 在發佈實例上，以便普通用戶無法訪問。 活動設定節點只能由處理與Adobe Target的活動同步的服務訪問。

的 **cq：活動設定** 節點在CRXDE lite中可用 `/content/campaigns/*nameofbrand*`* *活動jcr:content節點下；* *例如 `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`。 此節點僅在目標元件後建立。

的 **cq：活動設定** 活動的jcr:content下的節點受以下ACL保護：

* 拒絕所有人
* 允許「target-activity-authors」的jcr:read,rep:write（作者是此組的成員，現成）
* 允許jcr:read,rep:write用於&quot;targetservice&quot;

這些設定確保普通用戶無權訪問節點屬性。 對作者和發佈使用相同的ACL。 請參閱 [用戶管理和安全](/help/sites-administering/security.md) 的子菜單。

## 配置鏈AEM接外部化器 {#configuring-the-aem-link-externalizer}

在Adobe Target編輯活動時，URL指向 **本地主機** 除非您更改「作者」節AEM點上的URL。 如果希望導AEM出的內容指向特定內容，可以配置連結外部化程式 *發佈* 。

>[!NOTE]
>
>另請參閱 [添加雲配置](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)。

要配置外AEM部化程式：

>[!NOTE]
>
>有關詳細資訊，請參閱 [外部化URL](/help/sites-developing/externalizer.md)。

1. 導航至OSGi Web控制台，位於 **https://&lt;server>:&lt;port>/system/console/configMgr。**
1. 查找 **第CQ天連結外部化程式** 並輸入作者節點的域。

   ![chlimage_1-120](assets/aem-externalizer-01.png)
