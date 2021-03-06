#  前端开发，面试技术问题  

http://www.imooc.com/wenda/detail/323379 



当我们面在谈面试的时候，我们在说什么？

大家都在聊技术，而且都讲的很细，但是我觉得一些比较细的东西同学们可以利用搜索工具自行脑补。

首先面试不仅仅是面试，我觉得一场好的面试，你先要了解这个家公司，比如规模，团队气氛，工作环境等的一系列的东西。（这样的好处是，对公司负责，更对自己负责，避免浪费双方时间，每一次好的面试都是你的收获）。

既然我们认可了这家公司，那么就可以开始面试的准备工作了。作为一名前端工作者，我们可以先去该公司的官网看一下这家公司的发展历程（前面提到过），目标，愿景等，然后F12，看一下他们的源码，用了哪些框架，技术，等，有那些是你很了解的技术，哪些又是你比较欠缺的呢？

了解完了环境和技术就该准备去面试了，大部分程序汪都是比较傲娇的，穿着方面不是很注重，但是我建议大家面试的时候穿着干净，整洁，头发什么的必须洗干净打理好，第一印象非常重要。当然，如果你的技术已经达到登峰造极的境界，可以无视上面4条。

既然开始面试了，那么该讲开场白了，一个好的自我介绍也是加分项，这方面网上很多（主要就是扬长避短类的），大家可以自行补充，我想说的是气场非常重要，面对面试官，你一定要自信，稳定，把握节奏。

最后一个重头戏来了，作为一个前端你所需要的必备技能，HTML+Css+Js,这个大家都懂，我就不多说了，我主要说一些常见问题，布局方面了解一下盒模型，Css2，Html4和Css3Html5的一些区别就可以了。Js是前端的核心竞争力，问的比较多的就是AJAX，JSON,封装，原型，设计模式，继承，这些东西了（细节方面请按照我的提示自行搜索）。






一、前言
面试过程中有做面试题的，也有直接聊的，实话讲有些面试题其实就是背书，随便一百度就能出答案的东西其实不太适合用于面试题中。例如某某css属性的用法，js某函数的作用等等。

个人倾向于将实际工作中可能会遇到的问题的场景，以及各种技术的坑作为面试题，这样一则可以看出他的经验多少，二则也可以防止他做笔试题的时候手机搜索结果。

不过总体来讲基本上每家问的问题也差不多，可能不同业务的公司问的问题的侧重点不太一样，有点侧重于移动端适配css布局浏览器兼容IE hack，而有的侧重于JS逻辑面向对象设计模式考察等，如果你有三到五年左右的开发经验这些问题基本也都遇见过，就算是做个总结吧。
二、手写事件模型及事件代理/委托

这个算是被问到的最多次数的问题了，首先要求描述下js里面的【事件的三个阶段】，如果没听说过三个阶段，那基本上就没戏了。分别是捕获，目标，冒泡阶段，低版本IE不支持捕获阶段。

然后可能问到IE和W3C不同绑定事件解绑事件的方法有什么区别，参数分别是什么，以及事件对象e有什么区别等等。

如果上述都没问题，接下来可能会问【事件的代理/委托】的原理以及优缺点，这是靠事件的冒泡机制来实现的，优点是：

1、可以大量节省内存占用，减少事件注册，比如在table上代理所有td的click事件就非常棒
2、可以实现当新增子对象时无需再次对其绑定事件，对于动态内容部分尤为合适

事件代理的应用常用应该仅限于上述需求下，如果把所有事件都用代理就可能会出现事件误判，即本不应用触发事件的被绑上了事件，事实上我见过有人把页面里的所有事件都绑定到document用委托的，这是极其不明智的做法。

所谓劲酒虽好，可不要贪杯哦~

之后对方可能要求你手写原生js【实现事件代理】，并要求兼容浏览器，其实就是考核对事件对象e的了解程度，以及在IE下对应的属性名。其实此时如果你说就是用target，currentTarget，以及IE下的srcElement和this，基本就可以略过了。

如果上述都ok的话，那么极有可能要求让你【实现事件模型】，即写一个类或是一个模块，有两个函数，一个bind一个trigger，分别实现绑定事件和触发事件，核心需求就是可以对某一个事件名称绑定多个事件响应函数，然后触发这个事件名称时，依次按绑定顺序触发相应的响应函数。

这个需求如果对于做过C#的人来讲就再熟悉不过，他根本就是C#中的【委托】（delegate）。而委托与事件几乎是一家子。

回到前面说的题目，大致实现思路就是创建一个类或是匿名函数，在bind和trigger函数外层作用域创建一个字典对象，用于存储注册的事件及响应函数列表，bind时，如果字典没有则创建一个，key是事件名称，value是数组，里面放着当前注册的响应函数，如果字段中有，那么就直接push到数组即可。trigger时调出来依次触发事件响应函数即可。

不过还有很多细节，比如触发响应函数时的上下文应该是什么，触发响应函数的参数列表应该是什么，如果要求把调用trigger的参数列表都传到响应函数中还要考虑到吧arguments对象转化为纯数组才行等等。

还有一些面试官会问到事件如何派发也就是事件广播（dispatchEvent）等等，这里不再展开。

有关事件的考核点大概也就这么多了。
三、前端性能优化

这个简直老生常谈，不管是园子里还是园子外，关于前端优化的东西太多太多了，不同角度不同方向也有很多，网络性能优化，加快访问速度，浏览器并行加载数量，怎样实现原生JS异步载入，CDN加速的原理，如何将不同静态资源发布到多个域名服务器上，发布后这些静态字段的url路径改怎么批量改写，用什么工具进行项目打包，css打包后的相对路径怎么转换为绝对路径，用什么工具进行项目模块依赖管理，怎么进行cookie优化等等，

这个说起来就很多了，尽可能的按照自己做过的优化来讲，否则面试官随便挑一项深究都可能会卡壳，与其这样还不如不讲。
四、闭包原理及应用

这个问题的经典性，几乎所有面试官都会问到这个问题，什么情况下会发生闭包，为什么需要闭包，什么场景下需要，闭包闭了谁，怎么释放被闭包的变量内存，闭包的优点是什么，缺点是什么等等。

关于闭包，有的是上述提问，有的是直接做闭包面试题。关于概念网上一搜一大把，关于闭包面试题，可以参考我之前写过的一篇文章：大部分人都会做错的经典JS闭包面试题（http://www.cnblogs.com/xxcanghai/p/4991870.html）。

不夸张的讲，如果这篇文章完全弄懂了，基本上没有可以难住的闭包的题目了。
五、手写Function.bind函数

首先会要求解释下这个函数的作用，以及在什么场景下需要用到它，最后手写一个Function.bind函数。

只要掌握核心几点就没问题：

1、Function.bind返回的也是一个函数，所以注定发生了闭包；
2、在返回的这个函数中去调用一个其他的函数，这其实本质上就是函数钩子(HOOK)；

关于在JS里的函数钩子，我认为只需要维护以下三点即可：

1、保持函数的this指向；
2、保持函数的所有参数都传递到目标函数；
3、保持函数的返回值；

有了以上这几点，这个函数就非常好写了，下面是MSDN上的标准Polyfill：
if (!Function.prototype.bind) {
  Function.prototype.bind = function (oThis) {
    if (typeof this !== "function") {
      // closest thing possible to the ECMAScript 5
      // internal IsCallable function
      throw new TypeError("Function.prototype.bind - what is trying to be bound is not callable");
    }

    var aArgs = Array.prototype.slice.call(arguments, 1), 
        fToBind = this, 
        fNOP = function () {},
        fBound = function () {
          return fToBind.apply(this instanceof fNOP
                                 ? this
                                 : oThis || this,
                               aArgs.concat(Array.prototype.slice.call(arguments)));
        };

    fNOP.prototype = this.prototype;
    fBound.prototype = new fNOP();

    return fBound;
  };
}
六、手写数组快速排序/去重

不管是排序也好，还是去重也罢，都是计算机基础知识了，虽然快排写出来了，去重也用多种方式实现了，但是算法是我的弱项，这里就不展开了。

不过对于准备面试的童鞋来讲，准备下常用算法还是比较重要的，大部分公司还是比较看重此类基础知识的。
七、JS的定义提升

利用js的特性定义提升这个知识点衍生出来的面试题相当之多，诸如以下等等
(function(a){
    console.log(a);
    var a=10;
    function a(){};
}(100))

这算是我做过的定义提升里面的最简单的题目了,建议可以看下我的上一篇文章：一道常被人轻视的前端JS面试题（http://www.cnblogs.com/xxcanghai/p/5189353.html）

基本上能做对那篇文章中所说的题目的话，此类面试题基本平趟无悬念
八、跨域

关于跨域大概可以分iframe的跨域，和纯粹的跨全域请求。

关于跨域的可以去看园子里的这几篇文章:

JavaScript跨域总结与解决办法（http://www.cnblogs.com/rainman/archive/2011/02/20/1959325.html）
跨域-知识（http://www.cnblogs.com/scottckt/archive/2011/11/12/2246531.html）
跨域资源共享的10种方式（http://www.cnblogs.com/cat3/archive/2011/06/15/2081559.html）

其实正统的跨全域的解决方法大致也就，JSONP,Access Control和服务器代理这么三种
九、JSONP原理

只要你聊到跨域，就必须聊到JSONP，那么就必须要讲一下JSONP的实现原理，以及你在项目中那个需求使用了JSONP，这里简单讲就是HTML里面所有带src属性的标签都可以跨域，如iframe，img，script等。

所以可以把需要跨域的请求改成用script脚本加载即可，服务器返回执行字符串，但是这个字符串是在window全局作用域下执行的，你需要把他返回到你的代码的作用域内，这里就需要临时创建一个全局的回调函数，并把到传到后台，最后再整合实际要请求的数组，返回给前端，让浏览器直接调用，用回调的形式回到你的原代码流程中。

基本讲到这也就没什么要再讲的了。
十、将url的查询参数解析成字典对象

这个题目不约而同的出现在了多家公司的面试题中，当然也是因为太过于典型，解决方案无非就是拆字符或者用正则匹配来解决，我个人强烈建议用正则匹配，因为url允许用户随意输入，如果用拆字符的方式，有任何一处没有考虑到容错，就会导致整个js都报错。而正则就没有这个问题，他只匹配出正确的配对，非法的全部过滤掉，简单，方便。

实现代码：
function getQueryObject(url) {
    url = url == null ? window.location.href : url;
    var search = url.substring(url.lastIndexOf("?") + 1);
    var obj = {};
    var reg = /([^?&=]+)=([^?&=]*)/g;
    search.replace(reg, function (rs, $1, $2) {
        var name = decodeURIComponent($1);
        var val = decodeURIComponent($2);                
        val = String(val);
        obj[name] = val;
        return rs;
    });
    return obj;
}
十一、函数节流

对于常见的场景，如网页滚动时，经常会有滚动到哪时做什么样的动画效果，遂要注册onscroll事件，如何减少触发次数，到达优化性能，同时又满足效果要求不卡顿，一个是优化事件内代码，减少代码量，二就是做函数节流。

大部分节流都采用时间做节流，即时间间隔小于多少的不再调用，但同时保证一个最小调用间隔。（否则拖拽类的节流都将无效果），也可以用调用次数做节流，但要考虑最后一次调用需要要执行。

可以参考：浅谈javascript的函数节流(http://www.alloyteam.com/2012/11/javascript-throttle/)。
十二、设计模式

这方面被问到的比较多的有观察者模式，职责链模式，工厂模式。

主要是应用于js开发组件中会经常涉及，纯粹的页面业务逻辑可能涉及不多。

比如如何去设计一个前端UI组件，应该公开出哪些方法，应该提供哪些接口，应该提供哪些事件。哪部分逻辑流程应该开放出去让用户自行编写，如何实现组件与组件之间的通信，如何实现高内聚低耦合，如何实现组件的高复用等等
十三、css垂直居中方法

可以看到我提到上面大多数都是关于JS的面试题，主要是因为css并不是我的强项，但有几个出现频率很高，就是经典的垂直居中问题。

这个问题又可以细分为，被垂直居中的元素是否定高，是文字还是块，文字是单行还是多行文字等等

这个可以百度下，有N多种解决方案，主要还是看应用场景的限制。
十四、自适应布局

这个问题可以划分为：左固定右自适应宽度，上固定下固定中间自适应高度等等布局要求。

关于左右自适应的，不低于10种解决方案，还要看dom结构要求是并列还是嵌套，是否允许有父级元素，是否允许使用CSS3，是否有背景色，是否要两列等高，等等

而关于自适应高度的解决方案就略少一些，大致也是靠，CSS3的calc属性，内padding，绝对定位后拉伸，动态js计算等等解决方案，同样也是要看应用场景能用哪个
十五、移动端自适应

也被问到了很多移动端开发中的各种坑，比如2倍屏，3倍屏的自适应等，我移动端的经验略少，所以只是按照我做过的经验去尽可能的描述清楚，这里就不多说了
十六、其他关于前端

除了技术以外，因为带过一个小团队，所以更多的时间都是去聊关于项目，关于团队，关于如何管理，关于如何处理团队内问题，如何跨团队协作等等。这部分纯属工作经验了，按照做过的不同项目也会有不同。










前端超常见的五大问题：
如何解决不同浏览器之间的兼容性问题，或者是否有遇到过兼容性问题，如何解决？

这一问题主要想考察面试者对于不同内核和不同版本（如css3和css，html5和html）的了解，所以主要聊一下知道的不同浏览器之前一些差异（如空格大小不同等）及不同版本如何兼容（做多种处理方法）之类的即可；
    2.一个网页从地址栏输入url到最后在浏览器中显示，中间经过了那些过程？
这个是网上比较多人认为问得较有水平的一个问题，需要了解整个从域名到Ip到具体请求的整个流程，原理可以一两句话简单概括，也可以讲得比较细致，但之后一般会牵引出面试官想要问的其他问题；
    3.Cookie、session、localStorage的区别和用法；
主要为了考察对于前端内容存储的一些问题，三者的明显区别，三者应该用在什么地方，什么情况应该用那种，可从这些方面进行回答；
    4.盒模型；
盒模型基本是前端学习的入门课，所以这也是比较多面试官想问的问题，考察基础；
    5.Doctype的意义、作用和具体内容；
Doctype用于声明DTD类型，但在Html5中已不再使用，所以这个问题会逐渐比较少问及。









从今年找实习以来，也面试了不少公司，包括tab,zhu场和zhu场游戏部门，整体感觉是，t的面试过程，整体感觉最轻松，聊天式，a的面试内容会稍微比较新一点，目前比较新的东西，要适当了解，有时间可以自己用一用。b的问题问的稍微深一点，zhu场的整体感觉相对稍微简单一点，但是zhu场游戏要求的还是比较多，不仅仅是前端，数据库，服务器这些也是要了解的哦。
下面我整理了一下，希望能帮到大家，面试的内容有交叉，有一部分东西也是根据个人经历扯出来的，还有的面试到了二、三面就不问这些基础的东西， 问的更多的是你的项目经历，解决问题的能力，未来的规划，我当时没记录下来，但是我个人认为最重要的就是一面和二面，大部分的人是跪在前两轮，也包括我自己，所以希望以下内容能有助于大家顺利过关前两轮。最好能帮到大家拿下offer：
面试一

内容包括项目介绍、跨域、闭包、原型、设计模式、CSS盒子、Linux一些命令，SVN拉分支，还有一些项目的前后台交互。HTML5新特性及离线存储。
首先是问项目，项目里你做的什么东西，写了哪些页面，前后台是怎么调用的，遇到了什么问题，你是怎么解决的。用的前端框架是什么？源码你看了吗？觉得这个框架的优缺点是什么？ 
接下来是基础问题了。具体问题记下了： 
1. 为什么要用闭包？你对闭包的认识，应用场景是哪些？ 
2. JS里的继承有哪些？口述一个原型继承的代码。 
3. 在项目开发中是否遇到了跨域问题？有哪些解决方案，jsonp与html5的解决方案是什么？ 
4. 讲讲几种简单的设计模式的应用场景。外观模式与适配器模式的区别。 
5. 常见的Linux指令你用过哪些？管道是用来干嘛的。 
6. 讲讲CSS的盒子模型，怎么区分和使用。 
7. SVN拉分支的命令是什么？ 
8. 你对加班怎么看？
面试二 
内容包括项目介绍、CSS3新特性、HTML5新特性。 
首先是问项目，用的框架是什么（因为自己用的是公司内部框架，所以这个问题一般都会问。），这个框架与Angular有什么不一样？源码是否了解？ 
接下来是基础问题了。问的比较新，我就跪在这。具体问题记下了： 
1. CSS3 动画用过吗？animation有那几个属性？Transition呢？（自己用的都是jQuery里的animate，和他讲错了），那时候心里已经开始慌了，CSS3和Html5新特性只是了解一些，稍微一深入，就有点吃不消，我和他讲，平时公式用的CSS都是公共的，有专门的负责样式的自己只是拿过来用就是，对css掌握的不是很好。果然下面到了html5. 
2. Html5里的离线存储平时用过么？有哪些。Cookie与WebStorage的区别。 
3. Html5里的多线程知道吗，如何创建一个线程？线程嵌套了，他们之间是怎么通信的？ 
面试到此结束。我了他哪里答得不好？前端知识更新快，对于一些新东西要快速学习，快速理解。有一些比较重要的东西，光会用是不够的，里面的一些原理还是要弄清楚。

面试三 
内容包括项目介绍、JS闭包、HTML5跨域处理。整体来说这个面试最美压力，整个过程就是聊天一样。技术性东西没怎么聊。 
1. 首先问了一下为什么首选城市是上海？愿不愿去深圳。 
2. 学的是通信，为什么要选前端？你觉得你对于计算机专业有什么优势与不足？ 
3. 聊了大概十分钟的项目，吐槽了一下在实习遇到的部门沟通与最佳实践的种种问题，他也表示感同身受。 
4. 最后问了JS闭包、HTML5跨域处理。


面试四 
首先聊项目，这里聊得还可以，满顺畅的，但是接下来我犯了一个严重错误，就是因为聊得顺畅。我给他介绍了一个比较厉害的功能实现。但是其实这里在具体的项目中不是我实现的。记住一点不会就不要乱吹，不然是搬起石头砸自己的脚。 
聊完项目，开始聊知识点了，总体感觉是问的比较深，一共就问了4个问题，但是一个问题会拓展下去。 
1、 JS事件模型与事件流介绍一下，事件代理用过吗？自定义事件，事件广播和分发【答得不好】 
2、 浏览器原理，和他讲了一通。Js是怎么解析的？什么时候执行的？but定时器的执行原理【答的不好】 
3、 怎么设计一个JS组件。【复用性，扩展性】 
4、 jQuery与angular有什么特点。源码里哪里比较有特色。

总结：自己的做的要比较熟，一些基础的东西不能浮在表面，要深入一点，被问到的时候不能虚，会多少答多少，不会了就直接说出来，我当时不会了就在那里，一直让面试官等着，最后面试官问了句，你还在吗？这印象太不好了。干脆利落，他可能会多问几个问题，拖拖拉拉，对方可能就不想问了。

面试五

这里提醒一下，腾讯的电话，我事先没接到，前一天晚上打球去了，打球回来洗澡去了，晚上十点打了我两个电话没接到，第二天中午我直接打过去了，是hr接的电话，下午就电话就来了。
这次记住了上次的教训，聊项目的时候，可以给面试官挖几个坑，因为这次面试的明显能感觉出来是个boss。坑在哪里？坑是自己掌握的比较好，在聊项目的时候可以吸引到面试官的点，稍微带一带方向，下一个问题面试官可能就是要问你这个问题了。 
第一坑： 
我给他挖的第一个是angular的源码分析。（较上次jQuery源码的教训，还不如讲自己比较熟的angular）。 
为什么会挖这个坑？因为项目用到的框架是企业内部的框架，没法和他讲，但是是对angular的封装，我说这个框架，企业内部因为我权限不够，无法查看源码，但我知道它是对angular与ajax的封装，我对angular比较熟。这样他就被吸引了。
完事了聊了聊实习的一些经历。讲了在企业学到的一些东西，因为我感觉他对我做过的东西不是很感兴趣，都是一些和具体业务有关。我就和他聊了一些企业管理的东西，从开发中的代码规范到最佳实践，再到敏捷开发流程，最后发现面试官比较喜欢听团队管理，又和他聊了一些部门间沟通的事情，部门间联调，加班的一些事。
最后问了我一些技术问题，问我对算法熟不熟？计算机网络怎么样？【这个是聊到了通信与计算机专业差异性问题，我是学通信的，他想了解一些我对计算机基础的知识的掌握程度。】我说数据结构与算法学过，但是都还给老师了，但是学校没有吧学费退给我。他又问计算机网络呢？我说还行，【因为当时心里不敢再说不怎么熟，我就说了还行】
问题：怎么减少http的请求次数？答了前端的东西，他要求从协议去解释，没有想出来。


面试六

刚开始聊项目，项目问了怎么实现的
1、根据项目问了cookie机制
2、ajax和jsonp的实现原理，用原生js怎么实现
3、如果要实现一个自定义的事件，要怎么实现
4、描述一下angularjs的模块注入和依赖注入
5、angularjs的双向数据绑定实现原理
6、响应式设计的一些问题，问了rem


面试七 
1.实习期间做了一些什么？ 
2.canvas是否熟悉，说一下一些常用api，以及canvas的性能是否有关注过，你项目里那个网页游戏用到了canvas，游戏的fps能有多少。 
3. 你项目中组件是怎么写的，如果要你写一个弹窗组件，你怎么写。 
4. 一个a标签绑定点击事件怎么阻止提交，又让我说具体原理。 
5. tcp和udp具体有哪些不同？ 
6. 实习时间是多长？



面试八 
问题好多，好散，大概问了大概30个问题。我尽量回忆。考察的知识面好多。 
1、 css兼容性处理。 
2、 纯css3实现360度旋转，不能用js。 
3、 Css动画用过吗？过渡函数有哪些？ 
4、 Css盒子，怎么设置？ 
5、 Css定位，怎么响应式布局双栏，多种方法。 
6、 选择器有哪些？给我出了具体的个题目，问能不能达到效果。关于伪类选择器的，我猜了一下不能。 
7、 原生js实现ajax的流程，状态码有哪些。 
8、 怎么区分不同的浏览器（火狐，IE，google）,多种方法。 
9、 Js声明函数的方式有哪些？分别有什么不同？ 
10、 闭包与匿名函数的区别，分别怎么用？举例子说明 
11、 BOM的常用属性 
12、 节点的增删改查分别怎么操作？ 
13、 Javascript的继承机制，有什么好处与不足。 
14、 Js事件流的处理兼容性处理，一共有哪些，【答全比较难。】 
15、 SE6的let与const有什么区别？ 
16、 用过sea.js与reqire.js吗？【表示没用过】 
17、 Angular用过吗？有哪些特性，原理是什么？ 
18、 在angular的开发中遇到过什么问题吗，双向绑定吗中数据模型变，v不显示。 
19、 移动端与PC端开发有什么不同？ 
20、 怎么设置响应式布局？ 
21、 Bootstrap响应式布局是怎么实现的？ 
22、 为什么频繁操作dom节点的代价比较大？ 
23、 Html5有哪些新特性，你用过哪些？ 
24、 http1.0与http1.1有什么区别？http2有神么新特性？ 
25、 数据库常见的存储引擎有哪些？有什么区别？ 



总结：问的问题都比较基础，但是设计的面很广，问题量比较大。基本覆盖了所有的重要的知识点。认真打好基础吧。










1、面试中曾遇到哪些技术问题，你的解决思路？                                          
    本人工作差不多3年，应该面试加起来有20来家公司，总结一下面试的经验吧。
    一般都是，首先，肯定是自我介绍，这个不说了，表现的有自信一点就行了。
    然后，就是介绍你做过的项目，这一环很重要，一般会在介绍你的做过的项目的时候，面试官会插入问你一些问题，比如，这个位置垂直定位当时会怎么想到用margin:auto+position:absolute的（这个问题很经典，关于垂直居中的问题，也是被问到最多的问题之一）？为什么不用跟其他的垂直居中方法呢？这时候如果代码是你自己写的，而且对垂直定位有一定深刻理解的，这个东西完全是小case，你就要结合你当时的开发思路，说明一下，这个和其他的垂直定位的区别，这个的优点是什么。如果问到不会的技术问题，或者被面试官指出你这个代码有问题的时候，怎么办呢？如果是代码有问题，直接说明，这个部分当时的确考虑得不够周到，谢谢提醒；如果是被问到不会的问题了，你可以尝试重复面试官的问题，确认面试官的问题，确认的目的是看面试官有没有表达错误导致你没理解，如果，真的不懂的话，也就直接直接回答说，不太熟悉相关方面就是了，勉强应对怕是只有反效果。
 2、开发过什么项目，遇到哪部分难题，又是如何克服的？ 
    本人开发过4个P2P平台前后端，和一个购物网站，一个教育平台网站。
    就拿购物网站为例子吧，碰到的难题就是自适应，而且要做成很人性化那种自适应，由于身边没有能指导的人，只能自己上网，模仿人家的那些自适应的网站的布局，把它们那些优秀的代码运用到自己的项目里面。这个有的人说是偷人家的东西，但我自己说不是偷啊，是参考，我会在参考别人网站的同时，结合自己的开发经验，思考一下，他这种的开发方式有没有什么问题？然后再在它基础上修改啊。（这里说的参考不是建议直接拿人家的源码，是参考人家的，在理解的基础上，自己手打代码，毕竟打一次之后，代码就是自己的了，脑子也清楚了。）
    之外，还有就跟同事，分享一下问题，共同探讨解决，说不定换个思路去想问题更好呢？
    最后，有一个私人赠送的解决问题的方法就是，关掉电脑，打卡下班，回家洗个澡，睡一觉，放松一下，明天来自然就有思路了。（这个方法我试过好多次，屡试不爽。）










