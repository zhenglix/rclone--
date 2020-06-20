# rclone--
Rclone-魔改版
官方版rclone不支持挂载世纪互联版本的OneDrive，大佬们修改并编译了支持世纪互联版本的rclone。

挂载
地址：https://portal.azure.cn/，登录完成后按下面步骤进行
左侧Azure Active Directory---应用注册---新注册

名称：自己填写---受支持的账户类型：任何组织目录(任何 Azure AD 目录 - 多租户)中的帐户
---重定向 URI (可选)：http://localhost:53682---注册

应用程序(客户端) ID（**复制保存下来，即后面的client_id**）---左侧证书和密码---
右侧客户端密码部分：+新客户端密码

说明：自己填写---截止日期：2年内---添加

客户端密码部分：值（**复制保存下来，即后面的client_secret**）---左侧API权限---
添加权限---Microsoft Graph---委托的权限--- 搜索并勾选下面6个权限：
    Files.Read
    Files.Read.All
    Files.ReadWrite
    Files.ReadWrite.All
    offline_access
    User.Read
    
到此azure应用就注册完毕了，点击左侧Azure Active Directory—应用注册，可以看到你拥有的应用程序，记住之前应用程序(客户端) ID和客户端密码部分：值

3.挂载世纪互联版onedrive
在这里写下在远端linux主机上如何挂载。

Windows命令行进入rclone所在文件夹，执行命令：

 rclone authorize onedrive "应用程序(客户端) ID" "客户端密码值" --onedrive-is-21vianet-version=true

之后会跳转到浏览器，登录账号之后返回Windows命令行，会返回token，复制保存下来，后面要用。

需要复制的token格式类似于:

{"access_token":"exxxxxxxxxxxxDlkYzQvIiwiaWF0IjoxNTgwOTY5OTA5LCJuYmYiOjE1ODA5Njk5MDksImV4cCI6MTU4MDk3MzgwOSwiYWNjdCI6MCwiYWNyIjoiMSIsImFpbyI6IkFTUUEyLzhPQUFBQVhhOXZUUGdSa3hKOxxxxxxxxxxxxxxxxxxxqaUxxU2RNdjkwbVFPb1p1ejBVZTA9IiwiYW1yIjpbInB3ZCJdLCJhcHBfZGlzcGxheW5hbWUiOiJyY2xvbmUiLCJhcHBpZCI6ImIxNTY2NWQ5LWVkYTYtNDA5Mi04NTM5LTBlZWMzNzZhZmQ1OSIsImFwcGlkYWNyIjoixxxxxxxxxxxxxxxxxxIm9pZCI6IjdmM2RiYjJlLTZkNGQtNDI2MC1hOTI1LTE2MmViNzNhZDA3MiIsxxxxxxxxxxxxxxmIjoiMyIsInB1aWQiOiIxMDAzMjAwMDk0RjVGMjI3Iiwic2NwIjoiRmlsZXMuUmVhZCBGaWxlcy5SZWFkLkFsbCBGaWxlcy5SZWFkV3JpdGUgRmlsZXMuUmVhZFdyaXRlLkFsbCBwcm9maWxlIG9wZW5pZCBlbWFpbCIsInN1YiI6ImVLR0pUZjZEaTRJSnM3Z0I0SEpwOGpOa1JTV1FPQnR2VnVYbxxxxxxxxxxxxxxxxxxxxxxHl6IiwidXRpIjoic2IyMkxULVVKVW03cmh6S2NDd29BQSIsInZlciI6IjEuMCIsIndpZHMiOlsiNjJlOTAzOTQtNjlmNS00MjM3LTkxOTAtMDEyMTc3MTQ1ZTEwIl0sInhtc19zdCI6eyJzdWIiOiI4VzRJMk1EcUVoZVlsNDVBNng5RV9wNHNDWVZ5N1hsYnpNVksyYVYyZWpRIn0sInhtc190Y2R0IjoxNTc4ODI3NzQ1fQ.gJ1dJS-k3BnOGV0mh4Nwvm4bXGrW4HbNzkjeO1QXFsyxx06_ryuftftuL7oHJaDhWeNFc1sm0wqVVCu1VOCzbslgCrEKIxiExBBstQJruOEscSq7LKCrQQEMbVEgFcKdxZtfzR6U24tb6Bu2VXAL1fq3gEEud3-8Up-hjQe14M1XsN1F-sYgOOkTgNcJCytx_32o3OzONugxCvmCzK6KCmzpuUUYJhPfbubg48AaIjkvVbAhxl-1KnLnocass9Cfbvydlgs4gkVraAhYKEzoxl_meDsJWFtY9iz1ajrRU0l0MzpgUhWT0HgI_cBijmRgwe-mp2oa2h5TFS0UoBOCWQ","token_type":"Bearer","refresh_token":"OAQxxxxxxxxxxxxxxxxxxxxxxxxxxxzOzGoEEJh-Kcl7ktxI56rsY2QB5xKAhZYLfai-Al1CFzyxjdCXlwf5BUTPydTpXnSSoDDOVvs9mn8F8B-otfGJ7U5LJ5xqiRA3NPH5jL1XgGmzMN1CjnJvyPuEOOnS1dSkZu5i8KhgCdEfY8AXLmuq1JLDkAxmJVx_RmXmKidCf_6F9hXRQIelnFnR0X4addzah5Zxb0rrqdQVwNUdltTCsSZBdxo-NXjVbWxxxxxxxxxxxxxxxxxxxxxxxxxIsdC3qBpPBMx30gOMc_us2NVmOr9ybHsS8B-ZUMcVWaLhPtBW9baBKmcYF43-RKJqppZVQmyMaIo2sne72h8k4uUzJdWLPBx8AUlQSrrQaAH_mXMcQ4RG7qKIvfT0oAmrZcf2Fjp_GUPP-02uCd_z-NVZ_yne66jYVgTjqHZq3nuQ2KeTSrPOW9qNKMaCXtCnYj4Fmvr6BkbXR9qvd2SYexDEz7T9bT6T4CbTtBOXF8AY6E52bLkLJHViO3gkqVFtphRFwxaj59rBz466PVDooWxN423iiVhPQAYOQlZujea_R-tWmKjME8-4RVKaSZY0cW2ojaMRMT00RcWCCJ7PBedPYoVDDZ8Bn6W4VT8Phma0yS-cvy3EIjfI-p3Ojy4mLruaWagFlTfgqgq1it8whfpu6xPys1NGYBHm9fW6E4bU8YtzGXxzKmJ62INvYizoNbEfxBtjMx8etuze2qj5EJkPTfsbgzD6IbB_fQDxaYPGFM_3_zHOwkPUirkigWjWnpdNzqdRbiYxO06FsYkgAA","expiry":"2020-02-06T15:23:28.6393091+08:00"}

然后连接ssh
接下来将linux版的解压上传到usr/bin目录(必须此目录)，然后给权限chmod +x /usr/bin/rclone
执行rclone config，就进入了和官方版rclone一样的挂载程序，和国际版onedrive不同的是：client_id填写应用程序(客户端) ID，client_secret填写客户端密码。is_21vianet_version填true，Edit advanced config以及Use auto config都选no，下一步粘贴上之前在Windows获取的token，继续按提示完成之后的步骤。

上面绑定了账号之后将网盘挂载到linux主机。先安装fuse命令：
yum install fuse
创建挂载文件夹：
mkdir -p /mnt/od(替换自己的目录)
挂载：
rclone mount od(在绑定账号时起的名字): /mnt/od（挂载目录） --allow-other --allow-non-empty --vfs-cache- 
mode writes&
这样就挂载成功了，可以输入df -h查看。
重启主机挂载就会失效，网上也有添加自动挂载的教程。

卸载命令：
fusermount -qzu LocalFolder onedrive（创建时的Name）

Rclone 开机启动（请下载rcloned文件）

