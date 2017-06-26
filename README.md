
What is sitemap-php ?
----------

Fast and lightweight class for generating Google sitemap XML files and index of sitemap files. Written on PHP and uses XMLWriter extension (wrapper for libxml xmlWriter API) for creating XML files. XMLWriter extension is enabled by default in PHP 5 >= 5.1.2. If you having more than 50000 url, it splits items to seperated files. _(In benchmarks, 1.000.000 url was generating in 8 seconds)_


How to use
----------

Sitemap 封装了生成sitemap.xml的属性和方法的类，使用非常简单，示例代码：

	function testSitemap() {
		$sitemap = new Sitemap("http://mimvp.com");
		
		 $sitemap->addItem('/', '1.0', 'daily', 'Today');
		 $sitemap->addItem('/hr.php', '0.8', 'monthly', time());
		 $sitemap->addItem('/index.php', '1.0', 'daily', 'Jun 25');
		 $sitemap->addItem('/about.php', '0.8', 'monthly', '2017-06-26');
		 
		 $sitemap->addItem('/hr2.php', '1.0', 'daily', time())->addItem('/index2.php', '1.0', 'daily', 'Today')->addItem('/about2.php', '0.8', 'monthly', 'Jun 25');
		 
		 $sitemap->endSitemap();
	}

1. 初始化类对象

	$sitemap->addItem('/index.php', '1.0', 'daily', time());

2. 添加Item

	$sitemap->addItem('/', '1.0', 'daily', 'Today');
	$sitemap->addItem('/hr.php', '0.8', 'monthly', time());
	$sitemap->addItem('/index.php', '1.0', 'daily', 'Jun 25');
	$sitemap->addItem('/about.php', '0.8', 'monthly', '2017-06-26');

或者

	$sitemap->addItem('/hr2.php', '1.0', 'daily', time())->addItem('/index2.php', '1.0', 'daily', 'Today')->addItem('/about2.php', '0.8', 'monthly', 'Jun 25');

3. 结束文档

	$sitemap->endSitemap();
	
4. 生成结果 sitemap.xml

	<?xml version="1.0" encoding="UTF-8"?>
	<urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd" xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
		<url>
			<loc>http://mimvp.com/</loc>
			<priority>1.0</priority>
			<changefreq>daily</changefreq>
			<lastmod>2017-06-26T00:00:00+08:00</lastmod>
		</url>
		<url>
			<loc>http://mimvp.com/hr.php</loc>
			<priority>0.8</priority>
			<changefreq>monthly</changefreq>
			<lastmod>2017-06-26T19:20:24+08:00</lastmod>
		</url>
		<url>
			<loc>http://mimvp.com/index.php</loc>
			<priority>1.0</priority>
			<changefreq>daily</changefreq>
			<lastmod>2017-06-25T00:00:00+08:00</lastmod>
		</url>
		<url>
			<loc>http://mimvp.com/about.php</loc>
			<priority>0.8</priority>
			<changefreq>monthly</changefreq>
			<lastmod>2017-06-26T00:00:00+08:00</lastmod>
		</url>
	</urlset>



More Functions
----------

1. 设置根域名

	$sitemap = new Sitemap("http://mimvp.com");
	
修改初始化的域名为

	$sitemap->setDomain('http://blog.mimvp.com');
	
	
2. 设置保存路径
sitemap.xml默认保存在当前目录下，也可设置文件夹目录，例如： xmls/sitemap，表示sitemap.xml保存在当前目录下的xmls/目录下，其中xmls目录会自动创建。注：支持多级目录

	$sitemap->setXmlFile("xmls/sitemap");
	$sitemap->setXmlFile("xmls/mimvp/sitemap");
	
	
3. 设置是否更多头部

	$sitemap->setIsChemaMore(true);
	
如果设置为true，则sitemap.xml文件头部会增加一些头部信息：
	
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 	
	xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd" 
	
	
4. 获取当前写入的sitemap文件

	$sitemap->getCurrXmlFileFullPath();
	
	

Advanced Functions
----------

1. 指定包含文件，以/开头

	$GIncludeArray = array("", "/index.php", "about.php", "hr.php");

2. 排除特定文件或目录

	$GExcludeArray = array("usercenter/", "sadmin/", "admin/", "sitemap.php");

3. 递归扫描指定目录，默认扫描三层（可自己设定）

	function scanRootPath($rootPath=".", $dirLevel=1, $MaxDirLevel=3, &$resArray=array())

4. 转化 xml + xsl 为 html 

	function createXSL2Html($xmlFile, $xslFile, $htmlFile, $isopen_htmlfile=false) 



Sitemap Demo
----------

0. 全局变量，G开头
	
	$GCONFIG = array("domain"=>"http://mimvp.com",
		"xmlfile"=>"sitemap",
		"htmlfile"=>"sitemap.html",
		"xslfile"=>"sitemap-xml.xsl",
		"isopen_xmlfile"=>true,
		"isopen_htmlfile"=>true,
		"isscanrootpath"=>true,
		"isxsl2html"=>true,
		"isschemamore"=>true);


1. 生成sitemap.xml
		
	createSitemap();

生成示例：





2. 生成 sitemap.xml

	createXSL2Html($xmlFile, $xslFile, $htmlFile, $isopen_htmlfile=false);
	
生成示例：

	
	
You need to submit sitemap.xml and sitemap.html to Google、 Bing、 Baidu，etc.

**sitemap-php项目，目前支持指定网页、排除网页、扫描根目录等网站地图；后期完善时，会增加导出数据库、爬取整个网站等功能，也希望您的加入，继续完善此项目**

	Project sitemap-php All Rights by mimvp.com


