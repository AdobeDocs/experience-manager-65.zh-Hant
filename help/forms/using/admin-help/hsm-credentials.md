---
title: 管理HSM憑據
seo-title: Managing HSM credentials
description: 瞭解如何管理HSM憑據。
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

在「信任儲存管理」頁中，可以管理硬體安全模組(HSM)憑據。 HSM是第三方PKCS#11設備，您可以使用它安全地生成和儲存私鑰。 HSM在物理上保護對私鑰的訪問和使用。

客戶端軟體需要與HSM通信。 HSM客戶端軟體必須安裝並配置在與表單相同的計AEM算機上。

表AEM單數字簽名可以使用HSM上儲存的憑據應用伺服器端的數字簽名。 按照本節中的說明為數字簽名將使用的每個HSM憑據建立別名。 別名包含HSM所需的所有參數。

>[!NOTE]
>
>更改HSM配置後，重新啟AEM動表單伺服器。

## 在HSM設備聯機時為HSM憑據建立別名 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「HSM憑據」，然後按一下「添加」。
1. 在「配置檔案名稱」框中，鍵入用於標識別名的字串。 此值用作某些數字簽名操作的屬性，如簽名欄位操作。
1. 在「PKCS11庫」框中，在伺服器上鍵入HSM客戶端庫的完全限定路徑。 比如說， `c:\Program Files\LunaSA\cryptoki.dll`。 在群集環境中，此路徑對於群集中的所有伺服器必須相同。
1. 按一下「TestHSM連接」。 如AEM果表單能夠連接到HSM設備，則會顯示一條消息，指出HSM可用。 按一下下一步。
1. 使用令牌名稱、插槽ID或插槽清單索引來標識憑據在HSM上的儲存位置。

   * **令牌名稱：** 與要使用的HSM分區的名稱（例如HSMPART1）相對應。
   * **插槽ID:** 插槽ID是類型為long的資料類型的插槽標識符。
   * **插槽清單索引：** 如果選擇「插槽清單索引」，請將「插槽資訊」設定為與插槽對應的整數。 這是一個基於0的索引，這意味著如果客戶端首先註冊到HSMPART1分區，則將使用SlotListIndex值0引用HSMPART1。

1. 在「令牌管腳」框中，鍵入訪問HSM密鑰所需的密碼，然後按一下「下一步」。
1. 在「憑據」框中，選擇憑據。 按一下「儲存」。

## 在HSM設備離線時為HSM憑據建立別名 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「HSM憑據」，然後按一下「添加」。
1. 在「配置檔案名稱」框中，鍵入用於標識別名的字串。 此值用作某些數字簽名操作的屬性，如簽名欄位操作。
1. 在「PKCS11庫」框中，在伺服器上鍵入HSM客戶端庫的完全限定路徑。 比如說， `c:\Program Files\LunaSA\cryptoki.dll`。 在群集環境中，此路徑對於群集中的所有伺服器必須相同。
1. 選中「離線配置檔案建立」複選框。 按一下下一步。
1. 在HSM設備清單中，選擇儲存憑據的HSM設備的製造商。
1. 在「插槽類型」清單中，選擇「插槽ID」、「插槽索引」或「標籤名稱」，然後在「插槽資訊」框中指定值。 表AEM單使用這些設定來確定HSM上儲存憑據的位置。

   * **令牌名稱：** 與分區名稱（例如，HSMPART1）對應。
   * **插槽ID:** 插槽ID是與插槽對應的整數，插槽又與分區對應。 例如，客戶端（表單伺服器）首先註冊到HSMPART1分區。 此客戶端的插槽1映射到HSMPART1分區。 由於HSMPART1是註冊的第一個分區，因此插槽ID為1，您會將「插槽資訊」設定為1。

      插槽ID是按客戶端逐個設定的。 如果將第二台電腦註冊到不同的分區（例如，在同一HSM設備上的HSMPART2），則插槽1將與該客戶機的HSMPART2分區相關聯。

   * **插槽索引：** 如果選擇「插槽索引」，請將「插槽資訊」設定為與插槽對應的整數。 這是一個基於0的索引，這意味著如果客戶端首先註冊到HSMPART1分區，則插槽1將映射到此客戶端的HSMPART1。 由於HSMPART1是已註冊的第一個分區，因此插槽索引為0。

1. 選擇以下選項之一併提供路徑：

   * **證書**:（使用SHA1時不需要）按一下「瀏覽」並找到您使用的憑據的公鑰路徑。
   * **證書SHA1:** （使用物理證書時不需要）為您使用的憑據鍵入公鑰(.cer)檔案的SHA1值（指紋）。 確保SHA1值中沒有使用空格。

1. 在「密碼」框中，鍵入訪問給定插槽資訊的HSM密鑰所需的密碼，然後按一下「保存」。

## 查看HSM憑據別名屬性 {#view-hsm-credential-alias-properties}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「HSM憑據」。
1. 按一下憑據別名的別名以查看屬性，然後按一下確定。

## 檢查HSM憑據的狀態 {#check-the-status-of-an-hsm-credential}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「HSM憑據」。
1. 按一下要檢查的憑據旁邊的複選框，然後按一下「檢查狀態」。

「狀態」列反映憑據的當前狀態。 如果失敗，「狀態」(Status)列中將顯示紅色X。 將滑鼠懸停在X上，顯示包含故障原因的工具提示。

## 更新HSM憑據別名屬性 {#update-hsm-credential-alias-properties}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「HSM憑據」。
1. 按一下憑據別名的別名。
1. 按一下「更新憑據」，然後根據需要更新設定。

## 重置所有HSM連接 {#reset-all-hsm-connections}

在表單伺服器和HSM設備之間的網路會話中斷後，重設到HSM設備的開放連接。 例如，由於網路中斷或HSM設備離線以進行軟體更新，可能會造成中斷。 中斷後，現有連接已過時，針對這些連接的任何簽名請求都將失敗。 使用「重置所有HSM連接」選項清除舊連接。

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「HSM憑據」。
1. 按一下「重置所有HSM連接」。

## 刪除HSM憑據別名 {#delete-an-hsm-credential-alias}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「HSM憑據」。
1. 選中要刪除的HSM憑據的複選框，按一下刪除，然後按一下確定。

## 配置遠程HSM支援 {#configure-remote-hsm-support}

表AEM單使用基於Web服務的IPC/RPC機制。 此機制使AEM表單能夠使用安裝在遠程電腦上的HSM。 要使用此功能，請在安裝HSM的遠程電腦上安裝Web服務。 請參閱 [在Windows 64位平AEM台上使用Sun JDK為表單ES配置HSM支援](https://kb2.adobe.com/cps/808/cpsid_80835.html)的子菜單。

此機制不支援線上建立HSM配置檔案或狀態檢查。 但是，有兩種方法可建立HSM配置檔案並執行狀態檢查：

* 通過將AEM表單客戶端憑據傳遞給簽名者的證書來建立該憑據。 按照中的步驟操作 [在Windows 64位平AEM台上使用Sun JDK為表單ES配置HSM支援](https://kb2.adobe.com/cps/808/cpsid_80835.html)。 Web服務位置作為憑據屬性傳入。 還支援使用證書檔案或證書SHA-1十六進位建立離線HSM配置檔案。 但是，如果您已從早期版本AEM的表單升級到表AEM單，請更改客戶端，因為憑據帶有證書和Web服務資訊。
* Web服務位置是在簽名服務的管理控制台中指定的。 (請參閱 [簽名服務設定](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings)。) 在此，客戶端只在信任儲存中帶有HSM配置檔案的別名。 即使您已從早期版本的表單升級到表單，也可以無縫AEM地使用此選項，而不需要任何客AEM戶端更改。 此選項不支援使用證書SHA-1的HSM配置檔案。
