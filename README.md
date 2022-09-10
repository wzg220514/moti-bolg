## 注意
你需要修改的地方：
- qqconnectconfig.properties
- com.moti.config.ElasticSearchConfig
- com.moti.config.GiteeImgBedConfig
- resources/application.yml

## 前言
哈喽大家好，我是莫提。最近新写了一个非常简约的个人博客系统。用了差不多快一个月吧（中间肯定有划水摸鱼的时间，哈哈）。这次的项目用了几个我之前没有用过的技术，也成功结合并实现了我的一些想法。个人觉得也是非常适合于初学者学习！
## 主要功能
### 文章方面

首先既然是个人博客系统，肯定要对写文章有一个非常友好的支持！不然感觉只好看不实用也是扯淡。不得不说现在使用`MarkDown`写文章的人是越来越来。哈哈，这篇文章其实也是用`MarkDown`写的！

![](https://imgkr2.cn-bj.ufileos.com/f2d647ad-2caa-494b-9968-e645e4d08dc1.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=XX0gxbImrdIDhOQy4ai7WGRQn6k%253D&Expires=1603279904)

在写文章方面，我开发的个人博客同样支持`MarkDown`的语法，使用的是目前一个比较好用的编辑器叫`EditMd`。

![](https://imgkr2.cn-bj.ufileos.com/bea87d5d-400a-4a35-ae68-d042be666b9e.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=aHQ0HVRAE4BvwmJcrl517PTL1II%253D&Expires=1603280400)

在这个系统里面写的文章，把原文复制一下，就可以在任何支持MarkDown的文章轻松的发表，不需要改任何格式，也**不需要重新上传图片**。为什么嘞？因为我直接使用了码云当做我这个项目的**图床**（对外提供图片链接，通过链接就可以访问到这张图片）。这样如果之后再开发一个备份的功能就非常方便了！

为了更加友好的写博客，我自己还新增了从剪切板复制图片到输入框实现图片的粘贴上传。哈哈，我觉这个功能是很多个人开发的博客系统不具备的。

之后我还开发了一些作为博客系统必须具备的功能，比如编辑、存草稿、回收站、文集（文章分类）、标签、文章归档等等。这些功能其实和一般的博客系统都差不多，没啥好说的。

关于**文章评论**，读者看到后填写基本的信息之后就可以发表评论了。

![](https://imgkr2.cn-bj.ufileos.com/48cae64e-c88e-433e-9731-260574118dbe.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=DVQkQ2WE3StT9Y%252Fq5jl8WEGDDqo%253D&Expires=1603281181)

后台可以对评论进行管理，比如查看、删除、回复这些，回复的时候可以选择是否向用户填写的邮箱发送回复邮件，及时通知留言者。

评论管理

![](https://imgkr2.cn-bj.ufileos.com/5cc2f4e0-9ca6-4aef-af61-33b5633dd62b.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=N%252B%252B852plSKLOkA2qU3TuVxkVQn4%253D&Expires=1603281230)

查看与回复

![](https://imgkr2.cn-bj.ufileos.com/7d465294-9be6-4ad8-872d-39ddb32c4f9a.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=kXaS8u9FNsBq8YfxutGZ%252FKbAwrk%253D&Expires=1603281333)

发送邮件内容

![](https://imgkr2.cn-bj.ufileos.com/8a260bae-0194-4710-920a-4f1f7f461f7c.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=CC%252B5KrslPRhgVtzgGlDrOYMwZA8%253D&Expires=1603281361)

在前提主页有一个站内搜索，访客可以在这里根据关键词搜索文章！之后的搜索结果也会高亮显示！这里用到了ElasticSearch搜索引擎，配置了好用的IK分词器之后搜索的结果会更加的准确！

![](https://imgkr2.cn-bj.ufileos.com/94c15b10-d4eb-4348-bc9a-e356e4e5007a.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=B3F7%252BpMHQ10ZdRCu6CUKgLGlGxo%253D&Expires=1603281663)

![](https://imgkr2.cn-bj.ufileos.com/6632dedd-659c-413e-8906-9ac6d8914302.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=Y25pM9X36u0%252BipAKQrCbt5VGkCY%253D&Expires=1603281747)

### 用户方面

首先是登录，设计了两种登录方式，一个是用户名和密码，一个是QQ登录。诶？有的人可能很奇怪了，这怎么能用QQ登录呢？其实这个应该叫做绑定QQ，如果之前数据库里面没有QQ用户的信息，那么第一次登录的时候就将这个QQ的信息写到数据库实现绑定的功能，这应该叫**先入为主**。

![](https://imgkr2.cn-bj.ufileos.com/72f5101f-1366-4c15-9945-7ef4d42a1cd9.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=02HDQIkYEqE5R%252Fomxsak2iNE2ck%253D&Expires=1603282050)

之后用户可以修改个人资料，直接上图吧~

![](https://imgkr2.cn-bj.ufileos.com/12fd5bef-fb3c-44ee-904d-73ee4a9a528d.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=s0zHghzMIoPNkVaMnz5uBz4%252BClM%253D&Expires=1603282289)

上传完微信二维码和公众号二维码，之后可以在前台主页进行显示。

![](https://imgkr2.cn-bj.ufileos.com/0b39ac41-ffae-469e-99c0-8592b456d4e7.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=365YHY%252Fy2qtr1UHxINS4eeys9fw%253D&Expires=1603282357)

### 定时统计
项目中引入了Redis，我们就可以方便进行统计了，比如文章的阅读量，我只是简单的设计了刷新一次页面就算一次阅读。在没有引入Redis之前我是每次刷新，就更新数据库！**非常不推荐！**
现在我们就把今天的阅读量放到Redis中，然后写一个定时任务，把Redis中的数据写到数据库，这绝对算是一种优化吧~

![](https://imgkr2.cn-bj.ufileos.com/13ecaf0a-e963-469b-8f5c-17eeed3f8d5a.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=MJ%252F7FhdH2BLaWfovvpsT0HYP97g%253D&Expires=1603282741)

定时任务

![](https://imgkr2.cn-bj.ufileos.com/353cb6b5-3cfd-4fd9-89dd-b4f5e766762f.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=kDcIV8wM4GFKxv1C6fsV8Fgrp0U%253D&Expires=1603282842)

同样的原理，我们需要统计访客信息，统计访客的阅读记录与阅读次数（其实就是后台的访问与访客）。我们需要记录访客的IP地址和访问的文章以及阅读次数等等。其实这里我想把访客统计做的更加细致，能根据IP获取到地址的那种，但是找了几个免费的API，淘宝就有一个，能用是能用，但是访问的次数多了就获取不到数据了，哎，后来我就把这个功能删掉了，做成了现在比较简单的版本。

![](https://imgkr2.cn-bj.ufileos.com/e6104de5-3348-4f82-879f-8610c2e0c637.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=lU00gGoTw%252FiTO9W3I09k1zpB5LA%253D&Expires=1603283095)

### 站点装扮
这里就比较简单了，直接上图~

![](https://imgkr2.cn-bj.ufileos.com/1de98104-403d-4b9f-9035-66982c3a7801.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=f8GO%252FfIHmEYN5fsxk4t7DRPk7ac%253D&Expires=1603283176)

### 主页部件

这个前台主页我是想做的既美观又实用，额，只能做成这样了，来个效果。

![](https://imgkr2.cn-bj.ufileos.com/b4949d9b-88ed-42fe-9a9e-9e3b97ce0278.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=pV0j9LTBi7YGF%252FtiitN%252FA3OkWKM%253D&Expires=1603280787)

侧边开发了公告、本地天气、站内搜索、热门文章、标签云、文集、文章归档、友情链接、访客统计等。

阅读文章页面时长这样的

![](https://imgkr2.cn-bj.ufileos.com/a617c3ed-64af-40a9-81ca-dc96e0eb8c43.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=0h6IFKDrJJntG2gGI9CUOx53cMg%253D&Expires=1603283448)

## 技术栈
主要功能上面已经说得差不多了，现在来讲讲这个项目用到了哪些技术。

### 前端

|  名称   |   技术点  |
| --- | --- |
|  基础   |  Html、Css、JavaScript、Jquery   |
|  UI框架   |  BootStrap  |
|  文本编辑器   |   EditMd  |
|  前台模板   |  Olympus   |
|  后台模板   |  Pike Admin   |


前台模板和后台模板我都已经上传到了我的QQ交流群。喜欢的可以去下载一波~

![](https://imgkr2.cn-bj.ufileos.com/c754ce6c-f957-4e2e-9b8e-3b929cb6e265.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=eFBYGbrXf2gV%252FJpf99uQGQJHMkE%253D&Expires=1603283852)

![](https://imgkr2.cn-bj.ufileos.com/2b53f4fd-2b12-47cf-a131-4438f28a186b.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=z0Mb3zxyPAAQqi6QheFvP3HXZ2M%253D&Expires=1603283810)

### 后端

|  名称   |   技术点  |
| --- | --- |
|  开发   |  SpringBoot、MyBatis   |
|  数据库   |  MySQL 5.7 + Druid  |
|  缓存   |   Redis + EhCache  |
|  消息队列   |  RabbitMq   |
|  搜索引擎   |  ElasticSearch   |
|  其他   |   邮件任务、定时任务、QQ登录、Lombok、Jrebel、码云API  |

### 项目难点

项目使用到了ElasticSearch搜索引擎，后台在对文章进行修改、删除时更新数据库的同时需要更新ElasticSearch，如果使用串 行修改会很影响效率。难点在于在不影响系统性能的情况下保证MySQL与ES的数据一致性。 

### 解决

编写定时任务每天0点对ES进行数据重建，在文章做出更新后使用RabbitMq消息队列推送更新/删除的消息，分析场景最后我 使用了RabbitMq的Topic模型。编写更新消费者和删除消费者，使用同一个交换机，匹配不同的key对消息进行消费，实现对 ES中的数据进行同步。

## 结语
最后最后，决定把此项目开源！附上项目的Github地址😊。喜欢的话一定别忘了给我颗⭐。

> 






