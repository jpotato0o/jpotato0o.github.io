---
layout:            post
title:             "IE-Compatible"
date:              2016-12-20 16:31:00 +0300
tags:              IE, Compatible  
category:          IE
author:            sjiang
---

#### 1.Use-Agent

浏览器模式决定了 Internet Explorer 发出请求时自带的 User-Agent，也决定了在默认情况下 Internet Explorer 使用哪一种文档模式来渲染页面  
通常都会用user-agent中的关键字来判断浏览器版本类型，如下:
  
```
	public static String responseFileName(String fileName,String agent){
			try{
			if(null != agent){
				if(-1 != agent.indexOf("MSIE") || -1 != agent.indexOf("Trident") 
						|| -1 != agent.indexOf("Edge")){// ie
					fileName = URLEncoder.encode(fileName,"UTF-8");
				}else if(-1 != agent.indexOf("Mozilla")){// 火狐,chrome等
					fileName = new String(fileName.getBytes("UTF-8"),"ISO8859-1");
				}
			}
			}catch(IOException e){	
			}
			return fileName;
		}
```
或  
```
	// 文件名处理，否则会出现文件名为中文时不能下载
	if (request.getHeader("User-Agent").toLowerCase().indexOf("firefox") > 0) {
		originalName = new String(originalName.getBytes("UTF-8"), "ISO8859-1");// firefox浏览器
	} else{
		if (request.getHeader("User-Agent").toUpperCase().indexOf("MSIE") > 0) 
			originalName = URLEncoder.encode(originalName, "UTF-8");
	}
```  
但程序随着浏览器版本更新会修改当中的字段，并且某些情况可以更改user-agent，所以建议用特性检测 

```bash
---
if（target.addEventListener）
---
```
在实际使用中一般检查最多的是ie浏览器与标准dom浏览器的区别，这样可以使用window.addEventListener来判断这两种类型的浏览器 
```html
	if(typeof window.addEventListener==="function") 
		{ 
	    	alert("DOM浏览器"); 
		} 
		else 
		{ 
	   		alert("IE"); 
		}  
```

#### 2. <!DOCTYPE html>

- Internet Explorer 7, 8, 9 默认模式
Internet Explorer 7, 8, 9 会检测当前页面是否包含 <!DOCTYPE> 声明，如果有那就会用当前 IE 所支持最高的文档模式，如果没有，IE 则会使用 IE5 Quirks 文档模式  
- Internet Explorer 10, 11 默认模式
Internet Explorer 10 和 Internet Explorer 11 不管当前页面是否包含 <!DOCTYPE> 声明，都会使用最高的文档模式，即：IE10 使用 IE0 标准文档模式，IE11 使用 IE11 标准文档模式  

用<meta http-equiv=“X-UA-comptaible” content=“IE=Edge”>来声明文档模式以哪个版本浏览器解析  

使用标准方法:  
1. 为w3c标准化的方法
2. 使用第三方库，框架（jQuery，angularJS,VUE）


#### 3.标准化的CSS、DOM前缀
```html
-ms-transform:rotate(7deg);             //-ms代表ie内核识别码
-moz-transform:rotate(7deg);            //-moz代表火狐内核识别码
-webkit-transform:rotate(7deg);         //-webkit代表谷歌内核识别码
-o-transform:rotate(7deg);              //-o代表欧朋【opera】内核识别码
transform:rotate(7deg);                 //统一标识语句。。。最好这句话也写下去，符合w3c标准
```
使用css3属性时，大部分都要带这些识别前缀，早期点的浏览器才能识别，可以有整合一个js文件的，嵌入你的页面  

工具：autoprefixer  
[http://www.w3cplus.com/css3/autoprefixer-css-vender-prefixes.html](http://www.w3cplus.com/css3/autoprefixer-css-vender-prefixes.html)  

#### 4.创建有效的回退策略fallback
意思是有不支持这种方式的替代方式 
```
data=picture.swg
<img src=“picture.png”>
```

#### 5.文档模式优先级
meta标签 > HTTP返回头  
X-UA-Compatible > 浏览器默认行为模式，兼容模式  


#### 总结：
浏览器兼容方式:  
1. 代码内部兼容【虚拟机测试多IE版本浏览器】
2. 浏览器方面兼容（企业模式（组策略），兼容性视图）【两者不要混用】

- 确定站点支持的最高文档模式
- 确定站点当前是否需要某种指定的User-Agent
- 尽量加X-UA-Compatible来指定文档模式




参考文章：[http://joji.me/zh-cn/blog/ie11-migration-guide-understanding-browser-mode-document-mode-user-agent-and-x-ua-compatible](http://joji.me/zh-cn/blog/ie11-migration-guide-understanding-browser-mode-document-mode-user-agent-and-x-ua-compatible)



