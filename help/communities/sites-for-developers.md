---
title: 社群網站要點
description: 匯出和刪除社群網站並建立自訂網站範本
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---

# 社群網站要點 {#community-site-essentials}

## 自訂網站範本 {#custom-site-template}

您可以為社群網站的每個語言復本個別指定自訂網站範本。

若要這麼做：

* 建立自訂範本。
* 覆蓋預設的網站範本路徑。
* 新增自訂範本至覆蓋路徑。
* 將`page-template`屬性新增到`configuration`節點，以指定自訂範本。

**預設範本**：

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**覆蓋路徑中的自訂範本**：

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**屬性**： page-template

**型別**：字串

**值**： `template-name` （無副檔名）

**設定節點**：

`/content/community site path/lang/configuration`

例如：`/content/sites/engage/en/configuration`

>[!NOTE]
>
>覆蓋路徑中的所有節點只需要是型別`Folder`。

>[!CAUTION]
>
>如果自訂範本的名稱為&#x200B;*sitepage.hbs*，則會自訂所有社群網站。

### 自訂網站範本範例 {#custom-site-template-example}

例如，`vertical-sitepage.hbs`是網站範本，導致在頁面左側垂直向下放置功能表連結，而不是在橫幅下方水平放置。

[取得檔案](assets/vertical-sitepage.hbs)
將自訂網站範本放置在覆蓋資料夾中：

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

將`page-template`屬性新增至設定節點，以識別自訂範本：

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

請務必&#x200B;**儲存全部**&#x200B;並將自訂程式碼復寫至所有Adobe Experience Manager (AEM)執行個體（從主控台發佈社群網站內容時不含自訂程式碼）。

復寫自訂程式碼的建議作法是[建立套件](../../help/sites-administering/package-manager.md#creating-a-new-package)並在所有執行個體上部署它。

## 匯出社群網站 {#exporting-a-community-site}

社群網站建立後，即可將網站匯出為儲存在封裝管理員中的AEM套件，並可供下載和上傳。

這可從[社群網站主控台](sites-console.md#exporting-the-site)取得。

UGC和自訂程式碼未包含在社群網站套件中。

若要匯出UGC，請使用[AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration)，這是GitHub上提供的開放原始碼移轉工具。

## 刪除社群網站 {#deleting-a-community-site}

截至AEM Communities 6.3 Service Pack 1，「刪除網站」圖示會顯示在從&#x200B;**[!UICONTROL 社群]** > **[!UICONTROL 網站]**&#x200B;主控台暫留在社群網站上。 在開發期間，如果想要刪除社群網站並重新開始，您可以使用此功能。 刪除社群網站時，會移除與該網站相關聯的下列專案：

* [UGC](#user-generated-content)
* [使用者群組](#community-user-groups)
* [資料庫記錄](#database-records)

### 社群唯一網站ID {#community-unique-site-id}

若要使用CRXDE識別與社群網站相關聯的不重複網站ID：

* 導覽至網站的語言根目錄，例如`/content/sites/*<site name>*/en/rep:policy`。

* 尋找此格式為`rep:principalName = *community-enable-nrh9h-members*`且具有`rep:principalName`的`allow<#>`節點。

* 網站ID是`rep:principalName`的第三個元件

  例如，如果`rep:principalName = community-enable-nrh9h-members`

   * **網站名稱** = *啟用*
   * **網站識別碼** = *nrh9h*
   * **唯一網站識別碼** = *enable-nrh9h*

### 使用者產生的內容 {#user-generated-content}

從GitHub取得communities-srp-tools專案：

* [https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

這包含一個servlet，可從任何SRP刪除所有UGC。

所有UGC都可移除，或針對特定網站移除，例如：

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

這只會移除使用者產生的內容（在發佈時輸入），而不會移除編寫的內容（在作者時輸入）。 因此，[陰影節點](srp.md#shadownodes)不受影響。

### 社群使用者群組 {#community-user-groups}

在所有作者和發佈執行個體上，從[安全性主控台](../../help/sites-administering/security.md)，尋找並移除符合下列條件的[使用者群組](users.md)：

* 前置詞為`community`
* 後面接著[唯一網站識別碼](#community-unique-site-id)

例如，`community-engage-x0e11-members`。
