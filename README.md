# Summarize_People
Use 「History of City of Taipei」 as laguage material, summarize the lives of people recorded in it. 
  
# Prerequisite
jieba:  
`pip install jieaba`
  
ckip(中研院)  
1. 到官網申請線上服務(中研院斷詞沒有線下服務)
http://ckipsvr.iis.sinica.edu.tw/webservice.htm → 申請服務帳號 → 按此申請 → 到信箱啟動帳號 → 等待一段時間開通帳號  
2. 修改此目錄底下`config.ini.example`，將申請的帳號密碼寫入，並改名成`config.ini`  

# Usage
先試試看 `python main.py --most 5 --set-up`  
之後就不需要再加上`--set-up`了， 不需要重複轉檔和斷詞  
  
用 `python main.py -h`發現其他option  
在`main.py` 最底下也有兩個使用例  
  
Note: 另兩個py檔也有command line 的使用介面， 在檔案的最下面有該檔案的使用範例
  
# Regular Expression in SplitAndExtract
`^(\w　?\w+) ?\.+ (\d\d\d)$`:  
^ : 這裡是行首  
\w　?\w+ ： (人名) 一個文字，後面可能會接一個全形符號(二字人名時),再接數個文字  
 ？ ：有可能有空白有可能沒有 (四字人名後面沒有空格)  
\.+ ：一個以上的.  
\d\d\d : 三個數字(頁數)  
$ ：這裡是行尾  
() : 括號裏面的pattern 所match到的東西形成一個group  
  
re.findall 會回傳list of tuples
每個tuple 代表一個對pattern的match 裡的groups, i.e. tuple為 (group1, group2, ...)  
第3個argument是flags, re.MULTILINE 是把認清字串是多行的，才能在pattern裡用 ^ 和 $