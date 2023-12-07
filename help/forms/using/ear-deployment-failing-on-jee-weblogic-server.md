---
title: JEE WebLogic伺服器上的EAR部署失敗
description: 解決JEE WebLogic Server上EAR部署失敗的步驟
exl-id: b87a9eee-ee56-4dca-b4a3-a42c91db0b4f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 7%

---

# JEE WebLogic Server上的EAR部署失敗 {#ear-deployment-failing-on-jee-weblogic-server}

## 問題 {#issue}

當使用者嘗試部署 `adobe-livecycle-weblogic.ear`，則 `Null Pointer` 發生例外狀況。

## 套用至 {#applies-to}

此解決方案適用於：

* WebLogic JEE伺服器12.2.1.x版上的AEM Forms。

## 解決方案 {#solution}

若要解決問題，請依照下列步驟進行：

1. 前往 `<domain_home>\bin` 已安裝的WebLogic JEE伺服器目錄。

1. 編輯 `setDomainEnv.cmd` 或 `setDomainEnv.sh` 檔案，如 `applicable`.

1. 搜尋最後出現的 `JAVA_OPTS` 並新增 `-DANTLR_USE_DIRECT_CLASS_LOADING=true` 轉換至此。 例如，更新的字串會顯示為：

       set &#39;JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true&#39;
   
1. 儲存變更。
