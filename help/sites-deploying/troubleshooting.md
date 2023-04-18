---
title: 疑難排解AEM的安裝問題
description: 本文涵蓋您在使用AEM時可能會遇到的部分安裝問題。
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

# 疑難排解AEM的安裝問題{#troubleshooting}

本節包含可協助您進行疑難排解之記錄的詳細資訊，也包含您可能遇到AEM部分問題的相關資訊。

## 疑難排解作者效能 {#troubleshoot-author-performance}

在製作例項上分析效能緩慢可能會變得複雜。 作為第一步，需要確定效能正在降低的技術堆棧的級別。

以下決策樹提供縮小瓶頸的指導。

![chlimage_1-75](assets/chlimage_1-75.png)

## 基本最佳化 {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## 配置日誌檔案和審核日誌 {#configuring-log-files-and-audit-logs}

AEM會記錄您可能要設定以疑難排解安裝問題的詳細記錄。 如需詳細資訊，請參閱 [使用審核記錄和日誌檔案](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 區段。

## 使用詳細選項 {#using-the-verbose-option}

啟動AEM WCM時，可以將 — v(verbose)選項添加到命令行，如下所示：java -jar cq-wcm-quickstart-&lt;version>.jar -v。

詳細選項在控制台上顯示一些快速入門日誌輸出，以便用於故障排除。

## 常見安裝問題 {#common-installation-issues}

以下章節說明一些安裝問題及其解決方案。

### 按兩下Quickstart Jar沒有作用，或使用其他程式（例如，歸檔管理器）開啟jar檔案 {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

此問題通常表示作業系統的案頭環境設定為開啟副檔名為.jar的檔案時出現問題。 也可能表示您未安裝Java™，或您使用的Java™版本不受支援。

由於jar檔案使用普遍的ZIP格式，因此某些存檔程式可能會自動配置案頭以將jar檔案作為存檔檔案開啟。

若要進行疑難排解，請執行下列動作：

* 再次檢查您是否至少安裝了Java™ 1.6版。
* 在AEM WCM快速入門中嘗試上下文菜單（通常按一下滑鼠右鍵），然後選擇「開啟……」.&quot;
* 檢查是否列出了Java™或Sun Java™，並嘗試運行AEM WCM。 如果您已安裝多個Java™版本，請選取支援的版本。

   如果此步驟成功，且您的作業系統提供一個選項，可始終使用所選程式運行.jar檔案，請選擇該檔案。 從現在開始，按兩下應該就能運作。

* 有時重新安裝支援的Java™版本有助於恢復正確的關聯。
* 您始終可以使用命令行或啟動/停止指令碼運行CRX，如本文檔前面所述。

### 我在CRX上執行的應用程式擲回記憶體不足錯誤 {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>另請參閱 [分析記憶體問題](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=en).


CRX公司自身的記憶體佔用空間很小。 如果在CRX內運行的應用程式記憶體要求較高，或請求記憶體密集型操作（如大事務），則必須使用適當的記憶體設定來啟動CRX運行的JVM實例。

使用Java™命令選項定義JVM的記憶體設定（例如，java -Xmx512m -jar crx&amp;ast;.jar將heapsize設定為512 MB）。

從命令列啟動AEM WCM時，指定記憶體設定選項。 管理AEM WCM啟動的AEM WCM啟動/停止指令碼或自訂指令碼也可修改，以定義所需的記憶體設定。

如果已將堆大小定義為512 MB，則可能要通過建立堆轉儲進一步分析記憶體問題：

要在記憶體不足時自動建立堆轉儲，請使用以下命令：

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &amp;ast;.jar

此方法會產生堆轉儲檔案(**java_..hprof**)，而不是記憶體不足時。 生成堆轉儲後，該進程可繼續運行。 通常，一個堆轉儲檔案就足以分析問題。

### 按兩下「AEM快速入門」後，瀏覽器中不會顯示「AEM歡迎」畫面 {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

在某些情況下，即使存放庫本身已成功執行，AEM WCM歡迎畫面也不會自動顯示。 此問題可能取決於作業系統設定、瀏覽器設定或類似因素。

常見的症狀是AEM WCM Quickstart窗口顯示「AEM WCM正在啟動，等待伺服器啟動…….&quot; 如果顯示該訊息的時間相對較長，請使用預設的4502埠或執行個體所在的埠，手動將AEM WCM URL輸入到瀏覽器視窗中：http://localhost:4502/。

此外，記錄檔可能會顯示瀏覽器未啟動的原因。

有時，AEM WCM Quickstart視窗會顯示訊息「AEM WCM running on http://localhost:port/」，而瀏覽器不會自動啟動。 在這種情況下，請按一下「 AEM WCM快速入門」窗口中的URL（它是超連結），或在瀏覽器中手動輸入URL。

如果其他所有項目都失敗，請查看記錄，了解發生的情況。

### 網站沒有透過Java™ 11載入或間歇性失敗 {#the-website-does-not-load-or-fails-intermittently-with-java11}

AEM 6.5在Java™ 11上執行時有一個已知問題，網站可能不會間歇性載入或失敗。

如果發生此問題，請執行下列動作：

1. 開啟 `sling.properties` 檔案 `crx-quickstart/conf/` 資料夾
1. 找出下列行：

   `org.osgi.framework.bootdelegation=sun.,com.sun.`

1. 以下列項目取代：

   `org.osgi.framework.bootdelegation=sun.,com.sun.,jdk.internal.reflect,jdk.internal.reflect.*`

1. 重新啟動執行個體。

## 使用應用程式伺服器進行安裝故障排除 {#troubleshooting-installations-with-an-application-server}

### 要求geometrixx-outdoor頁面時傳回Page Not Found {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}

**適用於WebLogic 10.3.5和JBoss® 5.1**

當geometrixx-outdoors/en頁面要求傳回404（找不到頁面）時，您可能會重新檢查是否已在這些特定應用程式伺服器所需的sling.properties檔案中設定其他sling屬性。

請參閱 *部署AEM Web應用程式* 詳細資訊的步驟。

### 回應標頭大小可以大於4 KB {#response-header-size-can-be-greater-than-kb}

502錯誤可能表示Web伺服器無法處理AEM HTTP回應標頭的大小。 AEM可產生包含大於4 KB之Cookie的HTTP回應標題。 請確定您的servlet容器已設定，讓最大回應標頭大小可超過4 KB。

例如，對於Tomcat 7.0, [HTTP連接器](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) 控制標頭大小的限制。

## 解除安裝Adobe Experience Manager {#uninstalling-adobe-experience-manager}

由於AEM會安裝至單一目錄，因此不需要解除安裝公用程式。 卸載過程可能與刪除整個安裝目錄一樣簡單，不過卸載AEM的方式取決於您要實現什麼，以及您使用什麼持久儲存。

如果永久儲存嵌入安裝目錄（例如，在預設的TarPM安裝中），則刪除資料夾也會刪除資料。

>[!NOTE]
>
>Adobe建議您先備份儲存庫再刪除AEM。 如果您刪除 &lt;cq-installation-directory>，您也可以刪除存放庫。 若要在刪除、移動或複製 &lt;cq-installation-directory>/crx-quickstart/repository資料夾，再刪除其他資料夾。

如果安裝AEM時使用外部儲存（例如資料庫伺服器），則刪除資料夾不會自動刪除資料，但會刪除儲存配置，這會使JCR內容的還原變得困難。

### JSP檔案未在JBoss®上編譯 {#jsp-files-are-not-compiled-on-jboss}

如果您安裝或更新JSP檔案以在JBoss®上Experience Manager，且未編譯對應的servlet，請確保已正確設定JBoss® JSP編譯器。 如需詳細資訊，請參閱
[JBoss®中的JSP編譯問題](https://helpx.adobe.com/experience-manager/kb/jsps-dont-compile-jboss.html) 文章。
