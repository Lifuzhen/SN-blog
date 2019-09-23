
之前在人家网站上看到，我都能玩半个小时。
今天刚好看到了这个插件：react-canvas-nest,用来写写

[演示效果](https://lifuzhen.github.io/create-react-app-antd-less/build/#/nest)

在react环境下使用的
```
安装：

npm install react-canvas-nest
```

```
使用代码：

import React from "react";
import ReactCanvasNest from "react-canvas-nest"; //引入

class Home extends React.Component{
    render(){
        return <ReactCanvasNest
             className='canvasNest'
              config={{
                    pointColor: '173, 188, 213 ',
                    lineColor: '185, 198,219',
                    lineWidth: 2,
                    count: 120,
                    pointR: 1.5
                }}
              style={{zIndex: 1}}
          />
    }
}
export default Home;
```

效果如下所示：

![](../assets/超级酷炫的粒子围绕鼠标的效果(react-canvas-nest)/Animation.gif)


## API

config
![config](../assets/超级酷炫的粒子围绕鼠标的效果(react-canvas-nest)/config.png)

style 
Support style attribute, default style as follows:
![style](../assets/超级酷炫的粒子围绕鼠标的效果(react-canvas-nest)/style.jpg)

