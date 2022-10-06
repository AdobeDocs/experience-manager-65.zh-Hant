---
title: 微調運行狀況監視器效能
seo-title: Fine-tuning Health Monitor performance
description: 了解如何微調運行狀況監視器的效能
seo-description: Learn how to fine-tune Health Monitor performance
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
exl-id: 41042e08-5e14-4809-89b7-16d98a72d1b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 1%

---

# 微調運行狀況監視器效能{#fine-tuning-health-monitor-performance}

收集填入健康監視器的系統統計資料，會對AEM表單環境的效能造成一些影響。 您可以透過在應用程式伺服器中設定下列Java選項來控制此影響。

<table>
 <thead>
  <tr>
   <th><p>屬性</p></th>
   <th><p>用途</p></th>
   <th><p>預設值</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe.healthmonitor.enabled</p></td>
   <td><p>開啟或關閉健康監視器線程</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>開啟或關閉Gemfire快取</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>運行狀況監視器線程收集統計資訊的間隔（毫秒）</p></td>
   <td><p>10分鐘（600,000毫秒）</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>用於與分佈式系統的其他成員通信的多播埠。 如果設為零，則會禁用成員發現和分發的多播。 </p><p>注意：為不同的分佈式系統選擇不同的多播地址和埠。 請勿僅使用不同的地址。</p></td>
   <td><p>無預設值。 有效值範圍從0到65535。</p></td>
  </tr>
  <tr>
   <td><p>統計抽樣率</p></td>
   <td><p>統計資料被採樣的速率（毫秒）。 只有取樣時才會更新作業系統統計資料。</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>此屬性可啟用或禁用工作管理員統計收集，如工作或工作項計數。</p></td>
   <td><p>true</p></td>
  </tr>
 </tbody>
</table>

## 將Java選項新增至JBoss {#add-java-options-to-jboss}

1. 停止JBoss應用程式伺服器。
1. 開啟 *[appserver根]*/bin/run.bat(Windows)或run.sh（Linux或UNIX），並視需要新增任何Java選項。
1. 重新啟動伺服器。

## 將Java選項新增至WebLogic {#add-java-options-to-weblogic}

1. 輸入https://以啟動WebLogic管理控制台[主機名稱]:Web瀏覽器URL行中的&#39;port&#39;/console。
1. 鍵入您為WebLogic Server域建立的用戶名和密碼，然後按一下更改中心下的日誌，按一下鎖定和編輯。
1. 在「域結構」下，按一下「環境」>「伺服器」，然後在右窗格中按一下受控伺服器名稱。
1. 在下一個畫面中，按一下「設定」標籤>「伺服器開始」標籤。
1. 在「參數」框中，將所需的參數附加到當前內容的結尾。 例如，新增 —  `Dadobe.healthmonitor.enabled=false` 禁用運行狀況監視器。
1. 按一下「儲存」，然後按一下「啟動變更」。
1. 重新啟動WebLogic托管伺服器。

## 將Java選項添加到WebSphere {#add-java-options-to-websphere}

1. 在WebSphere管理控制台導航樹中，為應用程式伺服器執行以下操作：

   (WebSphere 6.x)按一下「伺服器」>「應用程式伺服器」

   (WebSphere 7.x)按一下「伺服器」>「伺服器類型」>「WebSphere應用程式伺服器」

1. 在右窗格中，按一下伺服器名稱。
1. 在「伺服器基礎架構」下，按一下「Java和表單工作流」>「流程定義」。
1. 在「其他屬性」下，按一下「Java虛擬機」。
1. 在「一般JVM參數」框中，鍵入所需參數。
1. 按一下「確定」或「應用」，然後按一下「直接保存到主配置」。
