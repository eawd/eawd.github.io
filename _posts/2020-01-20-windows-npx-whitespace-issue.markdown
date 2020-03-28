---
layout: post
title:  "npx issue with directories with whitespace (Windows)"
language: english
date: 2020-01-20 19:27:14 +02:00
categories: windows nodejs
---


I've been trying to use npx on Windows for a while now and everytime I got the following error:

```log
TypeError: Cannot read property 'get' of undefined
    at errorHandler (C:\Users\User Name\scoop\persist\nodejs\bin\node_modules\npx\node_modules\npm\lib\utils\error-handler.js:213:18)
    at C:\Users\User Name\scoop\persist\nodejs\bin\node_modules\npx\node_modules\npm\bin\npm-cli.js:83:20            
    at cb (C:\Users\User Name\scoop\persist\nodejs\bin\node_modules\npx\node_modules\npm\lib\npm.js:215:22)
    at C:\Users\User Name\scoop\persist\nodejs\bin\node_modules\npx\node_modules\npm\lib\npm.js:253:24
    at C:\Users\User Name\scoop\persist\nodejs\bin\node_modules\npx\node_modules\npm\lib\config\core.js:81:7         
    at Array.forEach (<anonymous>)
    at C:\Users\User Name\scoop\persist\nodejs\bin\node_modules\npx\node_modules\npm\lib\config\core.js:80:13        
    at f (C:\Users\User Name\scoop\persist\nodejs\bin\node_modules\npx\node_modules\npm\node_modules\once\once.js:25:25)
    at afterExtras (C:\Users\User Name\scoop\persist\nodejs\bin\node_modules\npx\node_modules\npm\lib\config\core.js:178:20)
    at C:\Users\User Name\scoop\persist\nodejs\bin\node_modules\npx\node_modules\npm\node_modules\mkdirp\index.js:47:53
C:\Users\User Name\scoop\persist\nodejs\bin\node_modules\npx\node_modules\npm\lib\utils\error-handler.js:213
if (npm.config.get('json')) {
                 ^

TypeError: Cannot read property 'get' of undefined
    at process.errorHandler (C:\Users\User Name\scoop\persist\nodejs\bin\node_modules\npx\node_modules\npm\lib\utils\error-handler.js:213:18)
    at process.emit (events.js:210:5)
    at process._fatalException (internal/process/execution.js:150:25)
Install for [ 'package@latest' ] failed with code 7
```

Or some other variation of it, I think the error was that my User's `$HOME` directory contained whitespace so to fixed it I had to set the `cache` and `prefix` keys in npm config, here's how it can be fixed.

First, if you don't already know where the npm `cache` and `prefix` directories are you can retrieve them using

```bash
npm config list -l
```

The output should look like the following:

![Command Output]({{site.baseurl}}/assets/img/posts/npx/1.png)

Find the following keys: `cache`, `prefix` and `userconfig`, `userconfig` should be your `.npmrc` file edit or create it using your favorite editor and add the `cache` and `prefix` to it, replacing your username directory with the short version for me that would be `USERNA~1`.

To get the short name you can use this powershell command (replace `$home` with the directories you get).

```powershell
(New-Object -ComObject Scripting.FileSystemObject).GetFolder("$home").ShortPath
```

If this doesn't work try the other methods [in this question](https://superuser.com/questions/348079/how-can-i-find-the-short-path-of-a-windows-directory-file).

Then add them to your `.npmrc` file, the final result should look something like:

```ini
cache = "C:\\Users\\USERNA~1\\scoop\\persist\\nodejs\\cache"
prefix = "C:\\Users\\USERNA~1\\scoop\\persist\\nodejs\\bin"
```

That's all FOLKS~1