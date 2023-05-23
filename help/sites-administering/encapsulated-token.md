---
title: 封裝的令牌支援
seo-title: Encapsulated Token Support
description: 瞭解中的封裝令牌支援AEM。
seo-description: Learn about the Encapsulated Token support in AEM.
uuid: a7c6f269-bb5a-49ba-abef-ea029202ab6d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 2c263c0d-2521-49df-88ba-f304a25af8ab
exl-id: e24d815c-83e2-4639-8273-b4c0a6bb008a
source-git-commit: ed2cb35593780cd627c15f493e58d3b68c55519b
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# 封裝的令牌支援{#encapsulated-token-support}

## 簡介 {#introduction}

預設情況下，AEM使用令牌驗證處理程式對每個請求進行身份驗證。 但是，為了提供身份驗證請求，令牌身份驗證處理程式要求對每個請求都訪問儲存庫。 這是因為使用cookie來維護身份驗證狀態。 從邏輯上講，需要將狀態保留在儲存庫中，以驗證後續請求。 實際上，這意味著認證機制是有狀態的。

這對於橫向可擴充性尤其重要。 在如下所示的發佈場等多實例設定中，無法以最佳方式實現負載平衡。 使用狀態身份驗證時，保留的身份驗證狀態將僅在用戶首次進行身份驗證的實例上可用。

![chlimage_1-33](assets/chlimage_1-33a.png)

以下方案為例：

在發佈實例1上可以對用戶進行身份驗證，但如果後續請求發佈實例2，則該實例不具有該持久驗證狀態，因為該狀態被保留在發佈實例的儲存庫中，而發佈實例的儲存庫具有其自己的儲存庫。

解決方案是在負載平衡器級別配置粘滯連接。 使用粘滯連接時，用戶將始終定向到同一發佈實例。 因此，不可能實現真正最優的負載平衡。

如果發佈實例不可用，在該實例上經過身份驗證的所有用戶都將丟失其會話。 這是因為驗證身份驗證cookie需要儲存庫訪問。

## 使用封裝令牌的無狀態身份驗證 {#stateless-authentication-with-the-encapsulated-token}

橫向擴展的解決方案是使用中新的封裝令牌支援進行無狀態驗AEM證。

封裝令牌是一種密碼學，它允許AEM在不訪問儲存庫的情況下安全地建立和驗證身份驗證資訊。 這樣，所有發佈實例上都可以發生身份驗證請求，而無需粘滯連接。 它還具有提高身份驗證效能的優勢，因為無需為每個身份驗證請求訪問儲存庫。

您可以在MongoMK作者和TarMK發佈實例的地理分佈部署中看到其工作原理：

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>請注意，封裝的令牌與身份驗證有關。 它確保可以驗證Cookie而無需訪問儲存庫。 但是，仍然需要用戶存在於所有實例上，並且每個實例都可以訪問儲存在該用戶下的資訊。
>
>例如，如果在發佈實例編號1上建立了新用戶，則由於封裝令牌的工作方式，將在發佈編號2上成功對其進行身份驗證。 如果用戶在第二個發佈實例上不存在，則請求仍將不成功。

## 配置封裝的令牌 {#configuring-the-encapsulated-token}

>[!NOTE]
>所有同步用戶並依賴令牌身份驗證（如SAML和OAuth）的身份驗證處理程式僅在以下情況下才能使用封裝的令牌：
>
>* 已啟用粘滯會話，或
>
>* 啟動同步時已AEM在中建立用戶。 這意味著在處理程式處於以下情況下將不支援封裝的令牌 **建立** 用戶。


配置封裝令牌時需要考慮以下幾點：

1. 由於涉及密碼學，所有實例都需要具有相同的HMAC密鑰。 自AEM6.3以來，密鑰材料不再儲存在儲存庫中，而儲存在實際檔案系統中。 考慮到這一點，複製密鑰的最佳方法是將它們從源實例的檔案系統複製到要複製密鑰的目標實例的檔案系統。 請參閱下面的「複製HMAC密鑰」下的詳細資訊。
1. 需要啟用封裝的令牌。 這可以通過Web控制台完成。

### 複製HMAC密鑰 {#replicating-the-hmac-key}

為了跨實例複製密鑰，您需要：

1. 訪問AEM包含要複製的關鍵材料的實例（通常為作者實例）;
1. 查找 `com.adobe.granite.crypto.file` 本地檔案系統中的綁定。 例如，在此路徑下：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25`

   的 `bundle.info` 每個資料夾中的檔案將標識包名稱。

1. 導航到資料資料夾。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. 複製HMAC和主檔案。
1. 然後，轉到要將HMAC密鑰複製到的目標實例，然後導航到資料資料夾。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. 貼上以前複製的兩個檔案。
1. [刷新加密包](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 目標實例已在運行。

1. 對要將密鑰複製到的所有實例重複上述步驟。

#### 啟用封裝的令牌 {#enabling-the-encapsulated-token}

複製HMAC密鑰後，您可以通過Web控制台啟用封裝令牌：

1. 將瀏覽器指向 `https://serveraddress:port/system/console/configMgr`
1. 查找名為 **Adobe花崗岩令牌驗證處理程式** 點擊它。
1. 在以下窗口中，勾選 **啟用封裝的令牌支援** 按框 **保存**。
