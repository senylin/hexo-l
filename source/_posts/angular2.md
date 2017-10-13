---
title: Angularjs2.x学习目录
date: 2017-08-10 17:10:07
tags: 
- javascript
- angularjs

---

### 官方文档
- 英文版https://angular.io/docs/js/latest/
- 中文版https://angular.cn/docs/ts/latest/api/

### ng2中文社区

- http://www.angularjs.cn/A2i2

<!--more-->

### angularjs－cli

- Angular2-使用Angular CLI快速搭建工程 http://www.jianshu.com/p/cba3fa12f0a3
- Angular 从0到1 http://www.jianshu.com/p/9af9f203e0b1(有实体书)

### angularjs2 变化与优势

- angularJS 1和2的区别 http://blog.csdn.net/jacoby_fire/article/details/52459215
- Angular2 相比 React 技术栈有什么具体的优势 https://www.zhihu.com/question/57521818/answer/154578682

### angularjs2 学习

- AngularJS2学习 http://www.cnblogs.com/bq-med/p/5253149.html
-  angular2的ngfor ngif指令嵌套 http://blog.csdn.net/pht1991/article/details/72461142
-  Angular2中select用法之设置默认值与事件详解 http://www.jb51.net/article/113139.htm
-  Angular2 组件通信 http://www.cnblogs.com/zzcit/p/6053324.html
-  Angular 2 constructor & ngOnInit   https://segmentfault.com/a/1190000008685752
-  Angular2新人常犯的5个错误 http://www.tuicool.com/articles/qymIRnA
-  TypeScript学习笔记（二）：基本数据类型及数据转换 http://www.cnblogs.com/hammerc/p/4908950.html
-  Angular 4.x 修仙之路 https://segmentfault.com/a/1190000008754631
-  Angular2 表单 http://www.cnblogs.com/SLchuck/p/5839790.html


### angularjs2 translate
ng2国际化翻译
```
import { TranslateModule,TranslateLoader,TranslateStaticLoader } from 'ng2-translate';
```
https://github.com/ngx-translate/core/blob/fb02ca5920aae405048ebab50e09db67d5bf12a2/README.md

### angularjs2 pipe 
https://segmentfault.com/a/1190000008646187

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

### *ngFor *ngIf 不能在同一个元素下

用`<ng-container></ng-container>`隔开

### angular1 $watch in angularjs2

用ngModelchange($event) / set||get / ngOnchanges() 三种代替

### angularjs2 ngModel
```
ngModelchange($event)
```
监听ngModel改变事件

### NG2-Interceptors
 api监控 增加token等操作
- https://github.com/voliva/angular2-interceptors

### ng-bootstrap

- 官网 https://ng-bootstrap.github.io/#/components/accordion
- 教程 http://www.jb51.net/article/95008.htm

### angularjs2 AOT编译器报错

Angular 2.0.2 - Error encountered resolving symbol values statically

https://stackoverflow.com/questions/39989083/angular-2-0-2-error-encountered-resolving-symbol-values-statically

### angularjs2 闭包

this问题

需要写
```
var _this = this
```

### angular2 component重复declaration问题

在上级module引用并exports这个共享的component
```
import { NgModule } from '@angular/core';
import { SharedModule } from '../../../shared/shared.module';
import { Routes,RouterModule } from '@angular/router';
import { IndexRoutingModule } from './index-routing.module';
import { IndexComponent } from './index.component';
import { csptHeaderComponent } from '../../../components/cspt-dynamic/cspt-header/cspt-header.component';
import { csptFooterComponent } from '../../../components/cspt-dynamic/cspt-footer/cspt-footer.component';
import { csptNavComponent } from '../../../components/cspt-dynamic/cspt-nav/cspt-nav.component';
import { csptTableComponent } from '../../../components/cspt-dynamic/cspt-table/cspt-table.component';
import { csptPageNavComponent } from '../../../components/cspt-dynamic/cspt-page-nav/cspt-page-nav.component';
import { csptSelectComponent } from '../../../components/cspt-dynamic/cspt-select/cspt-select.component';
import { csptPaginatorComponent } from '../../../components/cspt-dynamic/cspt-paginator/cspt-paginator.component';
import { HttpModule,Http } from '@angular/http';

@NgModule({
  declarations: [ 
    IndexComponent,
    csptHeaderComponent,
    csptFooterComponent,
    csptNavComponent,
    csptTableComponent,
    csptPageNavComponent,
    csptSelectComponent,
    csptPaginatorComponent
  ],
  imports: [
    IndexRoutingModule,
    SharedModule,
  ],
  exports:[
    csptTableComponent,
    csptPageNavComponent,
    csptSelectComponent,
    csptPaginatorComponent
  ]
})
export class IndexModule { }

```
请注意 以上无效，最终我把所有component组件都放入share.module

### angular2 Maximum call stack size exceeded

这个问题发生在我index.module懒加载user.module时，use.module import了index.module  去掉即可
https://stackoverflow.com/questions/42811049/angular-2-cli-error-in-maximum-call-stack-size-exceeded

后续

将共同的component放在shared.module中
[routerLink]会报错（属于angular route）
建议使用js的方法跳转相对路由  相对路由可以使页面不跳转
参考链接 http://www.cnblogs.com/jiagoushi/p/6108039.html


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

### No value accessor for form control with unspecified name attribute

 @input 格式错误
 
 
### angular2 简书博客问题记录
 
 http://www.jianshu.com/p/a5402332315d
 
 $compile转换
 
 @HostListener
 
 router
 
 interceptor
 
 form
 
### angular2 extends super
 
 需要写成class的写法
 不能用 = function()
 
 
### angular2 extands super this 回调与this作用域问题

https://ashan.org/archives/655/

将回调用的函数写成闭包可以将this作用域封闭

### angular2 BUG record

**单向数据绑定BUG**
在系统分页中 ，通过单向数据绑定page.start 
如HTML:[start]="mainTable.paginator.start"
TS:this.mainTable.paginator.start = 1;
当start属性被第二次通过this.mainTable.paginator.start赋值为1时失效，
导致页码无法改变bug，暂时无法看出系统BUG，故归为单向绑定的bug记录。
最终发现是内部改变导致单向数据绑定失效，改为双向数据绑定成功[(start)]="mainTable.paginator.start" 但仍有一定问题

**论*ngIf影响viewChild（viewChild元素undefined）**

在ngIf下的组件元素被viewchild调用时会在ngOninit之后被注册，
因此ngOninit中调用该viewchild为undefined，需要在ngAfterinit中调用，或者放弃*ngIf改为[hidden]

### angular2 component

**viewChild组件初始化**
实例描述
```
@ViewChild(csptReportComponent)
  report:csptReportComponent; 
  
  
    this.report.show =true;
    this.report.report = o;
    this.report.content = {
      id:o.standardCourseId,
      type:"standardCourses",
      description:o.courseName,
      fullname:_this.localStorage.getObject('config').session.iam.fullName,
      source:"witwin"
    };
```
  在父组件中引用该子组件,同时该子组件包含四个孙子组件
`@ViewChild(csptReporttableComponent)
  csptReporttable:csptReporttableComponent;
  @ViewChild(csptReportformComponent)
  csptReportform:csptReportformComponent;
  @ViewChild(csptReportdealComponent)
  csptReportdeal:csptReportdealComponent;
  @ViewChild(csptReportdetailComponent)
  csptReportdetail:csptReportdetailComponent;`
  现在我要在父组件中动态显示隐藏csptReportComponent，在显示的时候希望能够初始化该组件包括所有的孙子组件，
*part1*
`this.report.constructor();`
ngIf受到影响，无法第二次显示，this.report.show =true无效
*part2*
`this.report = new csptReportComponent(this.objectService,this.sessionLocalStorageService,this.csptProcessing,this.config,this.commonCtlService,this.reportService,this.localStorage);`
在 this.report.report = o;报错
`  set report(n){
    this._report = n;
    this.csptReporttable.report = n;
    this.csptReportform.report = n;
    this.csptReportdeal.report = n;
    this.csptReportdetail.report = n;
  }`报错，原因不明白，不选择
  
 *part3*
` this.report.ngOnInit();`
可用，相当于调用组件的方法，需要在组件中写上详细的初始化，目前选这个
  
  以上方法只能初始化组件中的数据，无法初始化组件中的html元素，未完待续
 https://stackoverflow.com/questions/35105374/how-to-force-a-components-re-rendering-in-angular-2


### angular2 组件库
 
 - https://www.primefaces.org/primeng/#/responsive  PrimeNG
 - 阿里的组件库zorro  
 
### ng2兼职

http://www.jianshu.com/p/3f38e60f18ef


### zone.js学习记录

就是angular2用的脏检查机制
