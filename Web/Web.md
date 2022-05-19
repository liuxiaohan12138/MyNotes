---

title: Web笔记
---

# Node命令

1.下载依赖

```
npm install
```

2.运行

```
npm run dev
```

3.打包

```
npm run build
```



# electron

1.偷来electron的官方例子

```
git clone https://github.com/electron/electron-quick-start
```

2.将项目打包，dist文件夹复制到之前的electron项目中

```
npm run build
```

3.删除electron项目中的index.html

4.修改main.js

```
mainWindow.loadFile('index.html')
```

5.执行命令预览效果

```
npm install
npm run start
```

6.下载打包依赖

```
npm install electron-packager
```

如果报错

npm ERR! code 1
npm ERR! path F:\electron\electron-quick-start\node_modules\electron
npm ERR! command failed
npm ERR! command C:\Windows\system32\cmd.exe /d /s /c node install.js
npm ERR! RequestError: read ECONNRESET

设置一下本地的python环境变量

```
npm config set python 3.9.6
```

7.修改package.json的打包命令

```
"scripts": { 
"start": "electron .", 
"packager": "electron-packager ./ App --platform=win32 --arch=x64 --overwrite"
} 
```

8.打包

```
npm run packager
```

