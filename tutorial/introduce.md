# Athena 简介

!> 鉴于该自动检测扫描框架的特殊功能，为加强 `Athena` 漏洞监控框架​的合法使用与管理，特郑重声明如下
   

    一、Athena 漏洞监控框架，仅限用于经过合法授权的在 Athena 漏洞监控框架上进行检测的信息系统，任何人均不得擅自将其用于任何其他非经合法授权的信息系统。
    
    二、任何擅自使用 Athena 漏洞监控框架对未经合法授权的信息系统进行检测的，均为非法和侵权行为，一切法律后果均由侵权人承担。
    
    三、请勿以SRC平台做挡箭牌使用本工具刷SRC，当平台与法律对立的时候，请牢记执法部门不是SRC平台。参见 刑法285，286，287，287之一，之二
    
    四、本工具适用于企业和个人对自身网站安全进行检查，禁止使用本工具进行任何对其他网站产生影响的行为。
    
    五、请您熟读网络安全法，因您个人的行为触犯法律，本工具开发者不负任何责任。
    
    六、参考 <袁炜 世纪佳缘>、<李培 银川 为家乡做贡献>，请勿以身正不怕影子斜为由进行网络攻击。

!> 法律声明

    刑法第二百八十五条 非法侵入计算机信息系统罪 违反国家规定，侵入国家事务、国防建设、尖端科学技术领域的计算机信息系统的，处三年以下有期徒刑或者拘役。 违反国家规定，侵入前款规定以外的计算机信息系统或者采用其他技术手段，获取该计算机信息系统中存储、处理或者传输的数据，或者对该计算机信息系统实施非法控制，情节严重的，处三年以下有期徒刑或者拘役，并处或者单处罚金；情节特别严重的，处三年以上七年以下有期徒刑，并处罚金。 提供专门用于侵入、非法控制计算机信息系统的程序、工具，或者明知他人实施侵入、非法控制计算机信息系统的违法犯罪行为而为其提供程序、工具，情节严重的，依照前款的规定处罚。 单位犯前三款罪的，对单位判处罚金，并对其直接负责的主管人员和其他直接责任人员，依照各该款的规定处罚。
    
    刑法第二百八十六条 破坏计算机信息系统罪 违反国家规定，对计算机信息系统功能进行删除、修改、增加、干扰，造成计算机信息系统不能正常运行，后果严重的，处五年以下有期徒刑或者拘役；后果特别严重的，处五年以上有期徒刑。 违反国家规定，对计算机信息系统中存储、处理或者传输的数据和应用程序进行删除、修改、增加的操作，后果严重的，依照前款的规定处罚。 故意制作、传播计算机病毒等破坏性程序，影响计算机系统正常运行，后果严重的，依照第一款的规定处罚。 单位犯前三款罪的，对单位判处罚金，并对其直接负责的主管人员和其他直接责任人员，依照第一款的规定处罚。
    
    刑法第二百八十六条之一 拒不履行信息网络安全管理义务罪 网络服务提供者不履行法律、行政法规规定的信息网络安全管理义务，经监管部门责令采取改正措施而拒不改正，有下列情形之一的，处三年以下有期徒刑、拘役或者管制，并处或者单处罚金： （一）致使违法信息大量传播的； （二）致使用户信息泄露，造成严重后果的； （三）致使刑事案件证据灭失，情节严重的； （四）有其他严重情节的。 单位犯前款罪的，对单位判处罚金，并对其直接负责的主管人员和其他直接责任人员，依照前款的规定处罚。 有前两款行为，同时构成其他犯罪的，依照处罚较重的规定定罪处罚。
    
    刑法第二百八十七条 利用计算机实施犯罪的提示性规定 利用计算机实施金融诈骗、盗窃、贪污、挪用公款、窃取国家秘密或者其他犯罪的，依照本法有关规定定罪处罚。
    
    刑法第二百八十七条之一 非法利用信息网络罪 利用信息网络实施下列行为之一，情节严重的，处三年以下有期徒刑或者拘役，并处或者单处罚金： （一）设立用于实施诈骗、传授犯罪方法、制作或者销售违禁物品、管制物品等违法犯罪活动的网站、通讯群组的； （二）发布有关制作或者销售毒品、枪支、淫秽物品等违禁物品、管制物品或者其他违法犯罪信息的； （三）为实施诈骗等违法犯罪活动发布信息的。 单位犯前款罪的，对单位判处罚金，并对其直接负责的主管人员和其他直接责任人员，依照第一款的规定处罚。 有前两款行为，同时构成其他犯罪的，依照处罚较重的规定定罪处罚。
    
    刑法第二百八十七条之二 帮助信息网络犯罪活动罪 明知他人利用信息网络实施犯罪，为其犯罪提供互联网接入、服务器托管、网络存储、通讯传输等技术支持，或者提供广告推广、支付结算等帮助，情节严重的，处三年以下有期徒刑或者拘役，并处或者单处罚金。 单位犯前款罪的，对单位判处罚金，并对其直接负责的主管人员和其他直接责任人员，依照第一款的规定处罚。 有前两款行为，同时构成其他犯罪的，依照处罚较重的规定定罪处罚。
    
    网络安全法第二十七条 任何个人和组织不得从事非法侵入他人网络、干扰他人网络正常功能、窃取网络数据等危害网络安全的活动；不得提供专门用于从事侵入网络、干扰网络正常功能及防护措施、窃取网络数据等危害网络安全活动的程序、工具；明知他人从事危害网络安全的活动的，不得为其提供技术支持、广告推广、支付结算等帮助。
    
    网络安全法第六十三条 违反本法第二十七条规定，从事危害网络安全的活动，或者提供专门用于从事危害网络安全活动的程序、工具，或者为他人从事危害网络安全的活动提供技术支持、广告推广、支付结算等帮助，尚不构成犯罪的，由公安机关没收违法所得，处五日以下拘留，可以并处五万元以上五十万元以下罚款；情节较重的，处五日以上十五日以下拘留，可以并处十万元以上一百万元以下罚款。单位有前款行为的，由公安机关没收违法所得，处十万元以上一百万元以下罚款，并对直接负责的主管人员和其他直接责任人员依照前款规定处罚。违反本法第二十七条规定，受到治安管理处罚的人员，五年内不得从事网络安全管理和网络运营关键岗位的工作；受到刑事处罚的人员，终身不得从事网络安全管理和网络运营关键岗位的工作。

Athena 是一款功能弱🐔的安全评估工具，由一名 `无名菜🐶` 拉屎的时候偶然想到的，主要特性有:

+ **检测速度快**。发包速度快; 漏洞检测算法高效。
+ **支持范围广**。大至 OWASP Top 10 通用漏洞检测，小至各种 CMS 框架 POC，均可以支持。
+ **代码质量高**。编写代码的人员素质高, 通过 Code Review、单元测试、集成测试等多层验证来提高代码可靠性。
+ **高级可定制**。通过内置 `KnowBase` 对象，实现信息的共享，
+ **安全无威胁**。Athena 定位为一款安全辅助评估工具，只要你`不开进攻性扫描`，内置的所有 payload 和 poc 均为无害化检查。


以后大概会支持并且现在不支持的漏洞检测类型包括:

- XSS漏洞检测 (key: xss)
- SQL 注入检测 (key: sqldet)
- 命令/代码注入检测 (key: cmd_injection)
- 目录枚举 (key: dirscan)
- 路径穿越检测 (key: path_traversal)
- XML 实体注入检测 (key: xxe)
- 文件上传检测 (key: upload)
- 弱口令检测 (key: brute_force)
- jsonp 检测 (key: jsonp)
- ssrf 检测 (key: ssrf)
- 基线检查 (key: baseline)
- 任意跳转检测 (key: redirect)
- CRLF 注入 (key: crlf_injection)
- Struts2 系列漏洞检测 (高级版，key: struts2)
- Thinkphp系列漏洞检测 (高级版，key: thinkphp)

其中 POC 框架默认内置内部公开扫描流程插件，用户也可以根据需要自行构建 插件 并运行。


## 设计理念

1. 发最少的包做效果最好的探测。

   如果一个请求可以确信漏洞存在，那就发一个请求。如果两种漏洞环境可以用同一个 payload 探测出来，那就
   不要拆成两个。
    
1. 允许一定程度上的误报来换取扫描速度的提升

   漏洞检测工具无法面面俱到，在漏报和误报的选择上必然要选择误报。如果在使用中发现误报比较严重，可以进行反馈。
    
+ 尽量不用时间盲注等机制检测漏洞。
    
   时间检测受影响因素太多且不可控，而且可能会影响其他插件的运行。因此除非必要（如 sql）请尽量使用与时间无关的
   payload。

+ 尽量不使用盲打平台

   如果一个漏洞能用回显检测就用回显检测，因为盲打平台增加了漏洞检测过程的不确定性和复杂性。
 
+ 耗时操作谨慎处理

   全局使用 Context 做管理，不会因为某个请求而导致全局卡死。

## 简易架构

了解 Athena 的整体架构可以更好的理解 插件的编写，方便大家更好的使用。

整体来看，扫描器这类工具大致都是由三部分组成：

1. 来源处理
1. 漏洞检测
1. 结果输出

#### 来源处理

这一部分的功能是整个漏洞检测的入口，在 Athena 中我们定义了 1 个入口

+ 插件中的assign函数负责任务调度


#### 漏洞检测


这一部分通过漏洞扫描引擎中的脚本引擎对扫描插件进行解析

并且完成联动调用

用户可以针对性的启用检测类别，配置扫描插件的参数，配置 HTTP 相关参数等。


#### 结果输出

漏洞扫描和运行时的状态统称为结果输出，Athena 定义了如下几种输出方式:

+ 在线查看报告
+ url报告分享
+ HTML离线报告导出

在使用 Athena 的过程中只要谨记这三个部分，所有的插件编写就看起来很简单了。 接下来就让我们上路吧。
