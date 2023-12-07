---
title: 設定AEM表單以預先擷取網域資訊
description: 如果您因為深度巢狀化群組或是許多群組的成員，而導致回應時間變慢，請設定AEM表單以預先擷取網域資訊。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# 設定AEM表單以預先擷取網域資訊 {#configure-aem-forms-to-prefetchdomain-information}

如果使用者屬於許多群組（例如500個或更多）或群組巢狀結構較深（例如30個層級），回應時間可能會變慢。 如果您遇到此問題，可以設定AEM表單以從特定網域預先擷取資訊。

1. 在管理控制檯中，按一下 **[!UICONTROL 「設定」 > 「使用者管理」 > 「組態」 > 「匯入與匯出組態檔」]**.
1. 若要將目前的組態設定匯出至檔案，請按一下 **[!UICONTROL 匯出]** 並將組態檔案儲存在其他位置。
1. 新增下列節點（以粗體標籤）：

   ```xml
    <node name="UM">
    <map/>
    <node name="PrincipalCache">
        <map>
            <entry key="principalCacheSize" value="1000"/>
            <entry key="principalCacheBatchFetchSize" value="10"/>
            <entry key="rebuildCacheAfterSync" value="true />
            <entry key="enableFullPrefetch" value="false"/>
            <entry key="principalCacheDomains" value="Domain_Name1/Domain_Name2/Domain_Name3"/>
        <map>
    </node>
    <node name="APSAuditService">
   ```

   在此範例中，有多個網域設定為預先擷取。 網域名稱以「/」分隔。 以上範例顯示，包含 *網域名稱1*， *網域名稱2*、和 *網域名稱3*.

1. 若要匯入更新的檔案，請在「使用者管理」中按一下 **[!UICONTROL 「組態」>「匯入與匯出組態檔」]**.
1. 按一下 **[!UICONTROL 瀏覽]** 若要尋找檔案，請按一下匯入，然後按一下 **[!UICONTROL 確定]**.
