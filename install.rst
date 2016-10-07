安裝步驟與秘訣
=======================

主要安裝步驟可以查閱 Umbraco `安裝說明網頁`_\ ，另外可以參考本書建議：用 Nuget 方法，先將檔案部分安裝在本機資料夾中，同時連結遠端資料庫，最後在將檔案資料複製到遠端伺服器中。


下載檔案
----------------

設定專案：

- 在本地電腦中開啟 Visual Studio 2015，選 ASP.Net 空白專案 + 測試專案
- 按照官網的 NuGet\ `安裝方式`_，在 NuGet 命令列中輸入 ``Install-Package UmbracoCms``


設定資料庫：

- 伺服器的資料庫種類必須為 MS SQL Server，不可以用 MySQL，會出安裝問題
- 新增資料庫和使用者名稱密碼


調整網頁設定：

- 檔案 web.config 的 ``<system.web>`` 區段中增加 ``<trust level="Full" />``
- 修改偵錯設定，或到檔案 web.Debug.config 中增加 ``<customErrors mode="Off" />``


設定目錄權限：

- 如果在本地機器用 VS 2015 安裝，則不需要調整
- 直接安裝在遠端伺服器時，安裝前需按照\ `官網連結`_\ 內容設定資料夾存取權限


執行安裝程式
----------------

啟動網頁：

- 在 VS 2015 中按下 Ctrl-F5 開啟瀏覽器
- 設定完新使用者名稱密碼後，選擇 Custom (而不是直接安裝才能設定資料庫）
- 選擇 Microsoft SQL Server
- 若安裝一切正常後，就會出現後台畫面


後台設定：

- 刪除 Content 底下的不需要資料


安裝收尾
----------------

如果將網頁原始碼放在版本管理中，記得調整安全相關項目：

- web.config 中 connectionStrings 移到另外的檔案，並改成 ``<connectionStrings configSource="Web.Secret.config"/>``
- web.config 中 email smtp 設定移到另外的檔案，改成 ``<smtp configSource="WebMail.secret.config" />``


細部調整：

- 管理後台進入 Developer -> Health Check -> 執行 Check All Group
- 檔案 web.config 中改回 ``<customErrors mode="Remote" />``


網頁部署
----------------

設定目錄權限：

-  按照\ `官網連結`_\ 將不需要最高權限的資料夾改回來
-  自動化權限設定：參考\ `網頁教學`_\ 設定，新增檔案 ``<projectName>.wpp.targets`` 在專案資料夾中，之後執行網頁部署（Web Deploy）時皆可自動設定


同步檔案：

-  自動化同步其他檔案（\ `網頁教學 <https://www.asp.net/mvc/overview/deployment/visual-studio-web-deployment/deploying-extra-files>`__\ ）



.. _安裝說明網頁: https://our.umbraco.org/documentation/Getting-Started/Setup/Install/
.. _安裝方式: https://our.umbraco.org/documentation/Getting-Started/Setup/Install/install-umbraco-with-nuget
.. _官網連結: https://our.umbraco.org/documentation/Getting-Started/Setup/Install/permissions
.. _網頁教學: http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx
