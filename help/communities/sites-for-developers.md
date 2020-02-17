---
title: 社群網站基本功能
seo-title: 社群網站基本功能
description: 匯出和刪除社群網站並建立自訂網站範本
seo-description: 匯出和刪除社群網站並建立自訂網站範本
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 社群網站基本功能 {#community-site-essentials}

## 自訂網站範本 {#custom-site-template}

可以為社區站點的每個語言副本單獨指定自定義站點模板。

為此，

* 建立自訂範本
* 覆蓋預設網站範本路徑
* 新增自訂範本至覆蓋路徑
* 將屬性新增至節點以指 `page-template` 定自訂范 `configuration` 本

**預設範本**:

/**libs**/social/console/components/hbs/sitepage/**sitepage**.hbs

**覆蓋路徑中的自訂範本**:

/**apps**/social/console/components/hbs/sitepage/**&lt;*template-name*>**.hbs

**屬性**:page-template **類型**:字串&#x200B;**值**:&lt;*template-name*>（無副檔名）

**配置節點**:

/content/&lt;*社群網站路徑*>/&lt;*lang*>/configuration

例如：/content/sites/engage/tw/configuration

>[!NOTE]
>
>覆蓋路徑中的所有節點都只需要類型 `Folder`。

>[!CAUTION]
>
>如果自訂範本的名稱為 *sitepage.hbs,* 則會自訂所有社群網站。

### 自訂網站範本範例 {#custom-site-template-example}

例如，網站范 `vertical-sitepage.hbs` 本會導致功能表連結在頁面左側垂直放置，而非橫幅下方水準放置。

[取得檔](assets/vertical-sitepage.hbs)案將自訂網站範本置於覆蓋資料夾：

/**apps**/social/console/components/hbs/sitepage/**vertical-sitepage**.hbs

通過向配置節點添加屬 `page-template` 性來標識自定義模板：

/content/sites/sample/tw/configuration

![chlimage_1-80](assets/chlimage_1-80.png)

請確定「全 **部儲存** 」並將自訂代碼複製至所有AEM例項（自訂代碼不包含在從主控台發佈社群網站內容時）。

複製自訂程式碼的建議做法是 [建立套件](../../help/sites-administering/package-manager.md#creating-a-new-package) ，並將它部署在所有例項上。

## 導出社區站點 {#exporting-a-community-site}

在建立社群網站後，就可以將網站匯出為儲存在套件管理員中的AEM套件，並可供下載和上傳。

這可從 [Communities Sites控制台獲得](sites-console.md#exporting-the-site)。

請注意，社群網站套件中不包含UGC和自訂代碼。

若要匯出UGC，請使用 [AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)，這是GitHub上提供的開放原始碼移轉工具。

## 刪除社群網站 {#deleting-a-community-site}

自AEM Communities 6.3 Service Pack 1起，「刪除網站」圖示會顯示在「社群>網站主控台」的社群網站上。 在開發期間，如果想要刪除社群網站並重新開始，您可以使用此功能。 刪除社群網站時，會移除與該網站相關的下列項目：

* [UGC](#user-generated-content)
* [使用者群組](#community-user-groups)
* [資產](#enablement-assets)
* [資料庫記錄](#database-records)

### 社群獨特網站ID {#community-unique-site-id}

要標識與社區站點關聯的唯一站點ID，請使用CRXDE:

* 導覽至網站的語言根目錄，例如 `/content/sites/*<site name>*/en/rep:policy`

* 查找 `allow<#>` 具有此格 `rep:principalName` 式的節點 `rep:principalName = *community-enable-nrh9h-members*`

* 網站ID是第3個元件， `rep:principalName`例如，如果 `rep:principalName = community-enable-nrh9h-members`

   * **網站名稱** =啟 *用*
   * **網站ID** = *nrh9h*
   * **唯一網站ID** = *enable-nrh9h*

### 使用者產生的內容 {#user-generated-content}

從Github取得communities-srp-tools專案：

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

這包含一個servlet，用於從任何SRP中刪除所有UGC。

所有UGC皆可移除，或針對特定網站移除，例如：

* path=/content/usergenerated/asi/mongo/content/sites/engage

這只會移除使用者產生的內容（在發佈時輸入）及未編寫的內容（在作者時輸入）。 因此，影 [子節點](srp.md#shadownodes) 不受影響。

### 社群使用者群組 {#community-user-groups}

在所有作者和發佈例項上，從安 [全性主控台](../../help/sites-administering/security.md)，找出並移 [除下列使用者群組](users.md) :

* 前置詞 `community`
* 後跟唯 [一的網站ID](#community-unique-site-id)

例如， `community-engage-x0e11-members`。

### 啟用資產 {#enablement-assets}

從主控制台：

* Select **[!UICONTROL Assets]**
* 進入 **[!UICONTROL 選擇模]** 式
* 選取以唯一網站Id命名 [的檔案夾](#community-unique-site-id)
* 選擇 **[!UICONTROL 刪除]** (可能需要從更 **[!UICONTROL 多……]**)

### 資料庫記錄 {#database-records}

沒有工具可選擇性地刪除某個特定啟用社群網站的資料庫項目。

刪除所有社群站點時，請使用MySQL Workbench刪除enablementdb和scormenginedb。
