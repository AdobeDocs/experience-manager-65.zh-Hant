---
title: JEE WebLogic伺服器上的EAR部署失敗
seo-title: EAR Deployment failing on JEE Weblogic Server
description: 解決JEE WebLogic Server上EAR部署失敗的步驟
seo-description: Steps to resolve EAR Deployment failing on JEE Weblogic Server
source-git-commit: 45bb54a2666c2c196a8fb52795a7f428aa751e4d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# JEE WebLogic Server上的EAR部署失敗 {#ear-deployment-failing-on-jee-weblogic-server}

## 問題 {#issue}

當使用者嘗試部署 `adobe-livecycle-weblogic.ear`，則 `Null Pointer` 發生例外狀況。

## 套用至 {#applies-to}

此解決方案適用於：

* WebLogic JEE伺服器12.2.1.x版上的AEM Forms。

## 解決方案 {#solution}

若要解決問題，請遵循下列步驟：

1. 前往 `<domain_home>\bin` 已安裝的WebLogic JEE伺服器目錄。

1. 編輯 `setDomainEnv.cmd` 或 `setDomainEnv.sh` 檔案，作為 `applicable`.

1. 搜尋最後出現的 `JAVA_OPTS` 並新增 `-DANTLR_USE_DIRECT_CLASS_LOADING=true` 至此。 例如，更新的字串會顯示為：

       set &#39;JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true&#39;
   
1. 儲存變更。


