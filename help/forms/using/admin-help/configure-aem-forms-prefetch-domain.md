---
title: 設定AEM表單以預先擷取網域資訊
seo-title: Configure AEM forms to prefetchdomain information
description: 如果您因深巢狀群組或您是許多群組的成員而遇到回應時間較慢，請設定AEM表單以預先擷取網域資訊。
seo-description: Configure AEM forms to prefetch domain information if you experience a slower response time due to deeply nested groups or if you are a member of many groups.
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# 設定AEM表單以預先擷取網域資訊 {#configure-aem-forms-to-prefetchdomain-information}

如果使用者屬於許多群組（例如500或更多），或者群組深度巢狀化（例如30個層級），則可能會遇到較慢的回應時間。 如果您遇到此問題，可以設定AEM表單以從特定網域預先擷取資訊。

1. 在管理控制台中，按一下 **[!UICONTROL 設定>使用者管理>設定>匯入和匯出設定檔]**.
1. 要將當前配置設定導出到檔案，請按一下 **[!UICONTROL 匯出]** 並將配置檔案保存到其他位置。
1. 新增下列節點（以粗體標示）:

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

   在此範例中，會設定多個網域以進行預先擷取。 網域名稱以「/」分隔。 這如上例所示，搭配 *域名1*, *域名2*，和 *域名3*.

1. 若要匯入更新的檔案，請在「使用者管理」中，按一下 **[!UICONTROL 配置>導入和導出配置檔案]**.
1. 按一下 **[!UICONTROL 瀏覽]** 要查找檔案，請按一下「導入」，然後按一下 **[!UICONTROL 確定]**.
