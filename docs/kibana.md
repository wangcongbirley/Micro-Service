一、前言
Kibana 是一个开源的分析和可视化平台，旨在与 Elasticsearch 合作。Kibana 提供搜索、查看和与存储在 Elasticsearch 索引中的数据进行交互的功能。开发者或运维人员可以轻松地执行高级数据分析，并在各种图表、表格和地图中可视化数据。

二、准备
本篇文章的内容基于《Elasticsearch 基础入门》 和 《Logstash 基础入门》 讲解，还没了解 Elasticsearch 和 Logstach 的读者可以在本站中翻阅相应的文章或自行百度进行知识普及后再回到本文进行阅览。

### 2.1 安装 Kibana

 
wget https://artifacts.elastic.co/downloads/kibana/kibana-5.6.3-linux-x86_64.tar.gz
 
tar -zxvf kibana-5.6.3-linux-x86_64.tar.gz
 
cd kibana-5.6.3-linux-x86_64/
### 2.2 修改配置文件

 
vim config/kibana.yml
 
#### 将默认配置改成如下：
 
server.port: 5601
server.host: "0.0.0.0"
elasticsearch.url: "http://192.168.2.41:9200"
kibana.index: ".kibana"
### 2.3 启动

 
bin/kibana
启动后打开浏览器访问 http://192.168.2.43:5601 浏览 kibana 界面：



三、演示
上图中，提示不能获取映射，即 Elasticsearch 中的索引。我们需要手动配置。在 Index Pattern 下边的输入框中输入 access-*，它是 Elasticsearch 中的一个索引名称开头。

Kibana 会自动检测在 Elasticsearch 中是否存在该索引名称，如果有，则下边出现 “Create” 按钮，我们点击进行创建并来到如下界面：



### 3.1 Discovery
“Discovery” 菜单界面主要用于通过搜索请求，过滤结果，查看文档数据。可以查询搜索请求的文档总数，获取字段值的统计情况并通过柱状图进行展示。

点击左侧 “Discovery” 菜单，来到如下界面：



不了解查询条件如何使用，可以先随便输入查询条件进行查询，界面会提示找不到信息，同时还会提示查询方式。

### 3.2 Visualize
“Visualize” 菜单界面主要用于将查询出的数据进行可视化展示，且可以将其保存或加载合并到 Dashboard 中。

点击左侧 “Visualize” 菜单，再点击界面中间的 “Create a visualization” 按钮来到如下界面：



本次测试选择柱状图演示，点击柱状图：



点击右上角“Save” 按钮可以进行保存。笔者将该可视化保存为 “Nginx access”。

### 3.3 Dashboard
在“Dashboard” 菜单界面中，我们可以自由排列一组已保存的可视化数据。

点击左侧 “Dashboard” 菜单，再点击界面中间的 “Create a dashboard” 按钮进行创建：



### 3.4 Timelion
Timelion 是一个时间序列数据的可视化，可以结合在一个单一的可视化完全独立的数据源。它是由一个简单的表达式语言驱动的，用来检索时间序列数据，进行计算，找出复杂的问题的答案，并可视化的结果。

### 3.5 Dev Tools
“Dev Tools” 菜单界面使用户方便的通过浏览器直接与 Elasticsearch 进行交互，发送 RESTFUL 请求可以对 Elasticsearch 数据进行增删改查：
