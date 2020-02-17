---
title: 微調運行狀況監視器效能
seo-title: 微調運行狀況監視器效能
description: 瞭解如何微調Health monitor效能
seo-description: 瞭解如何微調Health monitor效能
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 微調運行狀況監視器效能{#fine-tuning-health-monitor-performance}

收集填入Health Monitor的系統統計資料會對AEM表單環境的效能產生一定影響。 您可以透過設定應用程式伺服器中下列的Java選項來控制此影響。

<table>
 <thead>
  <tr>
   <th><p>屬性</p></th>
   <th><p>目的</p></th>
   <th><p>預設值</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe.healthmonitor.enabled</p></td>
   <td><p>開啟或關閉Health monitor線程</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics已啟用</p></td>
   <td><p>開啟或關閉Gemfire快取</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>Health monitor線程收集統計資訊的間隔（以毫秒為單位）</p></td>
   <td><p>10分鐘（600,000毫秒）</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>用於與分佈式系統的其他成員通信的組播埠。 如果設定為零，則會禁用成員發現和分發的多播。 </p><p>注意：為不同的分佈式系統選擇不同的組播地址和埠。 請勿僅使用不同的地址。</p></td>
   <td><p>無預設值。 有效值範圍從0到65535。</p></td>
  </tr>
  <tr>
   <td><p>統計採樣率</p></td>
   <td><p>統計資料取樣的速率（以毫秒為單位）。 作業系統統計資料只會在取得範例時更新。</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>此屬性啟用或禁用「工作管理器」統計收集，如作業或工作項目計數。</p></td>
   <td><p>true</p></td>
  </tr>
 </tbody>
</table>

## 將Java選項添加到JBoss {#add-java-options-to-jboss}

1. 停止JBoss應用程式伺服器。
1. 在編輯 *[器中開]*&#x200B;啟appserver root /bin/run.bat(Windows)或run.sh（Linux或UNIX），並視需要新增任何Java選項。
1. 重新啟動伺服器。

## 將Java選項新增至WebLogic {#add-java-options-to-weblogic}

1. 在Web瀏覽器的URL行中輸入https://[主機名]:[port]/console，以啟動WebLogic管理控制台。
1. 鍵入您為WebLogic server域建立的用戶名和密碼，然後按一下「更改中心」下的「日誌」，按一下「鎖定和編輯」。
1. 在「域結構」下，按一下「環境」>「伺服器」，然後在右窗格中按一下受控伺服器名稱。
1. 在下一個畫面中，按一下「設定」標籤>「伺服器開始」標籤。
1. 在「參數」框中，將所需參數附加到當前內容的末尾。 例如，添加——禁用 `Dadobe.healthmonitor.enabled=false` Health Monitor。
1. 按一下「儲存」，然後按一下「啟用變更」。
1. 重新啟動WebLogic受控伺服器。

## 將Java選項新增至WebSphere {#add-java-options-to-websphere}

1. 在WebSphere管理控制台導覽樹中，為應用程式伺服器執行下列動作：

   (WebSphere 6.x)按一下「伺服器>應用程式伺服器」

   (WebSphere 7.x)按一下「伺服器>伺服器類型> webSphere應用程式伺服器」

1. 在右窗格中，按一下伺服器名稱。
1. 在「伺服器基礎架構」下，按一下「Java和表單工作流」>「流程定義」。
1. 在「其他屬性」下，按一下「Java虛擬機」。
1. 在「通用JVM參數」框中，鍵入所需參數。
1. 按一下「確定」或「應用」，然後按一下「直接保存到主配置」。

