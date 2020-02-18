---
title: 應用程式伺服器安裝的升級步驟
seo-title: 應用程式伺服器安裝的升級步驟
description: 瞭解如何升級透過應用程式伺服器部署的AEM例項。
seo-description: 瞭解如何升級透過應用程式伺服器部署的AEM例項。
uuid: e4020966-737c-40ea-bfaa-c63ab9a29cee
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 1876d8d6-bffa-4a1c-99c0-f6001acea825
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e

---


# 應用程式伺服器安裝的升級步驟{#upgrade-steps-for-application-server-installations}

本節說明更新AEM for Application server安裝所需遵循的程式。

此程式中的所有範例都使用JBoss做為應用程式伺服器，並暗示您已部署AEM的工作版本。 此程式旨在記錄從 **AEM 5.6版到6.3版所執行的升級**。

1. 首先，啟動JBoss。 在大多數情況下，您可以通過運行啟動腳 `standalone.sh` 本，從終端機運行以下命令來執行此操作：

   ```shell
   jboss-install-folder/bin/standalone.sh
   ```

1. 如果已部署AEM 5.6，請執行下列動作，檢查組合是否運作正常：

   ```shell
   wget https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 接著，取消部署AEM 5.6:

   ```shell
   rm jboss-install-folder/standalone/deployments/cq.war
   ```

1. 停止JBoss。

1. 現在，使用crx2oak移轉工具移轉儲存庫：

   ```shell
   java -jar crx2oak.jar crx-quickstart/repository/ crx-quickstart/oak-repository
   ```

   >[!NOTE]
   >
   >在此示例中，oak-repository是新轉換的儲存庫將駐留的臨時目錄。 在執行此步驟之前，請確定您有最新的crx2oak.jar版本。

1. 請執行下列動作，刪除sling.properties檔案中的必要屬性：

   1. 開啟位於 `crx-quickstart/launchpad/sling.properties`
   1. 步驟文字移除下列屬性並儲存檔案：

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. 移除不再需要的檔案和檔案夾。 您需要特別移除的項目包括：

   * launchpad/ **startup資料夾**。 通過在終端機中運行以下命令可以刪除它： `rm -rf crx-quickstart/launchpad/startup`

   * base. **jar檔案**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * BootstrapCommandFile_timestamp.txt **檔案**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

1. 將新移轉的區段儲存區複製至其適當位置：

   ```shell
   mv crx-quickstart/oak-repository/segmentstore crx-quickstart/repository/segmentstore
   ```

1. 也複製資料儲存：

   ```shell
   mv crx-quickstart/repository/repository/datastore crx-quickstart/repository/datastore
   ```

1. 接下來，您需要建立包含將與新升級實例一起使用的OSGi配置的資料夾。 更具體地說，需要在 **crx-quickstart下建立名為install的資料夾**。

1. 現在，請建立將與AEM 6.3搭配使用的節點儲存區和資料儲存區。通過在 **crx-quickstart\install下建立兩個具有以下名稱的檔案，可以執行此操作**:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`

   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`
   這兩個檔案將設定AEM使用TarMK節點儲存區和檔案資料儲存區。

1. 編輯配置檔案以使其可供使用。 更具體地說：

   * 將下列行新 **增至org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**:\
      `customBlobStore=true`

   * 然後，將下列行新 **增至org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**:

      ```
      path=./crx-quickstart/repository/datastore
       minRecordLength=4096
      ```

1. 執行下列動作以移除crx2執行模式：

   ```shell
   find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \
   ```

1. 您現在需要變更AEM 6.3 war檔案中的執行模式。 為此，請先建立暫存檔案夾，以容納AEM 6.3戰爭。 此示例中資料夾的名稱將為 **temp**。 複製war檔案後，從temp資料夾內運行以提取其內容：

   ```shell
   jar xvf aem-quickstart-6.3.0.war
   ```

1. 提取內容後，移至 **WEB-INF檔案夾並編輯**`web.xml` 檔案以變更執行模式。 要查找在XML中設定它們的位置，請查找字 `sling.run.modes` 符串。 找到後，請變更下一行程式碼中的執行模式，依預設會設為編寫：

   ```shell
   <param-value >author</param-value>
   ```

1. 將上述作者值變更，並將執行模式設為：author,crx3,crx3tar程式碼的最後區塊應如下所示：

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 使用已修改的內容重新建立jar:

   ```shell
   jar cvf aem62.war
   ```

1. 最後，部署新的war檔案：

   ```shell
   cp temp/aem62.war jboss-install-folder/standalone/deployments/aem61.war
   ```

