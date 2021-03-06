# npm

## 添加用户
```bash
# registry 是指定源，有时候把源更好成了淘宝的镜像
$ npm adduser --registry http://registry.npmjs.org
# 命令执行后，会依次出现以下填写项
Username: work_lib_tlz
Password:
Email: (this IS public) work_lib_tlz@126.com
Logged in as work_lib_tlz on http://registry.npmjs.org/.
```

## node-gyp.js error MSB6006: “VCBuild.exe”
在安装`stompjs`的时候下载websocket模块报错
```bash
e:\IdeaProjects\net.tidebuy.sched\sched-vue\node_modules\websocket>if not defined npm_config_node_gyp (node "e:\node\node_global\node_modules\npm\bi
node-gyp-bin\\..\..\node_modules\node-gyp\bin\node-gyp.js" rebuild )  else (node "" rebuild )
Building the projects in this solution one at a time. To enable parallel build, please add the "/m" switch.
  错误: 项目文件“e:\IdeaProjects\net.tidebuy.sched\sched-vue\node_modules\websocket\build\bufferutil.vcproj”找不到或者不是有效的项目文件。
  该项目的所有配置项都需要系统提供对某些平台的支持，但在此计算机上没有安装这些平台。因此无法加载该项目。
MSBUILD : error MSB6006: “VCBuild.exe”已退出，代码为 -1。 [e:\IdeaProjects\net.tidebuy.sched\sched-vue\node_modules\websocket\build\binding.sln]
  错误: 项目文件“e:\IdeaProjects\net.tidebuy.sched\sched-vue\node_modules\websocket\build\validation.vcproj”找不到或者不是有效的项目文件。
  该项目的所有配置项都需要系统提供对某些平台的支持，但在此计算机上没有安装这些平台。因此无法加载该项目。
MSBUILD : error MSB6006: “VCBuild.exe”已退出，代码为 -1。 [e:\IdeaProjects\net.tidebuy.sched\sched-vue\node_modules\websocket\build\binding.sln]
```

原因是 node-gyp 需要调用相关的库，[官网中有依赖说明](https://github.com/nodejs/node-gyp)

在windows中安装[windows-build-tools](https://github.com/felixrieseberg/windows-build-tools)
```bash
npm install --global --production windows-build-tools
```
安装的时候卡在下面很久,在[issues/307](https://github.com/nodejs/node-gyp/issues/307)中说道，可能要等待一个小时左右。而我自己等了快两个小时，最好开始的时候 加上 `--debug` 查看一部分日志
```bash
> windows-build-tools@1.3.2 postinstall e:\node\node_global\node_modules\windows-build-tools
> node ./lib/index.js

Downloading BuildTools_Full.exe
Downloading python-2.7.13.msi
[>                                            ] 0.0% (0 B/s)
Downloaded python-2.7.13.msi. Saved to C:\Users\Administrator\.windows-build-tools\python-2.7.13.msi.
Starting installation...
Launched installers, now waiting for them to finish.
This will likely take some time - please be patient!
Waiting for installers... |Successfully installed Python 2.7
Waiting for installers... -
```


## `.npmrc`
```bash
# 在npm install过程中打印当前的请求下载日志
loglevel=http
```

## npm install 与 lock
[Yarn vs npm: 你需要知道的一切](http://web.jobbole.com/88459/)

在install的时候由于绝大部分js库依赖的版本号都是动态的，小版本号最新，就会造成在每台机器上install的版本不一致的问题。
