---
title: "How to batch edit title case into sentence case for multiple items in Zotero"
date: 2024-06-13 15:45:50
author: Yongkang Yang
categories:
  - Software
---

Zotero users might use APA 7<sup>th</sup> for their reference. There is a problem when the metadata in Zotero is title case, it is laborious to change it every time to sentence case. I found a java script that can take care of all items at once.

<!--more--> 

**Usage:** 

1. copy the code below
2. Zotero-Tools-Developer-Run JavaScript

```javascript
zoteroPane = Zotero.getActiveZoteroPane();
items = zoteroPane.getSelectedItems();
var result = "";
for (item of items) {
var title = item.getField('title');
result += " " + title + "\n";
var new_title = title.replace(/\b([A-Z][a-z0-9]+|A)\b/g, function (x) { return x.toLowerCase(); });
new_title = new_title.replace(/(^|\?\s*)[a-z]/, function (x) { return x.toUpperCase(); });
result += "-> " + new_title + "\n\n";
// // Do it at your own risk
 item.setField('title', new_title);
 await item.saveTx();
}
return result;
```

<span style="color:#FF0000;">The only issue is that it can't uppercase the first letter after the ":"</span> there is still minimum work to be done, but I am not an expert in Java so if you find a better way, just let me know. 

**If you want all title case, you can try another script below:** 

```javascript
var items = ZoteroPane.getSelectedItems();
var n = 0;
for (item of items) {
            var title = item.getField('title');
            new_title = titleCase(title). // convert to title case
                            replace('And', 'and'). // replace 'And'
                            replace('For', 'for'). // replace 'For'
                            replace('In', 'in'). // replace 'In'
                            replace('Of', 'of'). // replace 'Of'
                            replace('With', 'with').
                            replace('Usa', 'USA').
                            replace('Dna', 'DNA').
                            replace('Pcr', 'PCR').
                            replace('Ros', 'ROS').
                            replace('To', 'to')
                            
                            
                            
            item.setField('title', new_title);
            await item.saveTx();
            n ++
};

return n + '个条目的题目大小写转为词首字母大写，有些特殊缩写单词可能转换错误，请查实。';

// 将单词转为首字母大写
function titleCase(str) {   
     var newStr = str.split(" ");    
     for(var i = 0; i < newStr.length; i++) {
        newStr[i] = newStr[i].slice(0,1).toUpperCase() + newStr[i].slice(1).toLowerCase();
        }      
     return newStr.join(" ");
};
```

Note: 

Before run the script, make sure the metadata (year, author name, doi, etc.) are right. 



**Reference:**

Find other useful scripts in Zotero, click: [zotero-javascripts](https://github.com/redleafnew/zotero-javascripts)