---
title: Angularjs2.x学习分解3(插件篇)
date: 2017-08-10 17:20:01
tags:
- javascript
- angularjs
---
使用中的angular2插件 tanslate,Interceptors,bootstrap,file-upload,datepicker,组件库等链接
<!--more-->
### angularjs2 translate
ng2国际化翻译
```
import { TranslateModule,TranslateLoader,TranslateStaticLoader } from 'ng2-translate';
```
https://github.com/ngx-translate/core/blob/fb02ca5920aae405048ebab50e09db67d5bf12a2/README.md


### NG2-Interceptors
 api监控 增加token等操作
- https://github.com/voliva/angular2-interceptors

### ng-bootstrap

- 官网 https://ng-bootstrap.github.io/#/components/accordion
- 教程 http://www.jb51.net/article/95008.htm

### angular2 ng2-file-upload上传

http://www.jianshu.com/p/0741186f60ab
http://valor-software.com/ng2-file-upload/

```
 upLoadItem(callback,error) {
    if(this.fileEnum!=null){
      this.uploader.setOptions({url:this.config.baseUrl + 'files?fileEnum=' + this.fileEnum});
    }
    var _is  = this;
    //未选择文件
    if (!this.uploader.queue[0]) {
      callback();
      return;
    }
    //console.log(this.uploader.queue);
    var length = this.uploader.queue.length;
    this.uploader.queue[length-1].onSuccess = (response, status, headers) => {
      // 上传文件成功   
      if (status == 200) {
        // 上传文件后获取服务器返回的数据
        let tempRes = JSON.parse(response);
        this.file = tempRes.responseBody;
        this.fileModel = tempRes.responseBody.fileId;
        callback();
        this.getUploaderSuccess.emit();
      } else {
        // 上传文件后获取服务器返回的数据错误      
        error();
      }

    };
    this.uploader.queue[length-1].onError = (response, status, headers) => {
      // 上传文件成功   
      error();
      _is.csptProcessing.done();
    };
    this.uploader.queue[length-1].upload();

  }
```

### angular2 ng-bootstrap datepicker

依赖于bootstrap4，生产中不可取,替换ng-datetime

ng-datetime ngmodel 绑定数据问题，从后台传入的参数需要转换成new Date()

```
    changeDate(data){
        var strs;
        if(typeof(data)=="string"){
            strs = data.split("-");
            data = new Date(strs[0],strs[1]-1,strs[2]);
        }
        return data
    }
    changeDateTime(data){
        return new Date(data);
    }
```

### angular2 组件库
 
 - https://www.primefaces.org/primeng/#/responsive  PrimeNG
 - 阿里的组件库zorro  

