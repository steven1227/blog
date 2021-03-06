#JavaScript全讲-架构原则透析

*2016-02-27* [Aric](javascript:void(0);)

由于最近一直在忙，很久没有更新，见谅。

上篇我们讲完JavaScript函数式编程的特性，今天我们就来聊聊JavaScript中的架构。

提到JavaScript架构，很多人会觉得不可思议，因为架构多是针对类似Java这种强语言，而JavaScript一直被看成是弱语言，它有设计模式，可以用来构建架构吗？

答案无疑是肯定的！ 设计模式本身是一种很重量级的东西，当JavaScript被当做辅助使用时，谈架构反而会增加复杂度！ 所以这么多年，大家并没有看到JavaScript关于设计模式，架构之类的文章。而现今Web的发展，前端越来越重要，自然而然会推动JavaScript关于设计模式，架构方面的发展。

由于JavaScript和Java的截然不同，在讨论设计模式时，我们不能直接套用Java中关于设计模式的讲解方法，而是从另一方面来讲解。设计模式的SOLID原则鼎鼎大名，今天我们就通过SOLID原则来透析JavaScript中的架构。

**1. 单一职责（Single Responsibility）**

简单说，就是一个类只要负责一种职责即可，如果有多个职责需要处理，那就分离另外一个类。

之前我们有讲过JavaScript的面向对象特性，通过对象的封装，我们可以把单一职责在一个对象实现即可。这就完美符合了单一职责。

这么说起来，很多程序员肯定会很鄙视，这有什么好说的？ 其实单一职责表面上很简单，任何人都能信手拈来，但是它作为设计原则中最基础的原则，是有原因的！

封装并不困难，困难的是在任何时候能准确的分离职责。举个例子：

单就系统登录功能，我们把它作为一个职责来看！ 但是随着需求的复杂，会有更多的情况出现:

- 添加了验证码功能，要不要分离职责？


- 添加用户有效期验证，要不要分离？


- 增加用户邮箱验证功能，要不要分离？

如果你一直不分离，随着需求的增加，你会被拖入万劫不复的境地，不要认为这是危言耸听！ 但是反过来说，要如何分离，如何做到恰到好处的分离，是需要多年软件经验才能做到的。

基础招式的出神入化，虽不能让你杀敌于千里之外，但会让你立于不败之地！

**2. 开闭原则，对扩展开放，对修改关闭（Open Close）**

这个原则听起来比较含蓄。通常程序的表现形式是继承！ 即有一个公共的父类，任何子类想要实现特殊的需求，都只要重写或者增加方法即可。实现起来，就是设计模式中的模板方法，别名钩子方法。

JavaScript是支持继承的。我们就用伪代码来解释如何实现模板方法，并且在子类中重写。

![开闭原则，对扩展开放，对修改关闭](http://mmbiz.qpic.cn/mmbiz/Y47sfVtxGfTRcm5RpjBRxba0IFQj1Y2WM53fdejDkicdT5k6icd01HG4nibicP1lxj9hjlpoziceWaRTiaian1dFKG8icA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

这种方式是开闭原则最直接的体现！ 从伪代码可以体会到，只要基础功能不变，我们都不需要修改Base类，而只要扩展其功能即可。

**3. 里氏替换原则（Liskov Substitution）**

听起来更加含蓄了！用简单的话说，就是不要瞎搞！ 

就如上面的例子，你的需求FormView大部分都能实现，所以需要继承FormView。但是你又有一个需求，功能和FormView压根不沾边，但是你强行继承FormView，全部重写来来实现自己的代码，这就是乱搞了。

 里氏替换，就是在任何时候，用父类直接代替子类，都能实现大部分功能，上面的乱搞方式，父类根本不能替换子类使用，就违背了该原则。

**4. 接口隔离（Interface Segregation）**

同单一职责思想差不多，单一职责是面向内部，即如何分离职责。而接口隔离，是如何提供更好的外部接口。

这个外部不是指WebService形式的接口，而是指类向外暴露的功能接口。

说简单点，**就是不要让一个类过于庞大混乱**，只负责一部分功能。让其他使用的人可以清晰的分辨。

**5. 依赖倒置（Dependence Inversion）**

高层不能依赖底层，其实很多人并不能什么叫高层，什么叫底层！这样学术的话，只能误导很多的新手。我们简单来说：这里的高层和底层就如建大厦，高层如果是23层，那么底层就是22层，建大厦时，23层一定要依赖于22层（这不是废话吗）

![依赖倒置](http://mmbiz.qpic.cn/mmbiz/Y47sfVtxGfTRcm5RpjBRxba0IFQj1Y2Wzwr8vXWticVDMUF4A7hHicna1ibfdoB2YGyyxfX3L6ZAIXCf6s53gFeLQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1)

那么，套用到软件中，功能A和功能B，功能A依赖功能B，即功能A中需要调用B的接口，那么我们可以说：功能A是依赖于功能B，功能A是高层，功能B是底层。

那么如何理解“不能依赖”呢？ 大厦的23层如果不能依赖22层，那不是扯淡吗？

在软件中，一个模块过多依赖于其他模块，那么它就是一团乱麻的中心点，为什么这么说呢？

假如模块A依赖很模块，伪代码就如下

![依赖倒置1](http://mmbiz.qpic.cn/mmbiz/Y47sfVtxGfTRcm5RpjBRxba0IFQj1Y2WLIDAC2t9Hgpj6G6CuKYPibUxnndsBblwfEuXVjnwzMg46vCpLCzI7Ow/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

这样的代码在软件后期对开发者就如噩梦一般。B C D模块的任何修改都有可能引起A代码的改动，可能很多开发者说，我的功能很简单，不会修改的！ 如果是这样，基本证明你的软件，要么不是给人用的，要么就是没人用！

**那么如果我们不能直接使用依赖，要如何处理这种代码引用呢？**

伴生依赖倒置的模式，就是依赖注入！这个可真是大名鼎鼎，Spring的基础之一。没有它，在现在来说，我们根本没办法写代码了。

它的核心思想也很简单，类似于我们去吃自助餐，我想吃牛扒，直接去拿就好了，不用我去烹饪。

用程序的语言来讲，我想吃牛扒，是我要依赖牛扒，本来我要亲手new一个牛扒，但是这时候由于有了厨师，我直接拿来吃就可以了。所以别名依赖倒置。

如果这时候，我都不用去拿牛扒，厨师直接送过来，这叫依赖注入！

我的牛扒吃完之后，师傅拿回去，直接给别人再继续吃，这叫单例注入，虽然有点恶心，但是很高效率！万一上面有异物（被别人修改了），这叫单例污染！

师傅每天预先做10个牛排，谁要给谁送去！这叫单例池，类似于连接池。

依赖注入在在我们平时的开发中处处可见，这里大家只要理解其思想即可。接下来，我们就要讲讲在JavaScript中如何实现依赖注入了？这里只用其伪代码实现其简单的思想

![构造对象池](http://mmbiz.qpic.cn/mmbiz/Y47sfVtxGfTRcm5RpjBRxba0IFQj1Y2W7J5kvuhJn0dqh7ntCsacymMz2uXgia45dBdPPf131lFbBSgicftvgHcw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

随着各种JS MVC框架的流行，依赖注入也在前端越来越流行，目前做的最好的就属AngularJS！有兴趣的同学可以深入学习。

上面五个原则的首字母拼在一起就是**SOLID**，构成了软件稳固的架构。

大家可能会发现五个原则都是非常简单的原理，事实也确实如此。但是熟练掌握并且灵活运用到软件中，却不是一件简单的事情。尤其它的表现形式-设计模式，复杂多变，很多更是雌雄同体，根本分不清楚，让我们困恼不堪，同时又让广大程序员欲罢不能，真真是痛并快乐着。

JavaScript作为面向对象的语言，具备实现架构的条件，类似BackBone，AngularJS等MVC框架已经逐渐引领前端。随着它们的持续发展，前端开发终将像Java一样可控，这对所有开发人员都是一大福音。

最后送给所有程序员一句话：如果你想的太多，那是因为你代码写的太少。

