---
title: TypeScript--面向对象特性(09)-注解
categories:
  -TypeScript
---
注解为程序的元素加上更为直观更明了的说明，这些说明信息与程序的业务逻辑无关，而是供指定的工具或框架使用的，下面来看一个demo
```javascript
import { Component ,OnInit} from '@angular/core';
import { EchartsServer } from './echarts.server/echarts.server';
import { Observable } from 'rxjs/Observable'
declare var echarts:any;
@Component({
	moduleId:module.id,
	selector:'my-echarts',
	templateUrl:'echart.bar.component.html',
	styleUrls:['echart.bar.component.css']
})
export class echartsBarComponent implements OnInit {
	private Observable = new Observable();
	constructor (private echartsServer:EchartsServer){}
	responseData:any;
	getData():void{
		 this.echartsServer.getData().then(data=>this.responseData=data)
		}
	resetData():void{
		 this.getData()
  		console.log(this.responseData)
	}
  ngOnInit():void{

  		let myEchart = echarts.init(document.getElementById('myCharts'))
  		console.log(myEchart)
  		myEchart.setOption({
		    title: { text: 'ECharts 入门示例' },
		    tooltip: {},
		    xAxis: {
		        data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
		    },
		    yAxis: {},
		    series: [{
		        name: '销量',
		        type: 'bar',
		        data: [5, 20, 36, 10, 10, 20]
		    }]
		});
  }
}
```
这是一个用ng2写的一个demo，我们可以从例子中看到有一个声明了一个echartsBarComponent类，在这类上面有一个注解(@Component),这个注解就是有angular2提供的，在这个注解中有些属性，例如moduleId、selector、templateUrl、styleUrls，这些属性会告诉angular2怎么来处理echartsBarComponent这个类。当angular2处理这个类时候会去加载'echart.bar.component.html'这个html和'echart.bar.component.css'这个css，然后渲染在页面上。这就是注解，用来告诉框架怎么来处理你的程序的元素，上面程序的元素就是一个类echartsBarComponent，下面来看看html、css和结果
html
```html
<h3>angular2引入echarts画柱状图</h3>
<button (click)="resetData()">重新获取数据</button>
<div id="myCharts">
	
</div>
```
css样式
```css
#myCharts{
	width: 300px;
	height: 300px;
	border: 1px solid red;
}
```
结果
![](/img/09/01.png)