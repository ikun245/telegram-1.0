# telegram监听1.0（开发中）
电报（telegram）监听，采用协议号（session+json）模式转发采集难以进入的群聊的消息并收集，再利用机器人安全稳定的api特点，将监听的消息转发出去

#
众所周知，在telegram中存在着一种机器人，监听机器人，他们的主要功能是在群中捕捉到发送关键词的用户名和关键词，并将消息转发的指定群聊里为各种行业提供精准的客源，通常一个月的价格为30u-60u不等，质量也参差不齐，部分价格低廉且过滤功能极差的机器人还会限制关键词的个数和采集的群聊个数，更有部分监听机器人并不是去那些真正活跃的搜索群或者指定群聊，而是自己仿造，口口声声喊着上千个群聊，却不展示真实实力，这种监听暂且不说实力如何，坑用户肯定是第一名的，贵的也不一定会带来什么特别大的效益
#
经过长时间的探索，我们发现，业内人士，都是通过使用个人账号将消息转发出来，然后再用机器人去转发到另一个群聊，这样的办法是解决了机器人无法进入指定群聊的问题（ps：普通群组和超级群组想要使用机器人要么使用邀请链接要么管理员拉），但是有一个仍有一个缺点。就是转发消息未免太过繁琐，而且难以控制广告的检测，大部分群聊里广告都是数以千计
#
那么我们可以省去这个转发，给他转移到其他地方，哪怕不是实时的（个人认为，没有监听是实时的，消息都是有滞后性的），差个半小时，甚至一小时，只要咱们可以躲避telegram的风控和绕开监听转发机器人的限制，那么这套方案就可以应运而生，我们已知，协议号的存在（session+json）的存在，可以应用于Telegram Expert（dbzj.pro）,以及telegram Gods，还有其他国产的电报辅助工具上，本质上是官方公开了接口，可以让咱们使用，通过查看Telegram Expert的参数生成器不难发现，专家模式下的参数生成器包括了app id和app hash，也就是说我们可以以一种不可视的方法去控制账号，但是要像一个真正的设备，就像高级爬虫一样，我像一个正常用户去登录获取数据，简单点形容就是我挂了一个cooike在身上，在简单点就是我套了一层皮
#
以下如果不会操作可以观看Telegram Expert所举的方法https://www.youtube.com/watch?v=yugIBRYUcTY
首先如何去模仿真实用户呢，就像现在这样，我怎么知道你是不是个真人？你拿着手机（OPPO，MI，Vivo，HUAWEI，IPhone），电脑(Windows,Mac)，他都是一个设备，有名字有身份，
在github上就有https://github.com/androidtrackers/certified-android-devices
该地址呢包含了大量的Android的标识名称
然后呢我们需要的还有app id和app hash，哪里去找呢，这里Telegram Expert的官方人员暖心的给你收集了，直达：https://blb.team/threads/app-hash-id-oficialnyx-klientov.294
安卓的历史版本： https://en.wikipedia.org/wiki/Android_version_history
各个国家地区所对应的语言：https://saimana.com/list-of-country-locale-code/
安卓的telegram对应的版本信息：https://ww.apkmirror.com/?post_type-app_release&searchtype-apk&s-
到这一步，我们基本就能解决怎么模仿真实用户去通过协议的方式登录Telegram，接下来编码并进行操作，本文将全程使用Python开发，文章作者还还在上大学，且对Python掌握不足，难免会有缺点，还请支出——————2024.12.05
