# Angualr echarts

其他框架基本上通用



<!-- tabs:start -->

#### **angular.ts**

```javascript
import { Component, OnInit } from '@angular/core';


@Component({
  selector: 'app-dynamic-data',
  templateUrl: './dynamic-data.component.html',
  styleUrls: ['./dynamic-data.component.less']
})
export class DynamicDataComponent implements OnInit {

  option:any = {
    title: {
        text: '动态数据',
        subtext: '纯属虚构'
    },
    tooltip: {
        trigger: 'axis',
        axisPointer: {
            type: 'cross',
            label: {
                backgroundColor: '#283b56'
            }
        }
    },
    legend: {
        data:['最新成交价', '预购队列']
    },
    toolbox: {
        show: true,
        feature: {
            dataView: {readOnly: false},
            restore: {},
            saveAsImage: {}
        }
    },
    dataZoom: {
        show: false,
        start: 0,
        end: 100
    },
    xAxis: [
        {
            type: 'category',
            boundaryGap: true,
            data: (function (){
                var now:any = new Date();
                var res = [];
                var len = 10;
                while (len--) {
                    res.unshift(now.toLocaleTimeString().replace(/^\D*/,''));
                    now = new Date(now - 2000);
                }
                return res;
            })()
        },
        {
            type: 'category',
            boundaryGap: true,
            data: (function (){
                var res = [];
                var len = 10;
                while (len--) {
                    res.push(10 - len - 1);
                }
                return res;
            })()
        }
    ],
    yAxis: [
        {
            type: 'value',
            scale: true,
            name: '价格',
            max: 300,
            min: 0,
            boundaryGap: [0.2, 0.2]
        },
        {
            type: 'value',
            scale: true,
            name: '预购量',
            max: 1200,
            min: 0,
            boundaryGap: [0.2, 0.2]
        }
    ],
    series: [
        {
            name: '预购队列',
            type: 'bar',
            xAxisIndex: 1,
            yAxisIndex: 1,
            data: [0,0,0,0,0,0,0,0,0,0]
        },
        {
            name: '最新成交价',
            type: 'line',
            data: [0,0,0,0,0,0,0,0,0,0]
        }
    ]
};;
  updateOptions:any



  constructor() { }
  ngOnInit(): void {

    let option = {
        xAxis: [
            {
                type: 'category',
                boundaryGap: true,
                data: (function (){
                    var now:any = new Date();
                    var res = [];
                    var len = 10;
                    while (len--) {
                        res.unshift(now.toLocaleTimeString().replace(/^\D*/,''));
                        now = new Date(now - 2000);
                    }
                    return res;
                })()
            },
            {
                type: 'category',
                boundaryGap: true,
                data: (function (){
                    var res = [];
                    var len = 10;
                    while (len--) {
                        res.push(10 - len - 1);
                    }
                    return res;
                })()
            }
        ],
        series: [
            {
                name: '预购队列',
                type: 'bar',
                xAxisIndex: 1,
                yAxisIndex: 1,
                data: [0,0,0,0,0,0,0,0,0,0]
            },
            {
                name: '最新成交价',
                type: 'line',
                data: [0,0,0,0,0,0,0,0,0,0]
            }
        ]
    }
    let count = 11
    setInterval(() => {

        var axisData = (new Date()).toLocaleTimeString().replace(/^\D*/, '');

        var data0 = option.series[0].data;
        var data1 = option.series[1].data;

        data0.shift();
        data0.push(Math.round(Math.random() * 1000));
        data1.shift();
        data1.push(+(Math.random() * 100 + 5).toFixed(1) - 0);

        option.xAxis[0].data.shift();
        option.xAxis[0].data.push(axisData);
        option.xAxis[1].data.shift();
        option.xAxis[1].data.push(count++);


        this.updateOptions = {
            xAxis: [
                {
                    type: 'category',
                    boundaryGap: true,
                    data: option.xAxis[0].data
                },
                {
                    type: 'category',
                    boundaryGap: true,
                    data: option.xAxis[1].data
                }
            ],
            series: [
                {
                    name: '预购队列',
                    type: 'bar',
                    xAxisIndex: 1,
                    yAxisIndex: 1,
                    data:data0
                },
                {
                    name: '最新成交价',
                    type: 'line',
                    data: data1
                }
            ]
        }
   
    }, 2100);
  }

}
```

#### **Html**

```html
<div echarts [options]="option" [merge]="updateOptions" class="demo-chart" style="width: 800px;"></div>
//option 是定义初始数据
//merge 是每次定时更新对比的数据-- echarts会比较改动的部分，然后进行实时变化
```

<!-- tabs:end -->







<!-- tabs:start -->

<!-- tabs:end -->

