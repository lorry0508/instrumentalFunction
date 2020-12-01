## 一.定时器

#### 1发送短信倒计时案例

```js
<body>
    手机号码： <input type="number"> <button>发送</button>
    <script>
        // 按钮点击之后，会禁用 disabled 为true 
        // 同时按钮里面的内容会变化， 注意 button 里面的内容通过 innerHTML修改
        // 里面秒数是有变化的，因此需要用到定时器
        // 定义一个变量，在定时器里面，不断递减
        // 如果变量为0 说明到了时间，我们需要停止定时器，并且复原按钮初始状态
        var btn = document.querySelector('button');
        var time = 5; // 定义剩下的秒数
        btn.addEventListener('click', function () {
            btn.disabled = true;   //点击之后禁用按钮
            var timer = setInterval(function () {
                if (time == 0) {
                    // 清除定时器和复原按钮
                    clearInterval(timer);
                    btn.disabled = false;
                    btn.innerHTML = '发送';
                    time = 5; //非常重要，要不然永远是time = 0
                } else {
                    btn.innerHTML = '还剩下' + time + '秒';
                    time--;
                }
            }, 1000)
        })
    </script>
</body>
```

## 二.随机数

#### 1.获取指定范围内的随机整数

```js
//获取指定范围内的随机整数：
function getRandom(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min; 
}
```

#### 2.获取总毫秒数

```js
// 实例化Date对象
var now = new Date();
// 1. 用于获取对象的原始值
console.log(date.valueOf())	
console.log(date.getTime())	
// 2. 简单写可以这么做
var now = + new Date();			
// 3. HTML5中提供的方法，有兼容性问题
var now = Date.now();
```

## 三.javaScript

#### 1.检测浏览器是否支持svg

```js
function isSupportSVG() { 
    var SVG_NS = 'http://www.w3.org/2000/svg';
    return !!document.createElementNS &&!!document.createElementNS(SVG_NS, 'svg').createSVGRect; 
} 

// 测试
console.log(isSupportSVG());
```

#### 2.检测浏览器是否支持canvas

```js
function isSupportCanvas() {
    if(document.createElement('canvas').getContext){
        return true;
    }else{
        return false;
    }
}

// 测试，打开谷歌浏览器控制台查看结果
console.log(isSupportCanvas());
```

#### 3.**检测是否是微信浏览器**

```js
function isWeiXinClient() {
    var ua = navigator.userAgent.toLowerCase(); 
    if (ua.match(/MicroMessenger/i)=="micromessenger") { 
        return true; 
    } else { 
        return false; 
    }
}

// 测试
alert(isWeiXinClient());
```

#### 4.**jQuery 获取鼠标在图片上的坐标**

```js
$('#myImage').click(function(event){
    //获取鼠标在图片上的坐标 
    console.log('X：' + event.offsetX+'\n Y:' + event.offsetY); 

    //获取元素相对于页面的坐标 
    console.log('X：'+$(this).offset().left+'\n Y:'+$(this).offset().top);
});
```

#### 5.**验证码倒计时代码**

```js
<!-- dom -->
<input id="send" type="button" value="发送验证码">
  
  // 原生js版本
var times = 60, // 临时设为60秒
    timer = null;

document.getElementById('send').onclick = function () {
    // 计时开始
    timer = setInterval(function () {
        times--;

        if (times <= 0) {
            send.value = '发送验证码';
            clearInterval(timer);
            send.disabled = false;
            times = 60;
        } else {
            send.value = times + '秒后重试';
            send.disabled = true;
        }
    }, 1000);
}

// jQuery版本
var times = 60,
    timer = null;

$('#send').on('click', function () {
    var $this = $(this);

    // 计时开始
    timer = setInterval(function () {
        times--;

        if (times <= 0) {
            $this.val('发送验证码');
            clearInterval(timer);
            $this.attr('disabled', false);
            times = 60;
        } else {
            $this.val(times + '秒后重试');
            $this.attr('disabled', true);
        }
    }, 1000);
});
```

#### 6.**常用的一些正则表达式**

```js
//匹配字母、数字、中文字符 
/^([A-Za-z0-9]|[\u4e00-\u9fa5])*$/ 

//验证邮箱 
/^\w+@([0-9a-zA-Z]+[.])+[a-z]{2,4}$/ 

//验证手机号 
/^1[3|5|8|7]\d{9}$/ 

//验证URL 
/^http:\/\/.+\./

//验证身份证号码 
/(^\d{15}$)|(^\d{17}([0-9]|X|x)$)/ 

//匹配中文字符的正则表达式 
/[\u4e00-\u9fa5]/ 

//匹配双字节字符(包括汉字在内) 
/[^\x00-\xff]/
```

#### 7.**js时间戳、毫秒格式化**

```js
function formatDate(now) { 
    var y = now.getFullYear();
    var m = now.getMonth() + 1; // 注意js里的月要加1 
    var d = now.getDate();
    var h = now.getHours(); 
    var m = now.getMinutes(); 
    var s = now.getSeconds();

    return y + "-" + m + "-" + d + " " + h + ":" + m + ":" + s; 
} 

var nowDate = new Date(2016, 5, 13, 19, 18, 30, 20);

console.log(nowDate.getTime()); // 获得当前毫秒数: 1465816710020
console.log(formatDate(nowDate));
```

#### 8.**js限定字符数（注意：一个汉字算2个字符）**

```js
<input id="txt" type="text">
//字符串截取
function getByteVal(val, max) {
    var returnValue = '';
    var byteValLen = 0;
    for (var i = 0; i < val.length; i++) {
        if (val[i].match(/[^\x00-\xff]/ig) != null) byteValLen += 2; else byteValLen += 1;
        if (byteValLen > max) break;
        returnValue += val[i];
    }
    return returnValue;
}

$('#txt').on('keyup', function () {
    var val = this.value;
    if (val.replace(/[^\x00-\xff]/g, "**").length > 14) {
        this.value = getByteVal(val, 14);
    }
});
```

#### 9.**js判断是否移动端及浏览器内核**

```js
var browser = { 
    versions: function() { 
        var u = navigator.userAgent; 
        return { 
            trident: u.indexOf('Trident') > -1, //IE内核 
            presto: u.indexOf('Presto') > -1, //opera内核 
            webKit: u.indexOf('AppleWebKit') > -1, //苹果、谷歌内核 
            gecko: u.indexOf('Firefox') > -1, //火狐内核Gecko 
            mobile: !!u.match(/AppleWebKit.*Mobile.*/), //是否为移动终端 
            ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), //ios 
            android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1, //android 
            iPhone: u.indexOf('iPhone') > -1 , //iPhone 
            iPad: u.indexOf('iPad') > -1, //iPad 
            webApp: u.indexOf('Safari') > -1 //Safari 
        }; 
    }
} 

if (browser.versions.mobile() || browser.versions.ios() || browser.versions.android() || browser.versions.iPhone() || browser.versions.iPad()) { 
    alert('移动端'); 
}
```

#### 10.生成id

```js
guid() {
    return Number(Math.random().toString().substr(3, 3) + Date.now()).toString(36);
},
```

#### 11.工具函数封装

```js
function Dateformat(fthis, fmt) {
    var o = {
        "M+": fthis.getMonth() + 1, //月份
        "d+": fthis.getDate(), //日
        "h+": fthis.getHours(), //小时
        "m+": fthis.getMinutes(), //分
        "s+": fthis.getSeconds(), //秒
        "q+": Math.floor((fthis.getMonth() + 3) / 3), //季度
        "S": fthis.getMilliseconds() //毫秒
    };
    if (/(y+)/.test(fmt)) {
        fmt = fmt.replace(RegExp.$1, (fthis.getFullYear() + "").substr(4 - RegExp.$1.length));
    }
    for (var k in o) {
        if (new RegExp("(" + k + ")").test(fmt)) {
            fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
        }
    }
    return fmt;
}

//使用 Dateformat(new Date(),"yyyy-MM-dd hh:mm:ss")
```

