
<div align="center">
	<div>
		<img width="200" src=".pic/vks-200.png" alt="Awesome Node.js" style="position: relative; float: left; width: 200px; margin-right: 40px; margin-bottom: 90px; margin-top: 13px;">
	</div>
	<br>

# VKS v 1.1.9 ![Python:3.7](https://img.shields.io/badge/Python-3.7-yellow) [![stability-unstable](https://img.shields.io/badge/stability-unstable-yellow.svg)](https://github.com/emersion/stability-badges#unstable) [![License:MIT](https://img.shields.io/badge/license-MIT-green)](https://img.shields.io/github/license/V1A0/VkScrapper)
Program for monitor <b>your own</b> online activity on [vk.com]
</div>



<div>

<div style="padding-left: 240px; font-size: 18px; line-height: 25px">

### Features:
- [x] 📈 Recording online activity
- [x] 📊 Live time visualizing data as HTML (ready for web)
- [x] 📑 Scrapping profile info
- [x] 🎯 Multiple targets support
- [x] 🌐 Proxy support
- [x] 🕵🏼 Secure mode
	- [x] 🔀 Random proxy
	- [x] 🎲 Random headers

> Coming soon
> - [ ] 🎱 Predicting activity
> - [ ] ❌ Get new proxy if previous failed
> - [ ] 👪 Multiple accounts support

</div>

## Update 1.1.9 - What's new?
 - Security UPD
 - Random proxy module
 - Random headers module
 - Speed up x3!
 - For scrapes now use only lxml
 - Some files moving
 - Less third-party modules

> Thanks [@jundymek](https://github.com/jundymek) for [free-proxy](https://github.com/jundymek/free-proxy) and [@skratchdot](https://github.com/skratchdot) for [random-useragent](https://github.com/skratchdot/random-useragent).

</div>



## 1. Libraries Installation

Use the package manager [pip] to install necessary for script modules.

```bash
pip install sqlite3
pip install lxml
pip install Pillow
pip install requests
```
OR add parameter `"1"` for key `install` into file `config.json`
```json
...
"install" : "1",
```



## 2. How to use
#### 2.1. First way - UI
For run use python 3.7+:
```bash
py vks.py
```
After that, enter id of your page on vk.com:
```bash
Enter user id: 10000451
```
Login (optional):
```bash
Are you sure you want to continue without authorisation?
(y/n) : n
Enter login: +79998887766
Enter password: [not displayed]
```
You don't have to login, but user page may be hidden from anonymous visits by privacy settings.<br/>
Script use login data only once, to create a web-session. After that password is erasing and will never be appear in memory.<br/>
If tracking session started successfully you'll get message like that in your terminal:
```bash
VKS v1.1.9 | vk.com opensource stalkerware
Running...

Tracking is started successfully
User: Guy Montag
Status:
05-01-1984 13:37:42  :  Offline
05-01-1984 13:38:42  :  Offline
05-01-1984 13:39:42  :  Online
05-01-1984 13:40:42  :  Online
```
---

#### 2.2. Second way - Advanced
##### 2.2.1 Open `config.json` and add some arguments into it: Target id (might be a few), login and password (optional), proxy settings (optional).
Example:

```json
{
	"id" : ["10000451", "19668908"],    	# Targets id
	"login" : "79998887766",		# Login data
	"password" : "mypaswd1234",		# Login data
	"proxy" : {},				# Custom proxy settings
	"sleep_time" : 60,			# Don't change it!
	"install" : "",				# Install requires
	"autoconvert": "True",  		# Auto converting data to HTML
	"debug" : "",				# Debug mod
	"rand_proxy" : "True",			# Get randome proxy from sslproxies.org (Secure setting)
	"rand_header" : "True",			# Set random header for login request (Secure setting)
}
```

##### 2.2.2. After this save file and run the program use python:
```bash
py vks.py
```

Script use login data only once, to create a session. After that password is erasing from program's memory. Also you can delete it from
`config.json` or enter it just use UI (p 2.1 - First way - UI). For this just leave empty "password" parameter. <br/>
If tracking session started successfully you'll get message in your terminal like this:
```bash
VKS v1.1.9 | vk.com opensource stalkerware
Running...

Tracking is started successfully
User: Guy Montag
Tracking is started successfully
User: Satoshi Nakamoto

Status:
05-01-1984 13:37:42  :  Offline (Guy Montag)
05-01-1984 13:37:43  :  Online (Satoshi Nakamoto)
05-01-1984 13:38:42  :  Online (Guy Montag)
05-01-1984 13:38:43  :  Offline (Satoshi Nakamoto)
05-01-1984 13:39:42  :  Online (Guy Montag)
05-01-1984 13:39:43  :  Offline (Satoshi Nakamoto)
```
Don't close the terminal until you didn't get enough data to analise.

---
If you have only one target your terminal will be looks like this
```bush
VKS v1.1.9 | vk.com opensource stalkerware
Running...

Tracking is started successfully
User: Guy Montag
Status:
05-01-1984 13:37:42  :  Offline (Guy Montag)
05-01-1984 13:38:42  :  Offline (Guy Montag)
05-01-1984 13:39:42  :  Online (Guy Montag)
05-01-1984 13:40:42  :  Online (Guy Montag)
```
#### 2.3 Secure settings

Into `config.json` you can find some kind of options like that

```json
{
	"proxy" : {},				# Custom proxy settings
	"rand_proxy" : "True",			# Get randome proxy from sslproxies.org
	"rand_header" : "True",			# Set random header for login request
}
```

##### 2.3.1 Random proxy
VKS have inline module to get free proxy from sslproxies.org: `getproxy.py`
It's based on ["free-proxy" by jundymek](https://github.com/jundymek/free-proxy). This script just scrapes proxies from https://www.sslproxies.org/ and checks it.

> ⚠️ This function is not stable at this moment, be careful, connection might fail at any time! ⚠️

🟢 To enable this setting, set
```
"rand_proxy" : "True",
```
🔴 To disable
```
"rand_proxy" : "",
```

##### 2.3.1 Random header
VKS have inline module to set random header for authorize request:
List of User-Agents based on [useragent-data.json](https://github.com/skratchdot/random-useragent/blob/master/useragent-data.json) from ["random-useragent" by skratchdot](https://github.com/skratchdot/random-useragent).

🟢 To enable this setting, set
```
"rand_header" : "True",
```
🔴 To disable
```
"rand_header" : "",
```


#### 2.4 Errors and how to fix ⚠

##### 2.4.1 Status error

If user hiding his page from anonymous visits, you'll see messages like this:
```bash
VKS v1.1.9 | vk.com opensource stalkerware
Running...

Tracking is started successfully
User: Guy Montag
Status:
05-01-1984 13:37:42  :  ERROR (Guy Montag)
05-01-1984 13:38:42  :  ERROR (Guy Montag)
05-01-1984 13:39:42  :  ERROR (Guy Montag)
05-01-1984 13:40:42  :  ERROR (Guy Montag)
```
Name displaying, but activity status is 'ERROR'.<br/>
To fix it authorise as 'real' user or friend of target.

##### 2.4.2 Any other errors

Read information about error into data\log\log_vks.txt
Try to fix it by yourself or [send bug report](https://github.com/V1A0/VKS/issues/new/choose)

### 3. Visualizing statistic
If html files was not created automatically into main dir of script. Open main path and run script ``` converter.py ```:
```bash
py converter.py
```
If process successfully started you'll se messages like this:
```bash
Visualising data to graphics...

T01_12_1984  DONE
T02_12_1984  DONE
T03_12_1984  DONE
    ( . . . )

Analysing data...

user_10000451.db
T01_12_1984  DONE
T02_12_1984  DONE
T03_12_1984  DONE
    ( . . . )

Combining all parts to html...

user_10000451.html  DONE

All data successfully converted to HTML
```
After that you can find some html files into main script's directory. Format of file name it 'user_%id%.html'.<br>
Open it by any browser and enjoy.

<b> Example of html file (screenshot): </b>

 <img src="https://raw.githubusercontent.com/V1A0/VKS/master/.pic/example.png"
     alt="example-screenshot"
     style="float: left;" />

# Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License
[MIT](https://choosealicense.com/licenses/mit/)


## OLD UPDs

## Update 1.1.8 - What's new?
 - Absolutely NEW frontend
 - Full collection of profile information

### Update 1.1.7
1. Quick conversion (picture and statistic is not creating again if it's already exist).
2. Auto (realtime) converting (ON by default)
3. Vars renaming
4. Code refactoring

### Update 1.1.6
1. HTML front end remastering
2. Code refactoring

### Update 1.1.5
1. Converter upd (bugfix)
2. Better algorithm of finding userinfo
3. HTML and CSS templates upd
4. config.json

### Update 1.1.4
1. Support multiple targets
2. Better error logging
3. Not support inline arguments anymore
4. Code refactoring
5. Bugfix



[vk.com]: (https://vk.com/)
[pip]:(https://pip.pypa.io/en/stable/)
