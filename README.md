# 円本位账本（离线版）

以日元为本位币的多币种记账。程序放在 GitHub Pages 上，记账数据只存在你的 iPhone 里（IndexedDB），不会上传到任何地方。

## 文件

- `index.html`：程序本体
- `sw.js`：离线缓存，没网也能打开
- `manifest.webmanifest`、`icons/`：主屏幕图标和名称

## 一、部署到 GitHub Pages（一次性，用电脑做比较方便）

1. 登录 GitHub，新建仓库，名字比如 `yen-ledger`，选 **Public**（免费账号的 Pages 只支持公开仓库）。
   仓库里只有程序，没有任何记账数据，公开没有关系。
2. 在仓库页面点 **Add file → Upload files**，把解压后的所有文件拖进去，包括整个 `icons` 文件夹，然后点 **Commit changes**。
3. 打开仓库的 **Settings → Pages**，在 Build and deployment 里选 **Deploy from a branch**，Branch 选 `main`，目录选 `/ (root)`，点 Save。
4. 等一两分钟，页面上方会显示网址，形如 `https://你的用户名.github.io/yen-ledger/`。

不想用 GitHub 的话，任何支持 HTTPS 的静态托管都可以，比如 Cloudflare Pages，或者你自己的域名。

## 二、装到 iPhone

1. 用 **Safari** 打开上面的网址。
2. 点底部的分享按钮 → **添加到主屏幕** → 添加。
3. 以后**一律从主屏幕图标打开**。iOS 上，主屏幕 App 和 Safari 标签页的数据是分开存的，在 Safari 里记的账，主屏幕 App 里看不到。
4. 第一次打开时要联网，它会顺便拉取汇率。之后断网也能正常记账。

## 三、备份（重要）

数据只在这台 iPhone 上。删掉主屏幕图标、换手机，或者在系统设置里清除网站数据，记录都会消失。

- 在「账户」页点 **导出备份**，在分享菜单里选 **存储到文件**，存到 iCloud Drive。
- 超过 14 天没备份时，明细页顶部会提醒你。
- 换手机或误删后：装好 App，在「账户」页点 **从备份恢复**，选那个 `.json` 文件。恢复会替换当前设备上的全部数据。

## 汇率

- 联网打开 App 时，如果距离上次更新超过 6 小时，会自动从 fawazahmed0/currency-api 拉取每日参考汇率；在「汇率」页也可以点「立即更新」。
- 断网时继续用最后一次保存的汇率。
- 每笔账会锁定记账当天折合的日元金额，之后汇率变化不影响历史统计。
- 某个币种需要特定汇率时，可以在「汇率」页点那一行手动修改；下一次自动更新拿到新数据后，会恢复使用自动汇率。

## 隐私

App 只会发出两类网络请求：拉取汇率（jsDelivr / Cloudflare）和加载字体（Google Fonts）。记账内容不会离开你的设备。

## 以后更新程序

1. 用新文件覆盖仓库里的旧文件。
2. 把 `sw.js` 第 4 行 `VERSION` 的数字加一，比如 `yen-ledger-v2`。
3. iPhone 联网打开一次 App，就会换成新版本，数据不受影响。
