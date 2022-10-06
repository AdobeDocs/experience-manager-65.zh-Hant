---
title: 管理HSM憑據
seo-title: Managing HSM credentials
description: 了解如何管理HSM憑據。
seo-description: Learn how to manage HSM credentials.
uuid: 30ddcd4a-f771-44d5-bdef-4826adcd0c44
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5f17ba8-8aab-4449-811a-20ad33de1c6f
exl-id: facbeab2-de95-4778-894c-faa771d3391e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 0%

---

# 管理HSM憑據 {#managing-hsm-credentials}

從「信任儲存管理」頁，您可以管理硬體安全模組(HSM)憑據。 HSM是第三方PKCS#11設備，可用於安全地生成和儲存私鑰。 HSM實際上保護了對私鑰的訪問和使用。

需要客戶端軟體才能與HSM通信。 HSM客戶端軟體必須安裝並配置在與AEM表單相同的電腦上。

AEM forms數字簽名可以使用儲存在HSM上的憑據來應用伺服器端數字簽名。 按照本節中的說明，為數字簽名將使用的每個HSM憑據建立別名。 別名包含HSM所需的所有參數。

>[!NOTE]
>
>更改HSM配置後，重新啟動AEM Forms伺服器。

## 在HSM設備聯機時為HSM憑據建立別名 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「HSM憑據」，然後按一下「添加」。
1. 在「設定檔名稱」方塊中，輸入用來識別別名的字串。 此值用作某些數字簽名操作（如簽名簽名欄位操作）的屬性。
1. 在「PKCS11庫」框中，在伺服器上鍵入HSM客戶端庫的完全限定路徑。 例如， `c:\Program Files\LunaSA\cryptoki.dll`. 在群集環境中，此路徑對於群集中的所有伺服器必須相同。
1. 按一下測試HSM連接。 如果AEM表單能夠連接到HSM設備，則會顯示一條消息，指出HSM可用。 按一下下一步。
1. 使用令牌名稱、插槽ID或插槽清單索引來標識HSM上儲存憑據的位置。

   * **代號名稱：** 與要使用的HSM分區的名稱（例如HSMPART1）相對應。
   * **插槽Id:** 插槽ID是長資料類型的插槽標識符。
   * **插槽清單索引：** 如果選擇「插槽清單索引」，請將「插槽資訊」設定為與插槽對應的整數。 這是一個基於0的索引，這意味著如果客戶端先註冊到HSMPART1分區，則HSMPART1將使用SlotListIndex值0引用。

1. 在Token Pin框中，鍵入訪問HSM密鑰所需的密碼，然後按一下Next。
1. 在「憑據」框中，選擇憑據。 按一下「儲存」。

## 在HSM設備離線時為HSM憑據建立別名 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「HSM憑據」，然後按一下「添加」。
1. 在「設定檔名稱」方塊中，輸入用來識別別名的字串。 此值用作某些數字簽名操作（如簽名簽名欄位操作）的屬性。
1. 在「PKCS11庫」框中，在伺服器上鍵入HSM客戶端庫的完全限定路徑。 例如， `c:\Program Files\LunaSA\cryptoki.dll`. 在群集環境中，此路徑對於群集中的所有伺服器必須相同。
1. 選取「離線設定檔建立」核取方塊。 按一下下一步。
1. 在「HSM設備」清單中，選擇儲存憑據的HSM設備的製造商。
1. 在「槽類型」清單中，選擇「槽ID」、「槽索引」或「令牌名稱」，並在「槽資訊」框中指定值。 AEM Forms使用這些設定來確定HSM上儲存憑據的位置。

   * **代號名稱：** 與分區名稱（如HSMPART1）對應。
   * **插槽Id:** 插槽ID是與插槽對應的整數，插槽又與分區對應。 例如，首先向HSMPART1分區註冊的客戶端（表單伺服器）。 這將此客戶端的插槽1映射到HSMPART1分區。 由於HSMPART1是註冊的第一個分區，因此插槽ID為1，您可將插槽資訊設定為1。

      插槽ID是逐個用戶端設定。 如果您將第二台電腦註冊到不同的分區（例如，同一HSM設備上的HSMPART2），則插槽1將與該客戶機的HSMPART2分區相關聯。

   * **插槽索引：** 如果選擇「插槽索引」，請將「插槽資訊」設定為與插槽對應的整數。 這是一個基於0的索引，這意味著如果客戶端先註冊到HSMPART1分區，則插槽1將映射到此客戶端的HSMPART1。 由於HSMPART1是註冊的第一個分區，因此插槽索引為0。

1. 選取下列其中一個選項，並提供路徑：

   * **憑證**:（若使用SHA1則非必要）按一下「瀏覽」 ，然後找到您所使用憑證的公開金鑰路徑。
   * **證書SHA1:** （如果使用物理證書，則不需要）為使用的憑據鍵入公鑰(.cer)檔案的SHA1值（指紋）。 請確定SHA1值中沒有使用空格。

1. 在「密碼」框中，鍵入訪問給定插槽資訊的HSM密鑰所需的密碼，然後按一下「保存」。

## 查看HSM憑據別名屬性 {#view-hsm-credential-alias-properties}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「HSM憑據」。
1. 按一下憑據別名的別名以查看屬性，然後按一下確定。

## 檢查HSM憑據的狀態 {#check-the-status-of-an-hsm-credential}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「HSM憑據」。
1. 按一下要檢查的憑據旁邊的複選框，然後按一下檢查狀態。

狀態列反映憑據的當前狀態。 如果失敗，「狀態」欄中會顯示紅色X。 將滑鼠移到X上，可顯示包含失敗原因的工具提示。

## 更新HSM憑據別名屬性 {#update-hsm-credential-alias-properties}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「HSM憑據」。
1. 按一下憑據別名的別名。
1. 按一下「更新憑據」，然後根據需要更新設定。

## 重置所有HSM連接 {#reset-all-hsm-connections}

在表單伺服器和HSM設備之間的網路會話出現任何中斷後，重置與HSM設備的開啟連接。 例如，由於網路中斷或HSM設備離線進行軟體更新，可能會發生中斷。 中斷後，現有連線會過時，且對這些連線提出的任何簽署要求都會失敗。 使用「重置所有HSM連接」選項可清除舊連接。

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「HSM憑據」。
1. 按一下「重置所有HSM連接」。

## 刪除HSM憑據別名 {#delete-an-hsm-credential-alias}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「HSM憑據」。
1. 選擇要刪除的HSM憑據的複選框，按一下「刪除」，然後按一下「確定」。

## 配置遠程HSM支援 {#configure-remote-hsm-support}

AEM表單使用以Web服務為基礎的IPC/RPC機制。 此機制使AEM表單能夠使用安裝在遠程電腦上的HSM。 要使用此功能，請在安裝HSM的遠程電腦上安裝Web服務。 請參閱 [在Windows 64位平台上使用Sun JDK為AEM表單ES配置HSM支援](https://kb2.adobe.com/cps/808/cpsid_80835.html)以取得更多資訊。

此機制不支援線上建立HSM配置檔案或狀態檢查。 但是，有兩種方法可以建立HSM配置檔案和執行狀態檢查：

* 傳遞簽署者憑證，以建立AEM表單用戶端憑證。 請依照 [在Windows 64位平台上使用Sun JDK為AEM表單ES配置HSM支援](https://kb2.adobe.com/cps/808/cpsid_80835.html). Web服務位置以憑據屬性的形式傳入。 也支援使用憑證碼或憑證SHA-1十六進位來建立離線HSM設定檔。 不過，如果您已從舊版AEM表單升級至AEM表單，請變更用戶端，因為憑證包含憑證和網站服務資訊。
* Web服務位置在簽名服務的管理控制台中指定。 (請參閱 [簽名服務設定](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings).) 在此，客戶端僅在信任儲存中攜帶HSM配置檔案的別名。 即使您已從舊版AEM表單升級至AEM表單，您仍可順暢地使用此選項，而不需進行任何用戶端變更。 此選項不支援使用證書SHA-1的HSM配置檔案。
