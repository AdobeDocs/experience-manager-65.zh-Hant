---
title: 6.5中的電子商AEM務儲存庫重組
seo-title: E-Commerce Repository Restructuring in AEM 6.5
description: 瞭解如何進行必要的更改，以便遷移到E-Commerce的AEM6.5版中的新儲存庫結構。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.5 for E-Commerce.
uuid: 1fff1a4b-c8d0-4016-92fb-e2ea26e3a302
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 28c92e7d-2106-4333-afa6-c5528a00d7b4
feature: Upgrading
exl-id: 78b7c497-c474-4308-bfab-8f424b5f7268
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 2%

---

# 6.5中的電子商AEM務儲存庫重組{#e-commerce-repository-restructuring-in-aem}

如父代中所述 [6.5中的AEM儲存庫重組](/help/sites-deploying/repository-restructuring.md) 頁面，升級到AEM6.5的客戶應使用此頁面評估與影響電子商務解決方案的儲存庫更改相關AEM的工作量。 某些更改需要在6.5升AEM級過程中進行工作，而其他更改則可以推遲到以後升級。

## 使用6.5升級 {#with-upgrade}

### 產品、訂單、收款、分類、發運方法和付款方法資料 {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><p><code>/etc/commerce/products</code></p> <p><code>/etc/commerce/orders</code></p> <p><code>/etc/commerce/collections</code></p> <p><code>/etc/commerce/classifications</code></p> <p><code>/etc/commerce/shipping-methods</code></p> <p><code>/etc/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/var/commerce/products</code></p> <p><code>/var/commerce/orders</code></p> <p><code>/var/commerce/collections</code></p> <p><code>/var/commerce/classifications</code></p> <p><code>/var/commerce/shipping-methods</code></p> <p><code>/var/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>您可以使用 <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">懶惰遷移</a> 遷移電子商務資料的任務。</p> <p>它執行以下步驟：</p>
    <ul>
     <li>將參照調整到舊位置以指向新位置</li>
     <li>將內容從舊位置移動到新位置</li>
     <li>刪除舊位置，以最終激活整個系統中新位置的使用</li>
    </ul> <p>任務所涵蓋的位置包括：</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment methods<br /> </li>
     <li>/etc/commerce/shipping方法<br /> </li>
    </ul> <p>對於較大的目錄，通過將以下Java系統屬性傳遞給以下對象，命令單獨運行商務遷移任AEM務：</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>遷移後AEM需要重新啟動。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>
