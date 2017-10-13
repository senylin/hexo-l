---
title: Angularjs2.x学习分解2(基础篇)
date: 2017-08-10 17:17:47
tags:
- javascript
- angularjs

---
angular2 基础知识解疑 http，pipe，ngmodel问题
<!--more-->
### angularjs2 http
ng2 http
http://www.cnblogs.com/SLchuck/p/5930740.html
angular2 学习笔记 ( Http 请求)http://www.cnblogs.com/keatkeat/p/5814708.html
```
import { Injectable,Inject } from '@angular/core';
import { Http,Headers } from '@angular/http';
import { InterceptorService  } from 'ng2-interceptors';
import { Observable } from "rxjs/Observable";
import 'rxjs/Rx';
import 'rxjs/add/operator/toPromise';

search(){
    return this.http....toPromise().then()
}
search().then()
///
search(){
    return this.http....map()
}
search().subscribe()
```


### angularjs2 pipe 
https://segmentfault.com/a/1190000008646187

### *ngFor *ngIf 不能在同一个元素下

用`<ng-container></ng-container>`隔开

### angular1 $watch in angularjs2

用ngModelchange($event) / set||get / ngOnchanges() 三种代替

### angularjs2 ngModel
```
ngModelchange($event)
```
监听ngModel改变事件

### zone.js学习记录

就是angular2用的脏检查机制


