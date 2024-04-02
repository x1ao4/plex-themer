# plex-themer
使用 plex-themer 可以轻松为 Plex 媒体库内的电影、电视节目、歌手和合集管理主题音乐，它由两个脚本组成：`plex-theme-uploader.py` 用于上传主题音乐，`plex-theme-deleter.py` 用于删除主题音乐。通过 plex-themer 可以为媒体库内的任何电影、电视节目、歌手或合集上传本地音频文件作为主题音乐，也可以用于删除已存在的主题音乐。

使用 Plex Series 代理刮削电视节目时，Plex 会为你的电视节目搜索主题音乐，如果在数据库中找到了，就会自动将其下载至本地，并在你浏览这些电视节目的页面时播放主题音乐（如果你启用了播放主题音乐），这是一个很有意思的功能。但是 Plex 使用的数据库覆盖范围有限，还是有很多电视节目无法匹配到主题音乐，虽然 Plex 提供了[使用本地主题音乐](https://support.plex.tv/articles/200220717-local-media-assets-tv-shows/)的方法，也支持用户[提交主题音乐文件进行投稿](https://support.plex.tv/articles/201572843-tv-theme-music-submissions/)，但操作起来还是有些麻烦。

好在 Plex 有一个很棒的第三方插件：[Themerr-plex](https://github.com/LizardByte/Themerr-plex)。Themerr-plex 会通过 [ThemerrDB](https://github.com/LizardByte/ThemerrDB) 获取电影、电视节目和合集的主题音乐，并将其添加到 Plex 媒体库对应项目的元数据中，而且还提供了一个 WebUI 用来管理主题音乐，如果有项目缺少主题音乐，你可以直接通过 WebUI 的添加按钮向 ThemerrDB 提交主题音乐进行投稿，不过 ThemerrDB 目前仅支持提交 YouTube 的主题音乐视频链接进行投稿，并且需要人工审核，待审核通过后 Themerr-plex 才会在之后的任务中将你投稿的主题音乐下载到本地，由于 Themerr-plex 是直接从 YouTube 下载主题音乐的，对部分地区的用户来说还是有些不便。

无论是 Plex Series 还是 Themerr-plex，都仅支持为存在于 TMDB（部分支持 IMDb）上的项目添加主题音乐，并且都需要使用指定的代理进行刮削。而通过 plex-themer，你可以为任何电影、电视节目、歌手或合集添加主题音乐，包括无法匹配的项目（比如自定义合集），并且无需任何审核，运行脚本后立刻就可以在 Plex 内播放主题音乐，它对资料库所使用的代理也没有任何限制，这样，你就可以无拘无束的为任意项目添加主题音乐啦。

## 示例
将音频文件按照要求命名，并放入指定的文件夹，然后运行 `plex-theme-uploader.py` 即可自动上传对应项目的主题音乐，例如：
```
已成功连接到服务器：x1ao4

已成功为 "云电影" 中的电影 "花木兰 (2020)" 上传主题音乐
已成功为 "电影" 中的电影 "花木兰 (2020)" 上传主题音乐
已成功为 "电影" 中的合集 "漫威（系列）" 上传主题音乐
已成功为 "电视剧" 中的合集 "漫威（系列）" 上传主题音乐
已成功为 "电视剧" 中的合集 "爱奇艺" 上传主题音乐
已成功为 "综艺" 中的合集 "爱奇艺" 上传主题音乐

1. "电影" 中的电影：霹雳娇娃 (2000)
2. "电影" 中的电影：霹雳娇娃 (2019)

请选择要添加主题音乐的项目（多个项目用分号隔开）：2

已成功为 "电影" 中的电影 "霹雳娇娃 (2019)" 上传主题音乐
已成功为 "电影" 中的电影 "功夫熊猫 (2008)" 上传主题音乐
```
运行 `plex-theme-deleter.py` 脚本，输入要删除主题音乐的项目名称，即可删除对应项目的主题音乐，例如：
```
已成功连接到服务器：x1ao4

请输入要删除主题音乐的项目名称（多个名称用分号隔开）：花木兰 (2020)；漫威（系列）；爱奇艺；霹雳娇娃；功夫熊猫

已成功删除 "云电影" 中的电影 "花木兰 (2020)" 的主题音乐
已成功删除 "电影" 中的电影 "花木兰 (2020)" 的主题音乐
已成功删除 "电影" 中的合集 "漫威（系列）" 的主题音乐
已成功删除 "电视剧" 中的合集 "漫威（系列）" 的主题音乐
已成功删除 "电视剧" 中的合集 "爱奇艺" 的主题音乐
已成功删除 "综艺" 中的合集 "爱奇艺" 的主题音乐

1. "电影" 中的电影：霹雳娇娃 (2000)
2. "电影" 中的电影：霹雳娇娃 (2019)

请选择要删除主题音乐的项目（多个项目用分号隔开）：2

已成功删除 "电影" 中的电影 "霹雳娇娃 (2019)" 的主题音乐
已成功删除 "电影" 中的电影 "功夫熊猫 (2008)" 的主题音乐
```

## 运行条件
- 安装了 Python 3.0 或更高版本。
- 安装了必要的第三方库：plexapi。（可以通过 `pip3 install plexapi` 安装）

## 配置文件
在运行脚本前，请先打开配置文件 `config.ini`，参照以下提示（示例）进行配置。
```
[server]
# Plex 服务器的地址，格式为 http://服务器 IP 地址:32400 或 http(s)://域名:端口号
address = http://127.0.0.1:32400
# Plex 服务器的 token，用于身份验证
token = xxxxxxxxxxxxxxxxxxxx
# Plex 元数据的基础目录，用于定位主题音乐的元数据文件
metadata_base_directory = /path/to/Plex Media Server/Metadata/
# 语言设置，'zh' 代表中文，'en' 代表英文
language = zh

[search]
# 是否搜索电影，true 代表搜索，false 代表不搜索
movie = true
# 是否搜索电视节目，true 代表搜索，false 代表不搜索
show = true
# 是否搜索歌手，true 代表搜索，false 代表不搜索
artist = true
# 是否搜索合集，true 代表搜索，false 代表不搜索
collection = true

[mode]
# 上传主题音乐后是否删除原文件，true 代表删除，false 代表上传后将文件移动至 themes 文件夹
delete_after_upload = false
# 是否在删除主题音乐时删除用户上传的主题音乐（包括所有非 Plex 提供的主题音乐），true 代表删除，false 代表不删除
user_theme = true
# 是否在删除主题音乐时删除 Plex 提供的主题音乐，true 代表删除，false 代表不删除
plex_theme = false
```

## 使用方法
### plex-theme-uploader
1. 将仓库克隆或下载到计算机上的一个目录中。
2. 修改 `uploader.command (Mac)` 或 `uploader.bat (Win)` 中的路径，以指向你保存的 `plex-theme-uploader.py` 脚本。
3. 打开 `config.ini`，填写你的 Plex 服务器地址（`address`）和 [X-Plex-Token](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/)（`token`），按照需要设置其他配置选项。
4. 将主题音乐文件按照其对应项目在 Plex 媒体库中的名称命名，并移动至 `uploads` 文件夹内。
5. 双击运行 `uploader.command` 或 `uploader.bat` 脚本以执行 `plex-theme-uploader.py` 脚本。
6. 脚本将自动读取 `uploads` 文件夹内的所有文件，并尝试将这些文件作为主题音乐上传到 Plex 服务器上对应的项目中。你可以在控制台查看处理进度，若同一个文件在媒体库内匹配到了多个不同年份的项目，将会需要你在控制台手动选择需要添加主题音乐的项目，脚本会根据选择上传主题音乐，并继续处理其余文件，待所有文件都处理完毕后，脚本会自动结束运行。

### plex-theme-deleter
1. 将仓库克隆或下载到计算机上的一个目录中。
2. 修改 `deleter.command (Mac)` 或 `deleter.bat (Win)` 中的路径，以指向你保存的 `plex-theme-deleter.py` 脚本。
3. 打开 `config.ini`，填写你的 Plex 服务器地址（`address`）、[X-Plex-Token](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/)（`token`）和 Plex 服务器的元数据文件夹目录（`metadata_base_directory`），按照需要设置其他配置选项。
4. 双击运行 `deleter.command` 或 `deleter.bat` 脚本以执行 `plex-theme-deleter.py` 脚本。
5. 输入要删除主题音乐的项目名称（若有多个项目的主题音乐需要删除，请用分号隔开多个名称），按回车。
6. 脚本将尝试定位 Plex 服务器上对应项目的主题音乐元数据文件的存储位置，并删除该文件所在的文件夹。你可以在控制台查看处理进度，若同一个项目名称在媒体库内匹配到了多个不同年份的项目，将会需要你在控制台手动选择需要删除主题音乐的项目，脚本会根据选择删除主题音乐，并继续处理其余项目名称，待所有项目名称都处理完毕后，脚本会自动结束运行。
