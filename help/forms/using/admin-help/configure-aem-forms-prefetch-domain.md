---
title: 設定AEM表單以預取網域資訊
seo-title: 設定AEM表單以預取網域資訊
description: 如果您由於巢狀內嵌的群組或您是許多群組的成員，而遇到較慢的回應時間，請設定AEM表單以預回遷網域資訊。
seo-description: 如果您由於巢狀內嵌的群組或您是許多群組的成員，而遇到較慢的回應時間，請設定AEM表單以預回遷網域資訊。
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# 設定AEM表單以預取網域資訊{#configure-aem-forms-to-prefetchdomain-information}

如果使用者屬於多個群組（例如500或更多），或者群組已深度巢狀化（例如30個層級），可能會遇到較慢的回應時間。 如果您遇到此問題，可以設定AEM表單，以從特定網域預回遷資訊。

1. 在管理控制台中，按一下「設定>使用者管理>設定>匯入和匯出設定檔&#x200B;**[!UICONTROL 」。]**
1. 要將當前配置設定導出到檔案，請按一下&#x200B;**[!UICONTROL Export]** ，並將配置檔案保存到其他位置。
1. 添加以下節點（以粗體標籤）:

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

   在此示例中，為預回遷配置了多個域。 域名以&quot;/&quot;分隔。 上述範例中顯示了此點：*Domain_Name1*、*Domain_Name2*&#x200B;和&#x200B;*Domain_Name3*。

1. 要導入更新的檔案，請在「用戶管理」中按一下「配置」>「導入和導出配置檔案」**[!UICONTROL 。]**
1. 按一下&#x200B;**[!UICONTROL 瀏覽]**&#x200B;查找檔案，按一下「導入」，然後按一下「確定」。****

