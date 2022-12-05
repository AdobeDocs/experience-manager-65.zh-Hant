---
title: 封裝的Token支援
seo-title: Encapsulated Token Support
description: 了解AEM中的封裝代號支援。
seo-description: Learn about the Encapsulated Token support in AEM.
uuid: a7c6f269-bb5a-49ba-abef-ea029202ab6d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 2c263c0d-2521-49df-88ba-f304a25af8ab
exl-id: e24d815c-83e2-4639-8273-b4c0a6bb008a
source-git-commit: f8d249f5d3fac243b4989c3eca4be2730dcf16ec
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# 封裝的Token支援{#encapsulated-token-support}

## 簡介 {#introduction}

依預設，AEM會使用Token Authentication Handler來驗證每個要求。 但是，為了提供驗證請求，令牌身份驗證處理程式要求對每個請求都訪問儲存庫。 這是因為使用Cookie來維護驗證狀態。 邏輯上，狀態必須保存在存放庫中，才能驗證後續的請求。 實際上，這表示驗證機制有狀態。

這對於橫向可擴充性尤其重要。 在如下所示的發佈伺服器陣列等多執行個體設定中，無法以最佳方式達成負載平衡。 使用有狀態驗證時，持續的驗證狀態將僅在使用者首次驗證的執行個體上可用。

![chlimage_1-33](assets/chlimage_1-33a.png)

以下列案例為例：

使用者可能會在發佈執行個體1上進行驗證，但如果後續請求進入發佈執行個體2，該執行個體就不會有持續的驗證狀態，因為該狀態持續存在於發佈執行個體的存放庫中，而發佈執行個體的存放庫則有其專屬的存放庫。

解決方案是在負載平衡器層級設定黏著連線。 有了黏著連線，使用者一律會被導向至相同的發佈例項。 因此，不可能真正實現最佳負載平衡。

如果發佈例項無法使用，在該例項上驗證的所有使用者都會失去工作階段。 這是因為驗證Cookie需要存放庫存取權。

## 使用封裝令牌的無狀態身份驗證 {#stateless-authentication-with-the-encapsulated-token}

橫向可擴充性的解決方案是使用AEM中新的封裝Token支援進行無狀態驗證。

封裝代號是密碼學的一部分，可讓AEM安全地離線建立和驗證驗證資訊，而不需存取存放庫。 如此一來，驗證要求便可在所有發佈執行個體上發生，且不需要黏著連線。 它還具有提高身份驗證效能的優勢，因為不需要為每個身份驗證請求訪問儲存庫。

您可以透過以下的MongoMK作者和TarMK發佈執行個體，了解這項功能在分散於不同地理位置的部署中的運作方式：

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>請注意，封裝令牌與身份驗證有關。 這可確保無須存取存放庫即可驗證Cookie。 但是，用戶仍必須存在於所有實例上，並且儲存在該用戶下的資訊可由每個實例訪問。
>
>例如，如果因封裝代號的運作方式，在發佈執行個體編號1上建立新使用者，則會在發佈編號2上成功驗證該使用者。 如果使用者不存在於第二個發佈例項上，要求仍不會成功。

## 設定封裝的Token {#configuring-the-encapsulated-token}

>[!NOTE]
>只有符合下列條件時，同步使用者並仰賴Token驗證（例如SAML和OAuth）的所有驗證處理常式，才能搭配封裝的Token運作：
>
>* 黏著工作階段已啟用，或
>
>* 同步開始時，已在AEM中建立使用者。 這表示在處理常式中，將不支援封裝的Token **建立** 使用者。


設定封裝代號時，您需要考慮一些事項：

1. 由於涉及密碼學，所有實例都需要具有相同的HMAC密鑰。 自AEM 6.3以來，關鍵資料不再儲存在儲存庫中，而是儲存在實際檔案系統中。 考慮到這一點，複製密鑰的最佳方式是將密鑰從源實例的檔案系統複製到要複製密鑰的目標實例的檔案系統。 請參閱下方的「複製HMAC金鑰」下方的更多資訊。
1. 必須啟用封裝代號。 這可透過Web主控台完成。

### 複製HMAC密鑰 {#replicating-the-hmac-key}

若要跨執行個體復寫金鑰，您必須：

1. 存取AEM例項，通常為製作例項，其中包含要複製的重要資料；
1. 找出 `com.adobe.granite.crypto.file` 在本機檔案系統中捆綁。 例如，在此路徑下：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   此 `bundle.info` 每個資料夾內的檔案會識別套件組合名稱。

1. 導覽至資料夾。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 複製HMAC和主檔案。
1. 接著，前往您要複製HMAC金鑰的目標執行個體，並導覽至資料夾。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 貼上您先前複製的兩個檔案。
1. [刷新加密包](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 如果目標實例已在運行。

1. 對於要將密鑰複製到的所有實例，重複上述步驟。

#### 啟用封裝的Token {#enabling-the-encapsulated-token}

複製HMAC密鑰後，您可以通過Web控制台啟用封裝令牌：

1. 將瀏覽器指向 `https://serveraddress:port/system/console/configMgr`
1. 尋找名為 **AdobeGranite代號驗證處理常式** 然後按一下。
1. 在下列視窗中，勾選 **啟用封裝的Token支援** 框和按 **儲存**.
