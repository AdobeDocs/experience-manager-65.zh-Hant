---
title: 排除安裝問題AEM
description: 本文介紹您可能遇到的一些安裝問題AEM。
uuid: 2ca898c3-b074-4ccd-a383-b92f226e6c14
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 5542de4e-6262-4300-9cf8-0eac79ba4f9a
exl-id: 55576729-be9c-412e-92ac-4be90650c6fa
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 0%

---

# 排除安裝問題AEM{#troubleshooting}

本部分包括可幫助您排除故障的日誌的詳細資訊，還包括您可能遇到的一些問題的信AEM息。

## 對作者效能進行故障排除 {#troubleshoot-author-performance}

分析創作實例上的慢效能會變得複雜。 作為第一步，需要確定效能正在下降的技術堆棧級別。

下面的決策樹為縮小瓶頸提供了指導。

![chlimage_1-75](assets/chlimage_1-75.png)

## 基本優化 {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## 配置日誌檔案和審核日誌 {#configuring-log-files-and-audit-logs}

記AEM錄詳細日誌，您可能要配置這些日誌來排除安裝問題。 有關資訊，請參見 [使用審計記錄和日誌檔案](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 的子菜單。

## 使用詳細選項 {#using-the-verbose-option}

啟動AEMWCM時，可將 — v(verbose)選項添加到命令行中，如所示：java -jar cq-wcm快速啟動 — &lt;version>.jar -v。

詳細選項顯示控制台上的一些Quickstart日誌輸出，以便用於故障排除。

## 常見安裝問題 {#common-installation-issues}

以下部分介紹一些安裝問題及其解決方案。

### 按兩下Quickstart jar無效，或使用其他程式（例如，存檔管理器）開啟jar檔案 {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

此問題通常表示作業系統的案頭環境配置為開啟副檔名為.jar的檔案時出現問題。 它還可能表明您未安裝Java™，或者您使用的是不受支援的Java™版本。

當jar檔案使用普遍的ZIP格式時，某些存檔程式可能會自動配置案頭以將jar檔案作為存檔檔案開啟。

要排除故障，請執行以下操作：

* 再次檢查是否至少安裝了Java™ 1.6版。
* 嘗試在WCM快速啟動上的上下文菜單(通AEM常用滑鼠按一下右鍵)，然後選擇「開啟方式……」&quot;
* 檢查是否列出了Java™或Sun Java™，並嘗試使用它AEM運行WCM。 如果安裝了多個Java™版本，請選擇支援的版本。

   如果此步驟成功，並且作業系統提供了始終使用選定程式運行.jar檔案的選項，請選擇它。 按兩下以後應該可以使用。

* 有時重新安裝支援的Java™版本有助於恢復正確的關聯。
* 您始終可以使用命令行或啟動/停止指令碼運行CRX，如本文檔前面所述。

### 我在CRX上運行的應用程式引發記憶體不足錯誤 {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>另請參閱 [分析記憶體問題](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=en)。


CRX本身記憶體佔用空間小。 如果在CRX中運行的應用程式具有較大的記憶體要求或請求大量記憶體操作（例如，大事務），則必須使用適當的記憶體設定啟動運行CRX的JVM實例。

使用Java™命令選項定義JVM的記憶體設定（例如，java -Xmx512m -jar crx&amp;ast;.jar將heapsize設定為512 MB）。

從命令行啟動AEMWCM時指定記憶體設定選項。 還可AEM以修改用於管理AEMWCM啟動的WCM啟動/停止指令碼或自定義指令碼，以定義所需的記憶體設定。

如果已將堆大小定義為512 MB，則可能希望通過建立堆轉儲來進一步分析記憶體問題：

要在記憶體不足時自動建立堆轉儲，請使用以下命令：

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &amp;ast;.jar

此方法生成堆轉儲檔案(**java_..教授**)進程記憶體不足時。 生成堆轉儲後，進程可能會繼續運行。 通常，一個堆轉儲檔案就足以分析問題。

### 按兩下AEMQuickstart後，瀏覽器中不顯示「歡迎」屏AEM幕 {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

在某些情況下，即使存AEM儲庫本身已成功運行，WCM歡迎螢幕也不會自動顯示。 此問題可能取決於作業系統設定、瀏覽器配置或類似因素。

通常的症狀是AEMWCM Quickstart窗口顯示「WCM正AEM在啟動，正在等待伺服器啟動……&quot; 如果該消息顯示時間較長，請使用預設的AEM4502埠或運行實例的埠將WCM URL手動輸入到瀏覽器窗口中：http://localhost:4502/。

此外，日誌可能會顯示瀏覽器未啟動的原因。

有時，AEM WCM Quickstart窗口會顯示消息「AEM WCM running on http://localhost:port/ 」，瀏覽器不會自動啟動。 在這種情況下，按一下「AEMWCM快速啟動」窗口中的URL（它是超連結），或在瀏覽器中手動輸入URL。

如果其他所有事情都失敗，請查看日誌以瞭解發生了什麼。

### 使用Java™ 11，網站未載入或間歇性失敗 {#the-website-does-not-load-or-fails-intermittently-with-java11}

在Java™ 11上運行AEM6.5時出現已知問題，網站可能未載入或間歇性失敗。

如果出現此問題，請執行以下操作：

1. 開啟 `sling.properties` 檔案 `crx-quickstart/conf/` 資料夾
1. 找到以下行：

   `org.osgi.framework.bootdelegation=sun.,com.sun.`

1. 替換為：

   `org.osgi.framework.bootdelegation=sun.,com.sun.,jdk.internal.reflect,jdk.internal.reflect.*`

1. 重新啟動實例。

## 使用應用程式伺服器進行安裝故障排除 {#troubleshooting-installations-with-an-application-server}

### 在請求幾何XX — 室外頁時返回「未找到頁」 {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}

**適用於WebLogic 10.3.5和JBoss® 5.1**

當對geometrixx-outdoors/en頁的請求返回404（未找到頁）時，可以重新檢查是否已在這些特定應用程式伺服器所需的sling.properties檔案中設定了附加sling屬性。

請參閱 *部署AEMWeb應用程式* 的子菜單。

### 響應標頭大小可以大於4 KB {#response-header-size-can-be-greater-than-kb}

502個錯誤可能表示Web伺服器無法處理AEMHTTP響應標頭的大小。 可AEM以生成包含大於4 KB的Cookie的HTTP響應頭。 確保已配置Servlet容器，以便最大響應標頭大小可以超過4 KB。

例如，對於Tomcat 7.0, [HTTP連接器](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) 控制標題大小的限制。

## 卸載Adobe Experience Manager {#uninstalling-adobe-experience-manager}

因AEM為安裝到單個目錄中，所以不需要卸載實用程式。 卸載可以與刪除整個安裝目錄一樣簡單，AEM但卸載方式取決於要實現的內容和使用的持久性儲存。

如果永久儲存嵌入到安裝目錄中，例如，在預設的TarPM安裝中，刪除資料夾也會刪除資料。

>[!NOTE]
>
>Adobe建議您在刪除之前備份儲存AEM庫。 如果刪除整個 &lt;cq-installation-directory>，您也會刪除儲存庫。 在刪除、移動或複製儲存庫資料之前保留 &lt;cq-installation-directory>在刪除其他資料夾之前，在其他位置使用/crx-quickstart/repository資料夾。

如果安裝時AEM使用外部儲存，則刪除資料夾不會自動刪除資料，而是會刪除儲存配置，這會使恢復JCR內容變得困難。

### JSP檔案未在JBoss®上編譯 {#jsp-files-are-not-compiled-on-jboss}

如果在JBoss®上安裝或更新JSP檔案以Experience Manager，且未編譯相應的Servlet，請確保正確配置了JBoss® JSP編譯器。 有關資訊，請參見
[JBoss®中的JSP編譯問題](https://helpx.adobe.com/experience-manager/kb/jsps-dont-compile-jboss.html) 文章。
