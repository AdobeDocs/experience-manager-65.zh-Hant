---
title: 微調運行狀況監視器效能
seo-title: Fine-tuning Health Monitor performance
description: 瞭解如何微調運行狀況監視器效能
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

收集填充運行狀況監視器的系統統計資訊會對表單環境的效能AEM產生一定影響。 可通過在應用程式伺服器中設定下面列出的Java選項來控制此影響。

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
   <td><p>開啟或關閉運行狀況監視器線程</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>開啟或關閉Gemfire快取</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>運行狀況監視器線程收集統計資訊的時間間隔（毫秒）</p></td>
   <td><p>10分鐘（600,000毫秒）</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>用於與分佈式系統的其他成員通信的組播埠。 如果設定為零，則會禁用成員發現和分發的多播。 </p><p>注：為不同的分佈式系統選擇不同的多播地址和埠。 不要只使用不同的地址。</p></td>
   <td><p>無預設值。 有效值範圍從0到65535。</p></td>
  </tr>
  <tr>
   <td><p>統計採樣率</p></td>
   <td><p>統計資訊採樣的速率（毫秒）。 只有在採集示例時才更新作業系統統計資訊。</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>此屬性啟用或禁用Work Manager統計資訊收集，如作業或工作項計數。</p></td>
   <td><p>true</p></td>
  </tr>
 </tbody>
</table>

## 將Java選項添加到JBoss {#add-java-options-to-jboss}

1. 停止JBoss應用程式伺服器。
1. 開啟 *[appserver根]*/bin/run.bat(Windows)或run.sh（Linux或UNIX），並根據需要添加任何Java選項。
1. 重新啟動伺服器。

## 將Java選項添加到WebLogic {#add-java-options-to-weblogic}

1. 鍵入https://啟動WebLogic管理控制台[主機名]: Web瀏覽器的URL行中的「port」/console。
1. 鍵入您為WebLogic Server域建立的用戶名和密碼，然後按一下「更改中心」下的「日誌」，然後按一下「鎖定和編輯」。
1. 在「域結構」下，按一下「環境」>「伺服器」，然後在右窗格中按一下受控伺服器名稱。
1. 在下一螢幕中，按一下「配置」頁籤>「伺服器啟動」頁籤。
1. 在「參數」框中，將所需參數追加到當前內容的末尾。 例如，添加 —  `Dadobe.healthmonitor.enabled=false` 禁用運行狀況監視器。
1. 按一下「保存」，然後按一下「激活更改」。
1. 重新啟動WebLogic托管伺服器。

## 將Java選項添加到WebSphere {#add-java-options-to-websphere}

1. 在WebSphere管理控制台導航樹中，為應用程式伺服器執行以下操作：

   (WebSphere 6.x)按一下「伺服器」>「應用程式伺服器」

   (WebSphere 7.x)按一下「伺服器」>「伺服器類型」>「WebSphere應用程式伺服器」

1. 在右窗格中，按一下伺服器名稱。
1. 在「伺服器基礎架構」下，按一下「Java」和「表單」工作流>「進程定義」。
1. 在「其他屬性」下，按一下「Java虛擬機」。
1. 在「一般JVM參數」框中，鍵入所需的參數。
1. 按一下「確定」或「應用」，然後直接按一下「保存」到主配置。
