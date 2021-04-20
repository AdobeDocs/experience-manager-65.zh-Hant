---
title: 6.5版中的電子商AEM務儲存庫重組
seo-title: 6.5版中的電子商AEM務儲存庫重組
description: 瞭解如何進行必要的更改，以遷移至適用於電子商務的AEM6.5中的新儲存庫結構。
seo-description: 瞭解如何進行必要的更改，以遷移至適用於電子商務的AEM6.5中的新儲存庫結構。
uuid: 1fff1a4b-c8d0-4016-92fb-e2ea26e3a302
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 28c92e7d-2106-4333-afa6-c5528a00d7b4
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 2%

---


# 6.5{#e-commerce-repository-restructuring-in-aem}中的電AEM子商務儲存庫重組

如[父6.5](/help/sites-deploying/repository-restructuring.md)頁中的「資料庫重組」頁中所述，升級至AEM6.5的客戶應使用本頁來評估與影響電子商務解決方案的資料庫更改相關的AEM工作成果。 有些變更需要在6.5升級程AEM序中努力工作，而有些則會延遲至日後升級。

## 使用6.5升級{#with-upgrade}

### 產品、訂單、收集、分類、發運方法和付款方法資料{#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

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
   <td><p>您可以使用<a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">延遲移轉</a>任務來移轉電子商務資料。</p> <p>它執行以下步驟：</p>
    <ul>
     <li>調整對舊位置的參照以指向新位置</li>
     <li>將內容從舊位置移到新位置</li>
     <li>移除舊位置，最終激活整個系統中新位置的使用</li>
    </ul> <p>任務涵蓋的位置包括：</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>對於較大型目錄，會將下列Java系統屬性傳遞至以下位置，以重新命令它個別執行商務移轉任務AEM:</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>遷移後AEM需要重新啟動。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

