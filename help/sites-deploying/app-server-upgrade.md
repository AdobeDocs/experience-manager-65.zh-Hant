---
title: 應用程式伺服器安裝的升級步驟
description: 了解如何升級透過應用程式伺服器部署的AEM例項。
feature: Upgrading
exl-id: 86dd10ae-7f16-40c8-84b6-91ff2973a523
source-git-commit: 5e875e0420540ca209e7d677046e8d010ae4e145
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# 應用程式伺服器安裝的升級步驟{#upgrade-steps-for-application-server-installations}

本節介紹為了更新AEM以安裝應用程式伺服器而需要遵循的過程。

此過程中的所有示例都使用Tomcat作為應用程式伺服器，並暗示您已部署了AEM的工作版本。 此程式旨在記錄從 **AEM 6.4版至6.5版**.

1. 首先，啟動TomCat。 在大多數情況下，您可以執行 `./catalina.sh` 通過從終端運行此命令來啟動啟動指令碼：

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. 如果已部署AEM 6.4，請存取以下項目，以檢查套件組合是否正常運作：

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 接下來，取消部署AEM 6.4。這可從TomCat App Manager(`http://serveraddress:serverport/manager/html`)

1. 現在，使用crx2oak移轉工具移轉存放庫。 若要這麼做，請從下載最新版crx2oak [此位置](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/).

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -XX:MaxPermSize=2048M -jar crx2oak.jar --load-profile segment-fds
   ```

1. 請執行下列動作，刪除sling.properties檔案中的必要屬性：

   1. 開啟位於的檔案 `crx-quickstart/launchpad/sling.properties`
   1. 步驟文字移除下列屬性並儲存檔案：

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. 移除不再需要的檔案和資料夾。 您需要明確移除的項目包括：

   * 此 **launchpad/startup資料夾**. 您可以在終端機中執行下列命令以刪除它： `rm -rf crx-quickstart/launchpad/startup`

   * 此 **base.jar檔案**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * 此 **BootstrapCommandFile_timestamp.txt檔案**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * 移除 **sling.options.file** 執行時： `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. 現在，建立將與AEM 6.5搭配使用的節點儲存區和資料儲存區。您可以在下方建立兩個檔案，其名稱如下 `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   這兩個檔案會將AEM設定為使用TarMK節點存放區和檔案資料存放區。

1. 編輯組態檔，使其可供使用。 更具體而言：

   * 將下列行新增至 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

      `customBlobStore=true`

   * 然後將下列行加入 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

      ```
      path=./crx-quickstart/repository/datastore
      minRecordLength=4096
      ```

1. 您現在需要變更AEM 6.5 war檔案中的執行模式。 為此，首先建立一個臨時資料夾，用於容納AEM 6.5戰爭。 此範例中的資料夾名稱為 `temp`. 複製戰爭檔案後，從臨時資料夾內執行以擷取其內容：

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. 擷取內容後，請前往 **WEB-INF** 資料夾和編輯web.xml檔案以更改運行模式。 要查找XML中設定它們的位置，請查找 `sling.run.modes` 字串。 找到此檔案後，請變更下一行程式碼中的執行模式，預設會將其設為製作：

   ```bash
   <param-value >author</param-value>
   ```

1. 將上述製作值變更，並將執行模式設為： `author,crx3,crx3tar`. 程式碼的最後一個區塊應如下所示：

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 使用已修改的內容重新建立jar:

   ```bash
   jar cvf aem65.war
   ```

1. 最後，在TomCat中部署新的戰爭檔案。
