---
title: 疑難排解AEM的安裝問題
description: 本文涵蓋您在使用AEM時可能會遇到的一些安裝問題。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 55576729-be9c-412e-92ac-4be90650c6fa
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# 疑難排解AEM的安裝問題{#troubleshooting}

本節包含可協助您進行疑難排解的記錄詳細資訊，也包含您可能在AEM中遇到的一些問題的相關資訊。

## 疑難排解作者效能 {#troubleshoot-author-performance}

在編寫執行個體上分析緩慢的效能可能會變得複雜。 首先，必須弄清楚效能下降的技術棧疊層次。

下列決策樹提供縮小瓶頸的指引。

![chlimage_1-75](assets/chlimage_1-75.png)

## 基本最佳化 {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## 設定記錄檔和稽核記錄 {#configuring-log-files-and-audit-logs}

AEM會記錄您可能想要設定以疑難排解安裝問題的詳細記錄。 如需詳細資訊，請參閱[使用稽核記錄和記錄檔](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)區段。

## 使用詳細資訊選項 {#using-the-verbose-option}

啟動AEM WCM時，您可以將 — v (verbose)選項新增到命令列，如下所示：java -jar cq-wcm-quickstart-&lt;version>.jar -v。

詳細資訊選項會在主控台上顯示一些「快速入門」記錄輸出，以便用於疑難排解。

## 常見安裝問題 {#common-installation-issues}

下節將說明一些安裝問題及其解決方案。

### 連按兩下Quickstart jar沒有任何效果，或使用其他程式（例如archive manager）開啟jar檔案 {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

此問題通常表示作業系統的案頭環境設定為開啟副檔名為.jar之檔案的方式發生問題。 這也可能表示您尚未安裝Java™，或您使用不支援的Java™版本。

由於jar檔案使用隨處可見的ZIP格式，因此某些封存程式可能會自動設定案頭以開啟作為封存檔案的jar檔案。

若要進行疑難排解，請執行下列動作：

* 再次確認您至少已安裝Java™ 1.6版。
* 在AEM WCM Quickstart上嘗試快顯功能表（通常按一下滑鼠右鍵），然後選取「開啟方式」....
* 檢查是否列出Java™或Sun Java™，並嘗試用它執行AEM WCM。 如果您已安裝多個Java™版本，請選取支援的版本。

  如果您成功完成此步驟，且您的作業系統提供選項，讓您一律使用選取的程式來執行.jar檔案，請選取它。 從現在開始，按兩下應該會正常運作。

* 有時重新安裝支援的Java™版本有助於還原正確的關聯。
* 您一律可以使用命令列或啟動/停止指令碼執行CRX，如本檔案先前所述。

### 在CRX上執行的應用程式擲回記憶體不足錯誤 {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>另請參閱[分析記憶體問題](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html)。


CRX本身的記憶體空間不足。 如果在CRX中執行的應用程式有更大的記憶體需求或請求記憶體密集型作業（例如大型交易），執行CRX的JVM執行個體必須以適當的記憶體設定啟動。

使用Java™命令選項來定義JVM的記憶體設定（例如，java -Xmx512m -jar crx&amp;amp；ast；.jar將棧大小設為512 MB）。

從命令列啟動AEM WCM時，請指定記憶體設定選項。 用於管理AEM WCM啟動的AEM WCM啟動/停止指令碼或自訂指令碼也可以修改，以定義所需的記憶體設定。

如果您已經將棧大小定義為512 MB，您可以建立棧積傾印以進一步分析記憶體問題。

若要在記憶體不足時自動建立棧積傾印，請使用以下命令：

java -Xmx256m -XX：+HeapDumpOnOutOfMemoryError -jar &amp;amp；ast；.jar

只要處理序的記憶體不足，此方法就會產生棧積傾印檔案(**java_...hprof**)。 產生棧積傾印後，該程式可能會繼續執行。

通常需要在一段時間內收集的三個棧積傾印檔案來分析問題：

* 在失敗發生之前
* 失敗期間1
* 失敗期間2
* *理想情況下，在事件解決後收集資訊也是不錯的做法*

您可以比較這些變更以及物件使用記憶體的方式。

>[!NOTE]
>
>如果您定期收集這類資訊，或曾經讀取棧積傾印，則一個棧積傾印檔案就足以分析問題。

### 按兩下AEM快速入門後，AEM歡迎畫面未顯示在瀏覽器中 {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

在某些情況下，即使存放庫本身成功執行， AEM WCM歡迎畫面也不會自動顯示。 此問題可能取決於作業系統設定、瀏覽器設定或類似因素。

常見症狀為AEM WCM Quickstart視窗會顯示「AEM WCM正在啟動，等候伺服器啟動」.... 如果該訊息顯示的時間相對較長，請使用預設的4502連線埠，或執行處理執行所在的連線埠，手動將AEM WCM URL輸入瀏覽器視窗中： http://localhost:4502/。

此外，記錄可能會顯示瀏覽器未啟動的原因。

有時AEM WCM Quickstart視窗會顯示訊息「AEM WCM在http://localhost:port/上執行」，且瀏覽器不會自動啟動。 在這種情況下，請按一下AEM WCM Quickstart視窗中的URL （它是一個超連結）或在瀏覽器中手動輸入URL。

如果其他所有操作失敗，請檢查記錄檔以找出所發生的情況。

### 使用Java™ 11時，網站未載入或間歇性失敗 {#the-website-does-not-load-or-fails-intermittently-with-java11}

在Java™ 11上執行AEM 6.5有一個已知問題，網站可能無法載入或間歇性失敗。

如果發生此問題，請執行以下作業：

1. 開啟`crx-quickstart/conf/`資料夾下的`sling.properties`檔案
1. 找到下列行：

   `org.osgi.framework.bootdelegation=sun.,com.sun.`

1. 請以下列專案取代：

   `org.osgi.framework.bootdelegation=sun.,com.sun.,jdk.internal.reflect,jdk.internal.reflect.*`

1. 重新啟動執行個體。

## 應用程式伺服器的安裝疑難排解 {#troubleshooting-installations-with-an-application-server}

### 請求geometrixx-outdoor頁面時傳回頁面找不到 {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}

**套用至WebLogic 10.3.5和JBoss® 5.1**

對geometrixx-outdoors/en頁面的請求傳回404 （找不到頁面）時，您可以重新檢查是否已在這些特定應用程式伺服器所需的sling.properties檔案中設定其他sling屬性。

如需詳細資訊，請參閱&#x200B;*部署AEM Web應用程式*&#x200B;步驟。

### 回應標頭大小可以大於4 KB {#response-header-size-can-be-greater-than-kb}

502錯誤可能表示網頁伺服器無法處理AEM HTTP回應標頭的大小。 AEM可產生包含大小超過4 KB之Cookie的HTTP回應標頭。 請確定您的servlet容器已設定為最大回應標頭大小可超過4 KB。

例如，對於Tomcat 7.0，[HTTP Connector](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html)的maxHttpHeaderSize屬性可控制標頭大小的限制。

## 解除安裝Adobe Experience Manager {#uninstalling-adobe-experience-manager}

由於AEM會安裝在單一目錄中，因此不需要解除安裝公用程式。 雖然解除安裝AEM的方式取決於您想要達成的目標以及您使用的永久儲存體，但是解除安裝的方式卻可能像刪除整個安裝目錄一樣簡單。

如果永久儲存裝置內嵌於安裝目錄中（例如，在預設的TarPM安裝中），則刪除資料夾也會移除資料。

>[!NOTE]
>
>Adobe建議您在刪除AEM之前先備份存放庫。 如果您刪除整個&lt;cq-installation-directory>，也會刪除存放庫。 若要在刪除之前保留存放庫資料，請先將&lt;cq-installation-directory>/crx-quickstart/repository資料夾移動或複製到其他資料夾，然後再刪除其他資料夾。

如果您安裝的AEM使用外部儲存（例如資料庫伺服器），移除資料夾不會自動移除資料，但會移除儲存設定，因此還原JCR內容相當困難。

### JSP檔案未在JBoss上編譯® {#jsp-files-are-not-compiled-on-jboss}

如果您安裝或更新要Experience Manager在JBoss®上的JSP檔案，但未編譯對應的servlet，請確定JBoss® JSP編譯器已正確設定。 如需詳細資訊，請參閱
JBoss®[&#128279;](https://helpx.adobe.com/experience-manager/kb/jsps-dont-compile-jboss.html)文章中的JSP編譯問題。
