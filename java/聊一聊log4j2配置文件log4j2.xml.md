<div id="post_detail">
<!--done-->
<div id="topics">
	<div class="post">
		<h1 class="postTitle">
			<a id="cb_post_title_url" class="postTitle2" href="http://www.cnblogs.com/hafiz/p/6170702.html">聊一聊log4j2配置文件log4j2.xml</a>
		</h1>
		<div class="clear"></div>
		<div class="postBody">
			<div id="cnblogs_post_body"><h3>&nbsp;一、背景</h3>
<p>　　最近由于项目的需要，我们把log4j 1.x的版本全部迁移成log4j 2.x 的版本，那随之而来的slf4j整合log4j的配置（<span style="color: #ff0000;"><strong><span style="text-decoration: underline;"><a id="homepage1_HomePageDays_DaysList_ctl00_DayList_TitleUrl_0" class="postTitle2" href="http://www.cnblogs.com/hafiz/p/6160298.html" target="_blank"><span style="color: #ff0000; text-decoration: underline;">使用Slf4j集成Log4j2构建项目日志系统的完美解决方案</span></a></span></strong></span>）以及log4j2配置文件的详解，就需要我们来好好聊一聊了。本文就专门来讲解下log4j2.xml配置文件的各项标签的意义。</p>
<h3>二、配置全解</h3>
<p>　　1.关于配置文件的名称以及在项目中的存放位置</p>
<p>　　　　log4j 2.x版本不再支持像1.x中的.properties后缀的文件配置方式，2.x版本配置文件后缀名只能为".xml",".json"或者".jsn".</p>
<p>　　　　系统选择配置文件的优先级(从先到后)如下：</p>
<p>　　　　　　(1).classpath下的名为log4j2-test.json 或者log4j2-test.jsn的文件.</p>
<p>　　　　　　(2).classpath下的名为log4j2-test.xml的文件.</p>
<p>　　　　　　(3).classpath下名为log4j2.json 或者log4j2.jsn的文件.</p>
<p>　　　　　　(4).classpath下名为log4j2.xml的文件.</p>
<p>　　　　　我们一般默认使用log4j2.xml进行命名。如果本地要测试，可以把log4j2-test.xml放到classpath，而正式环境使用log4j2.xml，则在打包部署的时候不要打包log4j2-test.xml即可。</p>
<p>　　2.缺省默认配置文件</p>
<div class="cnblogs_code"><div class="cnblogs_code_toolbar"><span class="cnblogs_code_copy"><a href="javascript:void(0);" onclick="copyCnblogsCode(this)" title="复制代码"><img src="//common.cnblogs.com/images/copycode.gif" alt="复制代码"></a></span></div>
<pre><span style="color: #008080;"> 1</span> <span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="UTF-8"</span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #008080;"> 2</span> <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Configuration </span><span style="color: #ff0000;">status</span><span style="color: #0000ff;">="WARN"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;"> 3</span>   <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Appenders</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;"> 4</span>     <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Console </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Console"</span><span style="color: #ff0000;"> target</span><span style="color: #0000ff;">="SYSTEM_OUT"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;"> 5</span>       <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">PatternLayout </span><span style="color: #ff0000;">pattern</span><span style="color: #0000ff;">="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;"> 6</span>     <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Console</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;"> 7</span>   <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Appenders</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;"> 8</span>   <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Loggers</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;"> 9</span>     <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Root </span><span style="color: #ff0000;">level</span><span style="color: #0000ff;">="error"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">10</span>       <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">AppenderRef </span><span style="color: #ff0000;">ref</span><span style="color: #0000ff;">="Console"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">11</span>     <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Root</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">12</span>   <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Loggers</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">13</span> <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Configuration</span><span style="color: #0000ff;">&gt;</span></pre>
<div class="cnblogs_code_toolbar"><span class="cnblogs_code_copy"><a href="javascript:void(0);" onclick="copyCnblogsCode(this)" title="复制代码"><img src="//common.cnblogs.com/images/copycode.gif" alt="复制代码"></a></span></div></div>
<p>　　3.配置文件节点解析　　　　</p>
<p>　　　　(1).根节点Configuration有两个属性:status和monitorinterval,有两个子节点:Appenders和Loggers(表明可以定义多个Appender和Logger).</p>
<p>　　　　　　　status用来指定log4j本身的打印日志的级别.</p>
<p>　　　　　　　monitorinterval用于指定log4j自动重新配置的监测间隔时间，单位是s,最小是5s.</p>
<p>　　　　(2).Appenders节点，常见的有三种子节点:Console、RollingFile、File.</p>
<p>　　　　　　　<strong>Console</strong>节点用来定义输出到控制台的Appender.</p>
<p>　　　　　　　　name:指定Appender的名字.</p>
<p>　　　　　　　　target:SYSTEM_OUT 或 SYSTEM_ERR,一般只设置默认:SYSTEM_OUT.</p>
<p>　　　　　　　　PatternLayout:输出格式，不设置默认为:%m%n.</p>
<p>　　　　　　　<strong>File</strong>节点用来定义输出到指定位置的文件的Appender.</p>
<p>　　　　　　　　name:指定Appender的名字.</p>
<p>　　　　　　　　fileName:指定输出日志的目的文件带全路径的文件名.</p>
<p>　　　　　　　　PatternLayout:输出格式，不设置默认为:%m%n.</p>
<p>　　　　　　　<strong>RollingFile</strong>节点用来定义超过指定大小自动删除旧的创建新的的Appender.</p>
<p>　　　　　　　　name:指定Appender的名字.</p>
<p>　　　　　　　　fileName:指定输出日志的目的文件带全路径的文件名.</p>
<p>　　　　　　　　PatternLayout:输出格式，不设置默认为:%m%n.</p>
<p>　　　　　　　　filePattern:指定新建日志文件的名称格式.</p>
<p>　　　　　　　　Policies:指定滚动日志的策略，就是什么时候进行新建日志文件输出日志.</p>
<p>　　　　　　　 TimeBasedTriggeringPolicy:Policies子节点，基于时间的滚动策略，interval属性用来指定多久滚动一次，默认是1 hour。modulate=true用来调整时间：比如现在是早上3am，interval是4，那么第一次滚动是在4am，接着是8am，12am...而不是7am.</p>
<p>　　　　　　　　SizeBasedTriggeringPolicy:Policies子节点，基于指定文件大小的滚动策略，size属性用来定义每个日志文件的大小.</p>
<p>　　　　　　　　DefaultRolloverStrategy:用来指定同一个文件夹下最多有几个日志文件时开始删除最旧的，创建新的(通过max属性)。</p>
<p>　　　　(3).Loggers节点，常见的有两种:Root和Logger.</p>
<p>　　　　　　　<strong>Root</strong>节点用来指定项目的根日志，如果没有单独指定Logger，那么就会默认使用该Root日志输出</p>
<p>　　　　　　　　　level:日志输出级别，共有8个级别，按照从低到高为：All&nbsp;&lt; Trace &lt; Debug &lt;&nbsp;Info&nbsp;&lt;&nbsp;Warn&nbsp;&lt; Error &lt; Fatal &lt;&nbsp;OFF.</p>
<p>　　　　　　　　　AppenderRef：Root的子节点，用来指定该日志输出到哪个Appender.</p>
<p>　　　　　　　<strong>Logger</strong>节点用来单独指定日志的形式，比如要为指定包下的class指定不同的日志级别等。</p>
<p>　　　　　　　　　level:日志输出级别，共有8个级别，按照从低到高为：All&nbsp;&lt; Trace &lt; Debug &lt;&nbsp;Info&nbsp;&lt;&nbsp;Warn&nbsp;&lt; Error &lt; Fatal &lt;&nbsp;OFF.</p>
<p>　　　　　　　　　name:用来指定该Logger所适用的类或者类所在的包全路径,继承自Root节点.</p>
<p>　　　　　　　　　AppenderRef：Logger的子节点，用来指定该日志输出到哪个Appender,如果没有指定，就会默认继承自Root.如果指定了，那么会在指定的这个Appender和Root的Appender中都会输出，此时我们可以设置Logger的additivity="false"只在自定义的Appender中进行输出。</p>
<p>　　　　(4).关于日志level.</p>
<p>　　　　　　共有8个级别，按照从低到高为：All&nbsp;&lt; Trace &lt; Debug &lt; Info&nbsp;&lt;&nbsp;Warn &lt; Error &lt; Fatal &lt;&nbsp;OFF.</p>
<p>　　　　　　All:最低等级的，用于打开所有日志记录.</p>
<p>　　　　　　Trace:是追踪，就是程序推进以下，你就可以写个trace输出，所以trace应该会特别多，不过没关系，我们可以设置最低日志级别不让他输出.</p>
<p>　　　　　　Debug:指出细粒度信息事件对调试应用程序是非常有帮助的.</p>
<p>　　　　　　Info:消息在粗粒度级别上突出强调应用程序的运行过程.</p>
<p>　　　　　　Warn:输出警告及warn以下级别的日志.</p>
<p>　　　　　　Error:输出错误信息日志.</p>
<p>　　　　　　Fatal:输出每个严重的错误事件将会导致应用程序的退出的日志.</p>
<p>　　　　　　OFF:最高等级的，用于关闭所有日志记录.</p>
<p>　　　　　　<span style="color: #ff0000;"><strong>程序会打印高于或等于所设置级别的日志，设置的日志等级越高，打印出来的日志就越少</strong></span>。</p>
<p>　　4.比较完整的log4j2.xml配置模板</p>
<div class="cnblogs_code"><div class="cnblogs_code_toolbar"><span class="cnblogs_code_copy"><a href="javascript:void(0);" onclick="copyCnblogsCode(this)" title="复制代码"><img src="//common.cnblogs.com/images/copycode.gif" alt="复制代码"></a></span></div>
<pre><span style="color: #008080;"> 1</span> <span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="UTF-8"</span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #008080;"> 2</span> <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">日志级别以及优先级排序: OFF &gt; FATAL &gt; ERROR &gt; WARN &gt; INFO &gt; DEBUG &gt; TRACE &gt; ALL </span><span style="color: #008000;">--&gt;</span>
<span style="color: #008080;"> 3</span> <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">Configuration后面的status，这个用于设置log4j2自身内部的信息输出，可以不设置，当设置成trace时，你会看到log4j2内部各种详细输出</span><span style="color: #008000;">--&gt;</span>
<span style="color: #008080;"> 4</span> <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">monitorInterval：Log4j能够自动检测修改配置 文件和重新配置本身，设置间隔秒数</span><span style="color: #008000;">--&gt;</span>
<span style="color: #008080;"> 5</span> <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">configuration </span><span style="color: #ff0000;">status</span><span style="color: #0000ff;">="WARN"</span><span style="color: #ff0000;"> monitorInterval</span><span style="color: #0000ff;">="30"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;"> 6</span>     <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">先定义所有的appender</span><span style="color: #008000;">--&gt;</span>
<span style="color: #008080;"> 7</span>     <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appenders</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;"> 8</span>     <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">这个输出控制台的配置</span><span style="color: #008000;">--&gt;</span>
<span style="color: #008080;"> 9</span>         <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">console </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Console"</span><span style="color: #ff0000;"> target</span><span style="color: #0000ff;">="SYSTEM_OUT"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">10</span>         <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">输出日志的格式</span><span style="color: #008000;">--&gt;</span>
<span style="color: #008080;">11</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">PatternLayout </span><span style="color: #ff0000;">pattern</span><span style="color: #0000ff;">="[%d{HH:mm:ss:SSS}] [%p] - %l - %m%n"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">12</span>         <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">console</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">13</span>     <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">文件会打印出所有信息，这个log每次运行程序会自动清空，由append属性决定，这个也挺有用的，适合临时测试用</span><span style="color: #008000;">--&gt;</span>
<span style="color: #008080;">14</span>     <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">File </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="log"</span><span style="color: #ff0000;"> fileName</span><span style="color: #0000ff;">="log/test.log"</span><span style="color: #ff0000;"> append</span><span style="color: #0000ff;">="false"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">15</span>        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">PatternLayout </span><span style="color: #ff0000;">pattern</span><span style="color: #0000ff;">="%d{HH:mm:ss.SSS} %-5level %class{36} %L %M - %msg%xEx%n"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">16</span>     <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">File</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">17</span>     <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 这个会打印出所有的info及以下级别的信息，每次大小超过size，则这size大小的日志会自动存入按年份-月份建立的文件夹下面并进行压缩，作为存档</span><span style="color: #008000;">--&gt;</span>
<span style="color: #008080;">18</span>         <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">RollingFile </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="RollingFileInfo"</span><span style="color: #ff0000;"> fileName</span><span style="color: #0000ff;">="${sys:user.home}/logs/info.log"</span>
<span style="color: #008080;">19</span> <span style="color: #ff0000;">                     filePattern</span><span style="color: #0000ff;">="${sys:user.home}/logs/$${date:yyyy-MM}/info-%d{yyyy-MM-dd}-%i.log"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">20</span>             <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">控制台只输出level及以上级别的信息（onMatch），其他的直接拒绝（onMismatch）</span><span style="color: #008000;">--&gt;</span>        
<span style="color: #008080;">21</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ThresholdFilter </span><span style="color: #ff0000;">level</span><span style="color: #0000ff;">="info"</span><span style="color: #ff0000;"> onMatch</span><span style="color: #0000ff;">="ACCEPT"</span><span style="color: #ff0000;"> onMismatch</span><span style="color: #0000ff;">="DENY"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">22</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">PatternLayout </span><span style="color: #ff0000;">pattern</span><span style="color: #0000ff;">="[%d{HH:mm:ss:SSS}] [%p] - %l - %m%n"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">23</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Policies</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">24</span>                 <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">TimeBasedTriggeringPolicy</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">25</span>                 <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SizeBasedTriggeringPolicy </span><span style="color: #ff0000;">size</span><span style="color: #0000ff;">="100 MB"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">26</span>             <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Policies</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">27</span>         <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">RollingFile</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">28</span>         <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">RollingFile </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="RollingFileWarn"</span><span style="color: #ff0000;"> fileName</span><span style="color: #0000ff;">="${sys:user.home}/logs/warn.log"</span>
<span style="color: #008080;">29</span> <span style="color: #ff0000;">                     filePattern</span><span style="color: #0000ff;">="${sys:user.home}/logs/$${date:yyyy-MM}/warn-%d{yyyy-MM-dd}-%i.log"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">30</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ThresholdFilter </span><span style="color: #ff0000;">level</span><span style="color: #0000ff;">="warn"</span><span style="color: #ff0000;"> onMatch</span><span style="color: #0000ff;">="ACCEPT"</span><span style="color: #ff0000;"> onMismatch</span><span style="color: #0000ff;">="DENY"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">31</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">PatternLayout </span><span style="color: #ff0000;">pattern</span><span style="color: #0000ff;">="[%d{HH:mm:ss:SSS}] [%p] - %l - %m%n"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">32</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Policies</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">33</span>                 <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">TimeBasedTriggeringPolicy</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">34</span>                 <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SizeBasedTriggeringPolicy </span><span style="color: #ff0000;">size</span><span style="color: #0000ff;">="100 MB"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">35</span>             <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Policies</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">36</span>         <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> DefaultRolloverStrategy属性如不设置，则默认为最多同一文件夹下7个文件，这里设置了20 </span><span style="color: #008000;">--&gt;</span>
<span style="color: #008080;">37</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">DefaultRolloverStrategy </span><span style="color: #ff0000;">max</span><span style="color: #0000ff;">="20"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">38</span>         <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">RollingFile</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">39</span>         <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">RollingFile </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="RollingFileError"</span><span style="color: #ff0000;"> fileName</span><span style="color: #0000ff;">="${sys:user.home}/logs/error.log"</span>
<span style="color: #008080;">40</span> <span style="color: #ff0000;">                     filePattern</span><span style="color: #0000ff;">="${sys:user.home}/logs/$${date:yyyy-MM}/error-%d{yyyy-MM-dd}-%i.log"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">41</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ThresholdFilter </span><span style="color: #ff0000;">level</span><span style="color: #0000ff;">="error"</span><span style="color: #ff0000;"> onMatch</span><span style="color: #0000ff;">="ACCEPT"</span><span style="color: #ff0000;"> onMismatch</span><span style="color: #0000ff;">="DENY"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">42</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">PatternLayout </span><span style="color: #ff0000;">pattern</span><span style="color: #0000ff;">="[%d{HH:mm:ss:SSS}] [%p] - %l - %m%n"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">43</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Policies</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">44</span>                 <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">TimeBasedTriggeringPolicy</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">45</span>                 <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SizeBasedTriggeringPolicy </span><span style="color: #ff0000;">size</span><span style="color: #0000ff;">="100 MB"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">46</span>             <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Policies</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">47</span>         <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">RollingFile</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">48</span>     <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">appenders</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">49</span>     <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">然后定义logger，只有定义了logger并引入的appender，appender才会生效</span><span style="color: #008000;">--&gt;</span>
<span style="color: #008080;">50</span>     <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">loggers</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">51</span>         <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">过滤掉spring和mybatis的一些无用的DEBUG信息</span><span style="color: #008000;">--&gt;</span>
<span style="color: #008080;">52</span>         <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">logger </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="org.springframework"</span><span style="color: #ff0000;"> level</span><span style="color: #0000ff;">="INFO"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">logger</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">53</span>         <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">logger </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="org.mybatis"</span><span style="color: #ff0000;"> level</span><span style="color: #0000ff;">="INFO"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">logger</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">54</span>         <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">root </span><span style="color: #ff0000;">level</span><span style="color: #0000ff;">="all"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">55</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appender-ref </span><span style="color: #ff0000;">ref</span><span style="color: #0000ff;">="Console"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">56</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appender-ref </span><span style="color: #ff0000;">ref</span><span style="color: #0000ff;">="RollingFileInfo"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">57</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appender-ref </span><span style="color: #ff0000;">ref</span><span style="color: #0000ff;">="RollingFileWarn"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">58</span>             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appender-ref </span><span style="color: #ff0000;">ref</span><span style="color: #0000ff;">="RollingFileError"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #008080;">59</span>         <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">root</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">60</span>     <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">loggers</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008080;">61</span> <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span></pre>
<div class="cnblogs_code_toolbar"><span class="cnblogs_code_copy"></span></div></div>
<p>&nbsp;</p></div><div id="MySignature"></div>
<div class="clear"></div>
<div id="blog_post_info_block">
<div id="BlogPostCategory"></div>
<div id="EntryTag"></div>

</div>