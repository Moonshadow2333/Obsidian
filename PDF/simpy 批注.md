---
annotation-target: simpy-readthedocs-io-en-4.0.0.pdf
---



>%%
>```annotation-json
>{"created":"2024-08-26T15:12:04.827Z","text":"1. 当一个 process 生成了一个 event 时，process 就会被挂起；\n2. 当 event 被触发时，process 得以恢复。","updated":"2024-08-26T15:12:04.827Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":8028,"end":8174},{"type":"TextQuoteSelector","exact":"When a process yields an event, the process gets suspended. SimPy resumes the process, when the event occurs (wesay that the event is triggered). ","prefix":"o wait for them to be triggered.","suffix":"Multiple processes can wait for "}]}]}
>```
>%%
>*%%PREFIX%%o wait for them to be triggered.%%HIGHLIGHT%% ==When a process yields an event, the process gets suspended. SimPy resumes the process, when the event occurs (wesay that the event is triggered).== %%POSTFIX%%Multiple processes can wait for*
>%%LINK%%[[#^8aaazqomvh4|show annotation]]
>%%COMMENT%%
>1. 当一个 process 生成了一个 event 时，process 就会被挂起；
>2. 当 event 被触发时，process 得以恢复。
>%%TAGS%%
>
^8aaazqomvh4


>%%
>```annotation-json
>{"created":"2024-08-26T15:14:42.045Z","text":"1. Timeout 是一种 event；\n2. 既然 Timeout 是一种 event，那么它什么时候被触发？自然是计时结束的时候；\n3. 作用：允许 event 睡觉","updated":"2024-08-26T15:14:42.045Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":8291,"end":8329},{"type":"TextQuoteSelector","exact":"An important event type is the Timeout","prefix":"n which they yielded that event.","suffix":". Events of this type are trigge"}]}]}
>```
>%%
>*%%PREFIX%%n which they yielded that event.%%HIGHLIGHT%% ==An important event type is the Timeout== %%POSTFIX%%. Events of this type are trigge*
>%%LINK%%[[#^116f80qk0h6j|show annotation]]
>%%COMMENT%%
>1. Timeout 是一种 event；
>2. 既然 Timeout 是一种 event，那么它什么时候被触发？自然是计时结束的时候；
>3. 作用：允许 event 睡觉
>%%TAGS%%
>
^116f80qk0h6j


>%%
>```annotation-json
>{"created":"2024-08-26T15:30:32.416Z","text":"例子：car process:\n\n- drive 和 park 两种状态；\n- car process 要求 env 作为参数，以创建新的参数；\n- car 的行为被描述为一个无穷的循环；","updated":"2024-08-26T15:30:32.416Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":8672,"end":8712},{"type":"TextQuoteSelector","exact":"Our first example will be a car process.","prefix":"example).2.2.1 Our First Process","suffix":" The car will alternately drive "}]}]}
>```
>%%
>*%%PREFIX%%example).2.2.1 Our First Process%%HIGHLIGHT%% ==Our first example will be a car process.== %%POSTFIX%%The car will alternately drive*
>%%LINK%%[[#^844u2vbifvv|show annotation]]
>%%COMMENT%%
>例子：car process:
>
>- drive 和 park 两种状态；
>- car process 要求 env 作为参数，以创建新的参数；
>- car 的行为被描述为一个无穷的循环；
>%%TAGS%%
>
^844u2vbifvv


>%%
>```annotation-json
>{"created":"2024-08-26T15:38:26.247Z","text":"[ˈyo͞odlˌīz] 利用","updated":"2024-08-26T15:38:26.247Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":11199,"end":11207},{"type":"TextQuoteSelector","exact":"utilized","prefix":"by Environment.process() can be ","suffix":" for process interactions.The tw"}]}]}
>```
>%%
>*%%PREFIX%%by Environment.process() can be%%HIGHLIGHT%% ==utilized== %%POSTFIX%%for process interactions.The tw*
>%%LINK%%[[#^xh5sncka6zh|show annotation]]
>%%COMMENT%%
>[ˈyo͞odlˌīz] 利用
>%%TAGS%%
>
^xh5sncka6zh


>%%
>```annotation-json
>{"created":"2024-08-26T15:39:44.561Z","text":"process 也是一个 event","updated":"2024-08-26T15:39:44.561Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":11476,"end":11506},{"type":"TextQuoteSelector","exact":"a process actually is an event","prefix":"sed like an event (technically, ","suffix":"). If you yieldit, you are resum"}]}]}
>```
>%%
>*%%PREFIX%%sed like an event (technically,%%HIGHLIGHT%% ==a process actually is an event== %%POSTFIX%%). If you yieldit, you are resum*
>%%LINK%%[[#^sd46f0r4kb|show annotation]]
>%%COMMENT%%
>process 也是一个 event
>%%TAGS%%
>
^sd46f0r4kb


>%%
>```annotation-json
>{"created":"2024-08-26T15:43:44.195Z","updated":"2024-08-26T15:43:44.195Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":10741,"end":10810},{"type":"TextQuoteSelector","exact":"The Process returned by process() can be used for process interaction","prefix":"d atthe current simulation time.","suffix":"s (we will cover that in the nex"}]}]}
>```
>%%
>*%%PREFIX%%d atthe current simulation time.%%HIGHLIGHT%% ==The Process returned by process() can be used for process interaction== %%POSTFIX%%s (we will cover that in the nex*
>%%LINK%%[[#^ahy9t498pmf|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^ahy9t498pmf


>%%
>```annotation-json
>{"created":"2024-08-27T15:25:00.850Z","text":"电车：\n\n- 在一场旅途之后需要花大量的时间充电；\n- 下一次开车之前需要等电池充满电。","updated":"2024-08-27T15:25:00.850Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":11846,"end":12013},{"type":"TextQuoteSelector","exact":"Electric vehicles usually take alot of time charging their batteries after a trip. They have to wait until their battery is charged before they can startdriving again.","prefix":"lly became an electric vehicle. ","suffix":"We can model this with an additi"}]}]}
>```
>%%
>*%%PREFIX%%lly became an electric vehicle.%%HIGHLIGHT%% ==Electric vehicles usually take alot of time charging their batteries after a trip. They have to wait until their battery is charged before they can startdriving again.== %%POSTFIX%%We can model this with an additi*
>%%LINK%%[[#^y21vb0bbl28|show annotation]]
>%%COMMENT%%
>电车：
>
>- 在一场旅途之后需要花大量的时间充电；
>- 下一次开车之前需要等电池充满电。
>%%TAGS%%
>
^y21vb0bbl28


>%%
>```annotation-json
>{"created":"2024-08-27T15:48:19.304Z","text":"中断 Process：\n\n- 不想等到电车充满电，而是想中断 Process，并直接开始开车；\n- 在 Simpy 中，可以使用 interrupt 方法中断正在运行的 Process；","updated":"2024-08-27T15:48:19.304Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":13585,"end":13726},{"type":"TextQuoteSelector","exact":"you don’t want to wait until your electric vehicle is fully charged but want to interrupt the charging processand just start driving instead.","prefix":"rupting Another ProcessImagine, ","suffix":"SimPy allows you to interrupt a "}]}]}
>```
>%%
>*%%PREFIX%%rupting Another ProcessImagine,%%HIGHLIGHT%% ==you don’t want to wait until your electric vehicle is fully charged but want to interrupt the charging processand just start driving instead.== %%POSTFIX%%SimPy allows you to interrupt a*
>%%LINK%%[[#^mwcfgfq6ln|show annotation]]
>%%COMMENT%%
>中断 Process：
>
>- 不想等到电车充满电，而是想中断 Process，并直接开始开车；
>- 在 Simpy 中，可以使用 interrupt 方法中断正在运行的 Process；
>%%TAGS%%
>
^mwcfgfq6ln


>%%
>```annotation-json
>{"created":"2024-08-27T15:59:05.165Z","text":"不太理解\n\n[中断另外一个 Process](https://blog.csdn.net/cloud1980_cn/article/details/105379027)\n\n[SimPy 离散事件模拟框架详解 —— 以一个简单的汽车充电排队模拟为例](https://www.cnblogs.com/zjutlitao/p/16846050.html)","updated":"2024-08-27T15:59:05.165Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":14005,"end":14130},{"type":"TextQuoteSelector","exact":"Interrupts are thrown into process functions as Interrupt exceptions that can (should) be handled by the interruptedprocess. ","prefix":"teps, it interrupts thatprocess.","suffix":"The process can then decide what"}]}]}
>```
>%%
>*%%PREFIX%%teps, it interrupts thatprocess.%%HIGHLIGHT%% ==Interrupts are thrown into process functions as Interrupt exceptions that can (should) be handled by the interruptedprocess.== %%POSTFIX%%The process can then decide what*
>%%LINK%%[[#^lpwpo7xdu9|show annotation]]
>%%COMMENT%%
>不太理解
>
>[中断另外一个 Process](https://blog.csdn.net/cloud1980_cn/article/details/105379027)
>
>[SimPy 离散事件模拟框架详解 —— 以一个简单的汽车充电排队模拟为例](https://www.cnblogs.com/zjutlitao/p/16846050.html)
>%%TAGS%%
>
^lpwpo7xdu9


>%%
>```annotation-json
>{"created":"2024-08-27T16:14:14.434Z","updated":"2024-08-27T16:14:14.434Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":15268,"end":15296},{"type":"TextQuoteSelector","exact":"env.process(driver(env, car)","prefix":"ironment()>>> car = Car(env)>>> ","suffix":")<Process(driver) object at 0x.."}]}]}
>```
>%%
>*%%PREFIX%%ironment()>>> car = Car(env)>>>%%HIGHLIGHT%% ==env.process(driver(env, car)== %%POSTFIX%%)<Process(driver) object at 0x..*
>%%LINK%%[[#^nmr4cufrgm8|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^nmr4cufrgm8


>%%
>```annotation-json
>{"created":"2024-08-28T15:12:49.348Z","text":"使用 Resource 的场景：\n\n- 开车去充电，并使用两个充电桩中的其中一个；\n- 现在两个充电桩都在使用中；\n- 等待直到充电桩可以再次被使用；\n- 充电并离开充电站。","updated":"2024-08-28T15:12:49.348Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":16322,"end":16423},{"type":"TextQuoteSelector","exact":"The car will now drive to a battery charging station (BCS) and request one of its two charging spots.","prefix":"introduced in the last sections.","suffix":" If both of thesespots are curre"}]}]}
>```
>%%
>*%%PREFIX%%introduced in the last sections.%%HIGHLIGHT%% ==The car will now drive to a battery charging station (BCS) and request one of its two charging spots.== %%POSTFIX%%If both of thesespots are curre*
>%%LINK%%[[#^79pxxxgoia|show annotation]]
>%%COMMENT%%
>使用 Resource 的场景：
>
>- 开车去充电，并使用两个充电桩中的其中一个；
>- 现在两个充电桩都在使用中；
>- 等待直到充电桩可以再次被使用；
>- 充电并离开充电站。
>%%TAGS%%
>
^79pxxxgoia


>%%
>```annotation-json
>{"created":"2024-08-28T15:22:37.477Z","text":"Resource 的 request() 方法：\n\n- 生成了一个事件；\n- 等待资源可以再次变得可用；\n- 如果你恢复，你拥有 resource 直到你释放它。","updated":"2024-08-28T15:22:37.477Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":17027,"end":17204},{"type":"TextQuoteSelector","exact":"The resource’s request() method generates an event that lets you wait until the resource becomes available again.If you are resumed, you “own” the resource until you release it.","prefix":"he bcs at %s' % (name, env.now))","suffix":"If you use the resource with the"}]}]}
>```
>%%
>*%%PREFIX%%he bcs at %s' % (name, env.now))%%HIGHLIGHT%% ==The resource’s request() method generates an event that lets you wait until the resource becomes available again.If you are resumed, you “own” the resource until you release it.== %%POSTFIX%%If you use the resource with the*
>%%LINK%%[[#^qw5hw6irc4n|show annotation]]
>%%COMMENT%%
>Resource 的 request() 方法：
>
>- 生成了一个事件；
>- 等待资源可以再次变得可用；
>- 如果你恢复，你拥有 resource 直到你释放它。
>%%TAGS%%
>
^qw5hw6irc4n


>%%
>```annotation-json
>{"created":"2024-08-28T15:28:48.213Z","text":"- resource 自动被释放：使用 with 关键字；\n- 如果调用 request() 方法时不用 with，需要在你使用完 resource 时使用 release() 方法去释放 resource. ","updated":"2024-08-28T15:28:48.213Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":17204,"end":17314},{"type":"TextQuoteSelector","exact":"If you use the resource with the with statement as shown above, the resource is automatically being released. ","prefix":"e resource until you release it.","suffix":"If youcall request() without wit"}]}]}
>```
>%%
>*%%PREFIX%%e resource until you release it.%%HIGHLIGHT%% ==If you use the resource with the with statement as shown above, the resource is automatically being released.== %%POSTFIX%%If youcall request() without wit*
>%%LINK%%[[#^pkk35izc24|show annotation]]
>%%COMMENT%%
>- resource 自动被释放：使用 with 关键字；
>- 如果调用 request() 方法时不用 with，需要在你使用完 resource 时使用 release() 方法去释放 resource. 
>%%TAGS%%
>
^pkk35izc24


>%%
>```annotation-json
>{"created":"2024-08-28T15:36:39.225Z","text":"一个 resource 需要一个实例 \n\n- environment\n- capacity","updated":"2024-08-28T15:36:39.225Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":17610,"end":17691},{"type":"TextQuoteSelector","exact":"A resource needs a reference to an Environment and a capacity when it is created:","prefix":"a FIFO (first in—first out) way.","suffix":">>> import simpy>>> env = simpy."}]}]}
>```
>%%
>*%%PREFIX%%a FIFO (first in—first out) way.%%HIGHLIGHT%% ==A resource needs a reference to an Environment and a capacity when it is created:== %%POSTFIX%%>>> import simpy>>> env = simpy.*
>%%LINK%%[[#^x0xsj7oc7sd|show annotation]]
>%%COMMENT%%
>一个 resource 需要一个实例 
>
>- environment
>- capacity
>%%TAGS%%
>
^x0xsj7oc7sd


>%%
>```annotation-json
>{"created":"2024-08-30T13:29:28.870Z","text":"第 0 辆车在第 5 秒离开了充电站，第 2 辆车在第 2 秒就到充电站，但是第 0 辆与第 1 辆车正在充电，所以只有等第 1 辆车离开之后，也就是第 5 秒才开始充电","updated":"2024-08-30T13:29:28.870Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":18438,"end":18464},{"type":"TextQuoteSelector","exact":"Car 0 leaving the bcs at 5","prefix":"o charge at 2Car 2 arriving at 4","suffix":"Car 2 starting to charge at 5(co"}]}]}
>```
>%%
>*%%PREFIX%%o charge at 2Car 2 arriving at 4%%HIGHLIGHT%% ==Car 0 leaving the bcs at 5== %%POSTFIX%%Car 2 starting to charge at 5(co*
>%%LINK%%[[#^2mduydt2fg6|show annotation]]
>%%COMMENT%%
>第 0 辆车在第 5 秒离开了充电站，第 2 辆车在第 2 秒就到充电站，但是第 0 辆与第 1 辆车正在充电，所以只有等第 1 辆车离开之后，也就是第 5 秒才开始充电
>%%TAGS%%
>
^2mduydt2fg6


>%%
>```annotation-json
>{"created":"2024-08-30T13:45:47.508Z","text":"Simpy 就是一个异步事件分发器。","updated":"2024-08-30T13:45:47.508Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":19806,"end":19876},{"type":"TextQuoteSelector","exact":"If you break SimPy down, it is just an asynchronous event dispatcher. ","prefix":" with them?3.1.1 How SimPy works","suffix":"You generate events and schedule"}]}]}
>```
>%%
>*%%PREFIX%%with them?3.1.1 How SimPy works%%HIGHLIGHT%% ==If you break SimPy down, it is just an asynchronous event dispatcher.== %%POSTFIX%%You generate events and schedule*
>%%LINK%%[[#^nxzpx4idttp|show annotation]]
>%%COMMENT%%
>Simpy 就是一个异步事件分发器。
>%%TAGS%%
>
^nxzpx4idttp


>%%
>```annotation-json
>{"created":"2024-08-30T13:49:20.394Z","text":"事件的排序规则：\n\n- 优先级；\n- 仿真时间；\n- event id；","updated":"2024-08-30T13:49:20.394Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":19941,"end":20016},{"type":"TextQuoteSelector","exact":"Events are sorted by priority, simulation time, and an increasing event id.","prefix":"them at agiven simulation time. ","suffix":" An event also hasa list of call"}]}]}
>```
>%%
>*%%PREFIX%%them at agiven simulation time.%%HIGHLIGHT%% ==Events are sorted by priority, simulation time, and an increasing event id.== %%POSTFIX%%An event also hasa list of call*
>%%LINK%%[[#^8mynm4777ep|show annotation]]
>%%COMMENT%%
>事件的排序规则：
>
>- 优先级；
>- 仿真时间；
>- event id；
>%%TAGS%%
>
^8mynm4777ep


>%%
>```annotation-json
>{"created":"2024-08-30T13:53:14.617Z","text":"一个事件有一系列的回调，事件也可以有返回值。","updated":"2024-08-30T13:53:14.617Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":20017,"end":20170},{"type":"TextQuoteSelector","exact":"An event also hasa list of callbacks, which are executed when the event is triggered and processed by the event loop. Events may alsohave a return value.","prefix":"me, and an increasing event id. ","suffix":"The components involved in this "}]}]}
>```
>%%
>*%%PREFIX%%me, and an increasing event id.%%HIGHLIGHT%% ==An event also hasa list of callbacks, which are executed when the event is triggered and processed by the event loop. Events may alsohave a return value.== %%POSTFIX%%The components involved in this*
>%%LINK%%[[#^s78olw3hzh|show annotation]]
>%%COMMENT%%
>一个事件有一系列的回调，事件也可以有返回值。
>%%TAGS%%
>
^s78olw3hzh


>%%
>```annotation-json
>{"created":"2024-08-30T13:54:12.404Z","text":"组成：\n\n- 环境；\n- 事件；\n- Process 函数；","updated":"2024-08-30T13:54:12.404Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":20170,"end":20270},{"type":"TextQuoteSelector","exact":"The components involved in this are the Environment, events and the process functions that you write","prefix":"nts may alsohave a return value.","suffix":".Process functions implement you"}]}]}
>```
>%%
>*%%PREFIX%%nts may alsohave a return value.%%HIGHLIGHT%% ==The components involved in this are the Environment, events and the process functions that you write== %%POSTFIX%%.Process functions implement you*
>%%LINK%%[[#^nudf74egto8|show annotation]]
>%%COMMENT%%
>组成：
>
>- 环境；
>- 事件；
>- Process 函数；
>%%TAGS%%
>
^nudf74egto8


>%%
>```annotation-json
>{"created":"2024-08-30T13:56:38.752Z","text":"Process 函数实现了仿真模型","updated":"2024-08-30T13:56:38.752Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":20271,"end":20446},{"type":"TextQuoteSelector","exact":"Process functions implement your simulation model, that is, they define the behavior of your simulation. They areplain Python generator functions that yield instances of Event","prefix":"rocess functions that you write.","suffix":".The environment stores these ev"}]}]}
>```
>%%
>*%%PREFIX%%rocess functions that you write.%%HIGHLIGHT%% ==Process functions implement your simulation model, that is, they define the behavior of your simulation. They areplain Python generator functions that yield instances of Event== %%POSTFIX%%.The environment stores these ev*
>%%LINK%%[[#^nge4eg004i|show annotation]]
>%%COMMENT%%
>Process 函数实现了仿真模型
>%%TAGS%%
>
^nge4eg004i


>%%
>```annotation-json
>{"created":"2024-08-30T14:42:37.853Z","text":"environment 存储了事件和追踪当前的仿真时间","updated":"2024-08-30T14:42:37.853Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":20447,"end":20547},{"type":"TextQuoteSelector","exact":"The environment stores these events in its event list and keeps track of the current simulation time","prefix":"s that yield instances of Event.","suffix":".If a process function yields an"}]}]}
>```
>%%
>*%%PREFIX%%s that yield instances of Event.%%HIGHLIGHT%% ==The environment stores these events in its event list and keeps track of the current simulation time== %%POSTFIX%%.If a process function yields an*
>%%LINK%%[[#^y10ag0ofnz|show annotation]]
>%%COMMENT%%
>environment 存储了事件和追踪当前的仿真时间
>%%TAGS%%
>
^y10ag0ofnz


>%%
>```annotation-json
>{"created":"2024-08-30T14:59:35.625Z","text":"Process 函数生成了事件：\n\n- Simpy 会把 process 添加至 event 回调中；\n- 挂起 process 直到 event 被触发或者执行完成；\n- 当一个等待 event 的 process 被恢复了，它会收到 event 的值。 ","updated":"2024-08-30T14:59:35.625Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":20548,"end":20788},{"type":"TextQuoteSelector","exact":"If a process function yields an event, SimPy adds the process to the event’s callbacks and suspends the process untilthe event is triggered and processed. When a process waiting for an event is resumed, it will also receive the event’svalue","prefix":" of the current simulation time.","suffix":".Here is a very simple example t"}]}]}
>```
>%%
>*%%PREFIX%%of the current simulation time.%%HIGHLIGHT%% ==If a process function yields an event, SimPy adds the process to the event’s callbacks and suspends the process untilthe event is triggered and processed. When a process waiting for an event is resumed, it will also receive the event’svalue== %%POSTFIX%%.Here is a very simple example t*
>%%LINK%%[[#^vj7o8pwnrwf|show annotation]]
>%%COMMENT%%
>Process 函数生成了事件：
>
>- Simpy 会把 process 添加至 event 回调中；
>- 挂起 process 直到 event 被触发或者执行完成；
>- 当一个等待 event 的 process 被恢复了，它会收到 event 的值。 
>%%TAGS%%
>
^vj7o8pwnrwf


>%%
>```annotation-json
>{"created":"2024-09-01T06:34:39.988Z","text":"environment 管理：\n\n- 仿真时间；\n- 计划和事件的过程","updated":"2024-09-01T06:34:39.988Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":23640,"end":23744},{"type":"TextQuoteSelector","exact":"A simulation environment manages the simulation time as well as the scheduling and processing of events.","prefix":"n, Release 4.0.03.2 Environments","suffix":" It alsoprovides means to step t"}]}]}
>```
>%%
>*%%PREFIX%%n, Release 4.0.03.2 Environments%%HIGHLIGHT%% ==A simulation environment manages the simulation time as well as the scheduling and processing of events.== %%POSTFIX%%It alsoprovides means to step t*
>%%LINK%%[[#^ujto1b2fuf|show annotation]]
>%%COMMENT%%
>environment 管理：
>
>- 仿真时间；
>- 计划和事件的过程
>%%TAGS%%
>
^ujto1b2fuf


>%%
>```annotation-json
>{"created":"2024-09-01T07:13:01.398Z","text":"运行仿真；\n\n- 直到没有 events；\n- 直到一个确定的仿真时间；\n- 直到一个特定的事件被触发；\n","updated":"2024-09-01T07:13:01.398Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":24029,"end":24276},{"type":"TextQuoteSelector","exact":"You can run your simulation until there are no more events,until a certain simulation time is reached, or until a certain event is triggered. You can also step through the simulationevent by event. Furthermore, you can mix these things as you like","prefix":" terms of simulation execution. ","suffix":".For example, you could run your"}]}]}
>```
>%%
>*%%PREFIX%%terms of simulation execution.%%HIGHLIGHT%% ==You can run your simulation until there are no more events,until a certain simulation time is reached, or until a certain event is triggered. You can also step through the simulationevent by event. Furthermore, you can mix these things as you like== %%POSTFIX%%.For example, you could run your*
>%%LINK%%[[#^9mb2teb7lon|show annotation]]
>%%COMMENT%%
>运行仿真；
>
>- 直到没有 events；
>- 直到一个确定的仿真时间；
>- 直到一个特定的事件被触发；
>
>%%TAGS%%
>
^9mb2teb7lon


>%%
>```annotation-json
>{"created":"2024-09-01T07:16:13.675Z","text":"environment.run 方法：\n\n- 没有参数的情况下：一步步执行仿真直到没有事件；\n- 加一个过期时间。","updated":"2024-09-01T07:16:13.675Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":24532,"end":24583},{"type":"TextQuoteSelector","exact":"The most important method here is Environment.run()","prefix":"ur processeshave all terminated.","suffix":":• If you call it without any ar"}]}]}
>```
>%%
>*%%PREFIX%%ur processeshave all terminated.%%HIGHLIGHT%% ==The most important method here is Environment.run()== %%POSTFIX%%:• If you call it without any ar*
>%%LINK%%[[#^2gnndd9dem3|show annotation]]
>%%COMMENT%%
>environment.run 方法：
>
>- 没有参数的情况下：一步步执行仿真直到没有事件；
>- 加一个过期时间。
>%%TAGS%%
>
^2gnndd9dem3


>%%
>```annotation-json
>{"created":"2024-09-01T07:30:42.717Z","text":"为了逐个事件地逐步完成模拟，environment 提供了：\n\n- peek()\n- step()","updated":"2024-09-01T07:30:42.717Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":26178,"end":26264},{"type":"TextQuoteSelector","exact":"To step through the simulation event by event, the environment offers peek() and step(","prefix":"c)'Monty Python’s Flying Circus'","suffix":").peek() returns the time of the"}]}]}
>```
>%%
>*%%PREFIX%%c)'Monty Python’s Flying Circus'%%HIGHLIGHT%% ==To step through the simulation event by event, the environment offers peek() and step(== %%POSTFIX%%).peek() returns the time of the*
>%%LINK%%[[#^25wehh824mz|show annotation]]
>%%COMMENT%%
>为了逐个事件地逐步完成模拟，environment 提供了：
>
>- peek()
>- step()
>%%TAGS%%
>
^25wehh824mz


>%%
>```annotation-json
>{"created":"2024-09-01T07:34:45.711Z","text":"- 获取当前仿真时间：Environment.now 属性；\n- 获取当前活跃（active）的 process：Environment.active_process","updated":"2024-09-01T07:34:45.711Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":26595,"end":26607},{"type":"TextQuoteSelector","exact":"State access","prefix":".peek() < until:env.step()3.2.2 ","suffix":"The environment allows you to ge"}]}]}
>```
>%%
>*%%PREFIX%%.peek() < until:env.step()3.2.2%%HIGHLIGHT%% ==State access== %%POSTFIX%%The environment allows you to ge*
>%%LINK%%[[#^djaz3bmu62|show annotation]]
>%%COMMENT%%
>- 获取当前仿真时间：Environment.now 属性；
>- 获取当前活跃（active）的 process：Environment.active_process
>%%TAGS%%
>
^djaz3bmu62


>%%
>```annotation-json
>{"created":"2024-09-01T07:40:56.472Z","text":"创建事件：\n\n- Environment.event();","updated":"2024-09-01T07:40:56.472Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":28176,"end":28190},{"type":"TextQuoteSelector","exact":"Event creation","prefix":"cumentation, Release 4.0.03.2.3 ","suffix":"To create events, you normally h"}]}]}
>```
>%%
>*%%PREFIX%%cumentation, Release 4.0.03.2.3%%HIGHLIGHT%% ==Event creation== %%POSTFIX%%To create events, you normally h*
>%%LINK%%[[#^r2sslbmpfee|show annotation]]
>%%COMMENT%%
>创建事件：
>
>- Environment.event();
>%%TAGS%%
>
^r2sslbmpfee


>%%
>```annotation-json
>{"created":"2024-09-01T13:18:28.825Z","text":"给一个事件增加回调：\n\n- 最常见的方法是从你的 process 函数中生成。","updated":"2024-09-01T13:18:28.825Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":30798,"end":30826},{"type":"TextQuoteSelector","exact":"Adding callbacks to an event","prefix":"the event (value = yield event).","suffix":"“What? Callbacks? I’ve never see"}]}]}
>```
>%%
>*%%PREFIX%%the event (value = yield event).%%HIGHLIGHT%% ==Adding callbacks to an event== %%POSTFIX%%“What? Callbacks? I’ve never see*
>%%LINK%%[[#^7eg3b7uu0ka|show annotation]]
>%%COMMENT%%
>给一个事件增加回调：
>
>- 最常见的方法是从你的 process 函数中生成。
>%%TAGS%%
>
^7eg3b7uu0ka


>%%
>```annotation-json
>{"created":"2024-09-01T13:52:09.387Z","text":"当 event 被触发时，他们不是成功就是失败：\n\n- 触发事件并标记它为成功，使用 Event.succeed；\n- 触发事件并标记它为失败，使用 Event.fail；\n- 还有一种更通用的方式，使用 Event.trigger。","updated":"2024-09-01T13:52:09.387Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":32044,"end":32103},{"type":"TextQuoteSelector","exact":"When events are triggered, they can either succeed or fail.","prefix":", Release 4.0.0Triggering events","suffix":" For example, if an event is to "}]}]}
>```
>%%
>*%%PREFIX%%, Release 4.0.0Triggering events%%HIGHLIGHT%% ==When events are triggered, they can either succeed or fail.== %%POSTFIX%%For example, if an event is to*
>%%LINK%%[[#^hyw8zuroa2|show annotation]]
>%%COMMENT%%
>当 event 被触发时，他们不是成功就是失败：
>
>- 触发事件并标记它为成功，使用 Event.succeed；
>- 触发事件并标记它为失败，使用 Event.fail；
>- 还有一种更通用的方式，使用 Event.trigger。
>%%TAGS%%
>
^hyw8zuroa2


>%%
>```annotation-json
>{"created":"2024-09-01T13:56:34.572Z","text":"jə-ˈner-ik 通用","updated":"2024-09-01T13:56:34.572Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":32643,"end":32651},{"type":"TextQuoteSelector","exact":"generic ","prefix":"ed computation).There is also a ","suffix":"way to trigger an event: Event.t"}]}]}
>```
>%%
>*%%PREFIX%%ed computation).There is also a%%HIGHLIGHT%% ==generic== %%POSTFIX%%way to trigger an event: Event.t*
>%%LINK%%[[#^pvsktj1efe9|show annotation]]
>%%COMMENT%%
>jə-ˈner-ik 通用
>%%TAGS%%
>
^pvsktj1efe9


>%%
>```annotation-json
>{"created":"2024-09-01T13:57:30.839Z","text":"大纲","updated":"2024-09-01T13:57:30.839Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":32955,"end":32964},{"type":"TextQuoteSelector","exact":"outlined ","prefix":"s for EventThe simple mechanics ","suffix":"above provide a great flexibilit"}]}]}
>```
>%%
>*%%PREFIX%%s for EventThe simple mechanics%%HIGHLIGHT%% ==outlined== %%POSTFIX%%above provide a great flexibilit*
>%%LINK%%[[#^iq3sh119fck|show annotation]]
>%%COMMENT%%
>大纲
>%%TAGS%%
>
^iq3sh119fck


>%%
>```annotation-json
>{"created":"2024-09-01T14:24:43.765Z","text":"开始一个 process 函数包行两件事：\n\n- 必须调用 process 函数，其目的是创建一个 generator 对象；\n- 随后创建一个 process 的实例，并传递 Environment 和 generator 对象给它。","updated":"2024-09-01T14:24:43.765Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":22361,"end":22408},{"type":"TextQuoteSelector","exact":"Starting a process function involves two things","prefix":"ot when creating everythingelse.","suffix":":1. You have to call the process"}]}]}
>```
>%%
>*%%PREFIX%%ot when creating everythingelse.%%HIGHLIGHT%% ==Starting a process function involves two things== %%POSTFIX%%:1. You have to call the process*
>%%LINK%%[[#^qnjd7giko9m|show annotation]]
>%%COMMENT%%
>开始一个 process 函数包行两件事：
>
>- 必须调用 process 函数，其目的是创建一个 generator 对象；
>- 随后创建一个 process 的实例，并传递 Environment 和 generator 对象给它。
>%%TAGS%%
>
^qnjd7giko9m


>%%
>```annotation-json
>{"created":"2024-09-01T14:36:09.976Z","text":"不太理解","updated":"2024-09-01T14:36:09.976Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":33324,"end":33388},{"type":"TextQuoteSelector","exact":"self.pupil_procs = [env.process(self.pupil()) for i in range(3)]","prefix":"elf.class_ends = env.event()... ","suffix":"... self.bell_proc = env.process"}]}]}
>```
>%%
>*%%PREFIX%%elf.class_ends = env.event()...%%HIGHLIGHT%% ==self.pupil_procs = [env.process(self.pupil()) for i in range(3)]== %%POSTFIX%%... self.bell_proc = env.process*
>%%LINK%%[[#^ggqdl7o21a7|show annotation]]
>%%COMMENT%%
>不太理解
>%%TAGS%%
>#问题
^ggqdl7o21a7


>%%
>```annotation-json
>{"created":"2024-09-01T14:37:40.889Z","text":"- 事件可以共享；\n- 事件可以被一个 process 创建；\n- 事件可以被 process 的上下文的外面创建；\n- 事件可以被传递给其他 process；","updated":"2024-09-01T14:37:40.889Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":33051,"end":33223},{"type":"TextQuoteSelector","exact":"One example for this is that events can be shared. They can be created by a process or outside of the context of aprocess. They can be passed to other processes and chained","prefix":"en the basic Event) can be used.","suffix":":>>> class School:... def __init"}]}]}
>```
>%%
>*%%PREFIX%%en the basic Event) can be used.%%HIGHLIGHT%% ==One example for this is that events can be shared. They can be created by a process or outside of the context of aprocess. They can be passed to other processes and chained== %%POSTFIX%%:>>> class School:... def __init*
>%%LINK%%[[#^aq2ig9m7mo5|show annotation]]
>%%COMMENT%%
>- 事件可以共享；
>- 事件可以被一个 process 创建；
>- 事件可以被 process 的上下文的外面创建；
>- 事件可以被传递给其他 process；
>%%TAGS%%
>
^aq2ig9m7mo5


>%%
>```annotation-json
>{"created":"2024-09-01T14:57:57.380Z","text":"event.run 函数：\n\n除了传递数字，还可以传递任何事件给它","updated":"2024-09-01T14:57:57.380Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":25530,"end":25659},{"type":"TextQuoteSelector","exact":"Instead of passing a number to run(), you can also pass any event to it. run() will then return when the eventhas been processed.","prefix":"(until=i)progressbar.update(i)• ","suffix":"Assuming that the current time i"}]}]}
>```
>%%
>*%%PREFIX%%(until=i)progressbar.update(i)•%%HIGHLIGHT%% ==Instead of passing a number to run(), you can also pass any event to it. run() will then return when the eventhas been processed.== %%POSTFIX%%Assuming that the current time i*
>%%LINK%%[[#^0aac7n8xuo6m|show annotation]]
>%%COMMENT%%
>event.run 函数：
>
>除了传递数字，还可以传递任何事件给它
>%%TAGS%%
>
^0aac7n8xuo6m


>%%
>```annotation-json
>{"created":"2024-09-01T15:03:48.195Z","text":"- Timeout 也是一个事件；\n- Timeout 有两个参数，一个是 delay，一个是可选参数 value；\n- 触发时机：过期。","updated":"2024-09-01T15:03:48.195Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":33923,"end":33930},{"type":"TextQuoteSelector","exact":"Timeout","prefix":"ngs.3.3.3 Let time pass by: the ","suffix":"To actually let time pass in a s"}]}]}
>```
>%%
>*%%PREFIX%%ngs.3.3.3 Let time pass by: the%%HIGHLIGHT%% ==Timeout== %%POSTFIX%%To actually let time pass in a s*
>%%LINK%%[[#^5v135hlb9l6|show annotation]]
>%%COMMENT%%
>- Timeout 也是一个事件；
>- Timeout 有两个参数，一个是 delay，一个是可选参数 value；
>- 触发时机：过期。
>%%TAGS%%
>
^5v135hlb9l6


>%%
>```annotation-json
>{"created":"2024-09-01T15:05:51.887Z","text":"过程也是事件","updated":"2024-09-01T15:05:51.887Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":34458,"end":34483},{"type":"TextQuoteSelector","exact":"Processes are events, too","prefix":"s comparison and addition.3.3.4 ","suffix":"SimPy processes (as created by P"}]}]}
>```
>%%
>*%%PREFIX%%s comparison and addition.3.3.4%%HIGHLIGHT%% ==Processes are events, too== %%POSTFIX%%SimPy processes (as created by P*
>%%LINK%%[[#^fz05fwtumsj|show annotation]]
>%%COMMENT%%
>过程也是事件
>%%TAGS%%
>
^fz05fwtumsj


>%%
>```annotation-json
>{"created":"2024-09-02T13:48:58.565Z","text":"- 一个 process 可以生产另外一个 process；\n- 当其他 process 结束时，它会被恢复；\n- 事件的返回的值将会是那个 process 的返回值，这里的 that process 应该是 sub(env)。\n","updated":"2024-09-02T13:48:58.565Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":34584,"end":34748},{"type":"TextQuoteSelector","exact":"That means, that a process can yield another process. It will then be resumed when the other process ends. The event’svalue will be the return value of that process","prefix":"e property of being events, too.","suffix":":>>> def sub(env):... yield env."}]}]}
>```
>%%
>*%%PREFIX%%e property of being events, too.%%HIGHLIGHT%% ==That means, that a process can yield another process. It will then be resumed when the other process ends. The event’svalue will be the return value of that process== %%POSTFIX%%:>>> def sub(env):... yield env.*
>%%LINK%%[[#^wx1m7zeocdd|show annotation]]
>%%COMMENT%%
>- 一个 process 可以生产另外一个 process；
>- 当其他 process 结束时，它会被恢复；
>- 事件的返回的值将会是那个 process 的返回值，这里的 that process 应该是 sub(env)。
>
>%%TAGS%%
>
^wx1m7zeocdd


>%%
>```annotation-json
>{"created":"2024-09-02T13:59:41.056Z","text":"simpy.util.start_delayed() 函数的使用场景：\n\n- 定时启动一个 process（进程）","updated":"2024-09-02T13:59:41.056Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":35095,"end":35211},{"type":"TextQuoteSelector","exact":"If you don’t want a process to start immediately but after a certain delay, you can use simpy.util.start_delayed(). ","prefix":"to deal with this type of event.","suffix":"This method returns a helper pro"}]}]}
>```
>%%
>*%%PREFIX%%to deal with this type of event.%%HIGHLIGHT%% ==If you don’t want a process to start immediately but after a certain delay, you can use simpy.util.start_delayed().== %%POSTFIX%%This method returns a helper pro*
>%%LINK%%[[#^go6fquzj91e|show annotation]]
>%%COMMENT%%
>simpy.util.start_delayed() 函数的使用场景：
>
>- 定时启动一个 process（进程）
>%%TAGS%%
>
^go6fquzj91e


>%%
>```annotation-json
>{"created":"2024-09-02T14:19:48.449Z","text":"多事件使用场景：\n\n- 你想要等一个资源，但是没有限制时间；\n- 或者你想等直到一个事件的集合都发生了。\n\n---\n\nAnyof 和 Allof 都把一个事件的 list 作为参数，并且当 list  中的任意一个或 list  中所有的事件都被触发时会被触发。","updated":"2024-09-02T14:19:48.449Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":35693,"end":35728},{"type":"TextQuoteSelector","exact":"Waiting for multiple events at once","prefix":"ed for the helper process.3.3.5 ","suffix":"Sometimes, you want to wait for "}]}]}
>```
>%%
>*%%PREFIX%%ed for the helper process.3.3.5%%HIGHLIGHT%% ==Waiting for multiple events at once== %%POSTFIX%%Sometimes, you want to wait for*
>%%LINK%%[[#^enaqivwbdkn|show annotation]]
>%%COMMENT%%
>多事件使用场景：
>
>- 你想要等一个资源，但是没有限制时间；
>- 或者你想等直到一个事件的集合都发生了。
>
>---
>
>Anyof 和 Allof 都把一个事件的 list 作为参数，并且当 list  中的任意一个或 list  中所有的事件都被触发时会被触发。
>%%TAGS%%
>
^enaqivwbdkn


>%%
>```annotation-json
>{"created":"2024-09-02T14:28:50.719Z","text":"条目，Condition 事件的值是一个有序字典，其中包含每个触发事件的条目","updated":"2024-09-02T14:28:50.719Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":36500,"end":36506},{"type":"TextQuoteSelector","exact":"entry ","prefix":"s an ordered dictionary with an ","suffix":"for every triggered event. In th"}]}]}
>```
>%%
>*%%PREFIX%%s an ordered dictionary with an%%HIGHLIGHT%% ==entry== %%POSTFIX%%for every triggered event. In th*
>%%LINK%%[[#^xnmmguv9g3b|show annotation]]
>%%COMMENT%%
>条目，Condition 事件的值是一个有序字典，其中包含每个触发事件的条目
>%%TAGS%%
>
^xnmmguv9g3b


>%%
>```annotation-json
>{"created":"2024-09-05T14:38:52.798Z","text":"前两项已在 活动指南 中介绍，但为了完整起见，我们还将在此处包含它们","updated":"2024-09-05T14:38:52.798Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":38147,"end":38271},{"type":"TextQuoteSelector","exact":"The first two items were already covered in the Events guide, but we’ll also include them here for the sake of com-pleteness","prefix":"te• Interrupting another process","suffix":".Another possibility for process"}]}]}
>```
>%%
>*%%PREFIX%%te• Interrupting another process%%HIGHLIGHT%% ==The first two items were already covered in the Events guide, but we’ll also include them here for the sake of com-pleteness== %%POSTFIX%%.Another possibility for process*
>%%LINK%%[[#^dhhbywkrclo|show annotation]]
>%%COMMENT%%
>前两项已在 活动指南 中介绍，但为了完整起见，我们还将在此处包含它们
>%%TAGS%%
>
^dhhbywkrclo


>%%
>```annotation-json
>{"created":"2024-09-05T14:43:51.395Z","text":"当车辆行驶时，控制器可以是被动的，但一旦车辆连接到电网，就需要重新激活才能为电池充电","updated":"2024-09-05T14:43:51.395Z","document":{"title":"SimPy Documentation","link":[{"href":"urn:x-pdf:03a4d120c201d42da3f9f2a754f71c5c"},{"href":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf"}],"documentFingerprint":"03a4d120c201d42da3f9f2a754f71c5c"},"uri":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","target":[{"source":"vault:/PDF/simpy-readthedocs-io-en-4.0.0.pdf","selector":[{"type":"TextPositionSelector","start":38554,"end":38717},{"type":"TextQuoteSelector","exact":"While the vehicle isdriving, the controller can be passive but needs to be reactivate once the vehicle is connected to the power grid in orderto charge the battery","prefix":"nt battery-charging controller. ","suffix":".In SimPy 2, this pattern was kn"}]}]}
>```
>%%
>*%%PREFIX%%nt battery-charging controller.%%HIGHLIGHT%% ==While the vehicle isdriving, the controller can be passive but needs to be reactivate once the vehicle is connected to the power grid in orderto charge the battery== %%POSTFIX%%.In SimPy 2, this pattern was kn*
>%%LINK%%[[#^nll8gn3jdyh|show annotation]]
>%%COMMENT%%
>当车辆行驶时，控制器可以是被动的，但一旦车辆连接到电网，就需要重新激活才能为电池充电
>%%TAGS%%
>
^nll8gn3jdyh
