爬取数据之前首先需要清楚自己需要什么数据、这些数据在哪些页面上、得到这些数据分几步走（得到所有数据需要跳转几个页面、跳转每个页面需要先得到什么信息、跳转的页面可以得到什么信息），然后需要分析每个页面url的规律以便之后重复使用。

##### 环境：Anaconda Notebook Python3.0 
##### 用到的包：Requests、BeautifulSoup、Selenium、Pandas等（需要先安装包的请先找相关教程安装，其中Selenium Webdriver要注意与Chrome浏览器的版本相适应）
##### Chromedriver下载：http://chromedriver.storage.googleapis.com/index.html

##### Booking主要爬取某一城市的酒店名称、酒店评分、评分等级、评论人数以及评论区的用户国籍；
##### tripadvisor爬取了某一城市的景点名称、景点类型、景点评分、评论人数以及评论区的语言类型；
##### tripadvisor还爬取了某一城市的餐厅名称、餐厅评分、评论人数以及评论区的语言类型。
所有代码均可以直接在Notebook中运行，数据均已excel表格形式存储

这里主要以缤客、猫途鹰为例（Booking、TripAdvisor中文官网，因为发现外网和中文官网数据一致才决定使用中文官网，若需爬取其他外文网站首先需要清楚中文官网与外网上的数据的区别，是否符合要求的数据）

## Booking（缤客）
#### Booking爬取数据的挑战主要在于找到页面url的规律，精简页面的url；找到评论的url（评论单独作为一个文件在network的reviewlist里）
#### Booking前两个页面其实不需要headers，固定headers爬取数据可能会被发现，但reviewlist必须有headers！
主要分三步进行爬取。
第一步：爬取某一个城市酒店页面左侧住宿类型以及url，因为直接爬取全部酒店，booking隐藏了部分数据，爬不到完整的数据，所以按住宿类型爬取酒店名称和url内容能够爬取到全部的酒店信息，该代码写在‘1-城市（住宿类型、酒店名称、酒店link）.ipynb’，一页25条数据；
第二步：找到酒店详情页面的规律，把第一步保存的link清洗掉其中无用的部分，进行拼接爬取酒店评分、评分等级和评论人数；
第三步：找到network中的reviewlist，一页10条评论，爬取评论页面数据
#### 只要是Booking中这三个页面的数据都能爬到，代码只展示了一小部分

## TripAdvisor（猫途鹰）
#### tripadvisor的挑战在于评论数据用了Ajax，url不变，在network里也找不到相应的文件包含可跳转的url，所以用了selenium webdriver模拟点击
同样三步走：
第一步：爬取全部的景点/餐厅数据
第二步：爬取景点/餐厅评分、评论人数
第三步：评论区的语言类型

#### 写到这我特别想吐槽tripadvisor的前端！
首先值得肯定的是这个网站反爬虫机制做的不错，用Ajax渲染前端，但是前端样式写的也太混乱了，解决了Ajax没想到栽倒在前端样式上，同一个城市的景点详情页面排版不一样、排版一样的页面某一部分用的css名称不一样（比如评论版块的语言类型那里），同一个样式光名称分了至少四组！明明都是同样的样式内容……还有class-name太冗长，前端写的很不规范，感觉是好几个人写的，如果是多人协作负责前端应该内部有统一的前端标准吧？（这应该不是为了反爬虫吧），建议该网站的前端人员先找到BAT的前端标准通读一遍，说实话，学生项目的前端写的都比这规范。

### 一点感想：
爬虫初级者因为项目所需写的代码，可能代码还不够精简高效，但还是可以使用的。编程带来的快乐在于不停地实践，始终在学习的路上，写代码虽然累但会上瘾的，每次做完项目都暗下决心再也不碰搞技术这活儿，感觉要把人耗空，但还是不长记性，对下一次编程跃跃欲试，包揽了小组里所有需要编程技术的活……不要恐惧编程或者任何其他尚未涉猎的领域，只有勇敢迈出这一步，面对的未知领域才有机会变成自己熟悉的世界，一切恐惧都来源于无知与自我恐吓。
