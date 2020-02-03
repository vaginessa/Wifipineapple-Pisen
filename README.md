# Wifipineaple-Pisen-WPR001N
<!DOCTYPE html>












  


<html class="theme-next gemini use-motion" lang="zh-CN">
<head>
  <meta charset="UTF-8"/>
<meta http-equiv="X-UA-Compatible" content="IE=edge" />
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=2"/>
<meta name="theme-color" content="#222">












<meta http-equiv="Cache-Control" content="no-transform" />
<meta http-equiv="Cache-Control" content="no-siteapp" />






















<link href="/lib/font-awesome/css/font-awesome.min.css?v=4.6.2" rel="stylesheet" type="text/css" />

<link href="/css/main.css?v=6.3.0" rel="stylesheet" type="text/css" />


  <link rel="apple-touch-icon" sizes="180x180" href="/images/apple-touch-icon.png?v=6.3.0">


  <link rel="icon" type="image/png" sizes="32x32" href="/images/favicon-32x32.png?v=6.3.0">


  <link rel="icon" type="image/png" sizes="16x16" href="/images/favicon-16x16.png?v=6.3.0">


  <link rel="mask-icon" href="/images/logo-mine.svg?v=6.3.0" color="#222">









<script type="text/javascript" id="hexo.configurations">
  var NexT = window.NexT || {};
  var CONFIG = {
    root: '/',
    scheme: 'Gemini',
    version: '6.3.0',
    sidebar: {"position":"left","display":"post","offset":12,"b2t":true,"scrollpercent":true,"onmobile":false},
    fancybox: false,
    fastclick: false,
    lazyload: false,
    tabs: true,
    motion: {"enable":true,"async":false,"transition":{"post_block":"fadeIn","post_header":"slideDownIn","post_body":"slideDownIn","coll_header":"slideLeftIn","sidebar":"slideUpIn"}},
    algolia: {
      applicationID: '',
      apiKey: '',
      indexName: '',
      hits: {"per_page":10},
      labels: {"input_placeholder":"Search for Posts","hits_empty":"We didn't find any results for the search: ${query}","hits_stats":"${hits} results found in ${time} ms"}
    }
  };
</script>


  




  <meta name="description" content="WPR001N 和 WMM003N 刷不死Boot通用教程，使用品胜官方固件账号，免拆">
<meta name="keywords" content="OpenWrt">
<meta property="og:type" content="article">
<meta property="og:title" content="WPR001N 和 WMM003N 刷入OpenWrt">
<meta property="og:url" content="https://ifhw.github.io/2015/10/15/wpr001n-flash-firmware/index.html">
<meta property="og:site_name" content="Henry&#39;s Blog">
<meta property="og:description" content="WPR001N 和 WMM003N 刷不死Boot通用教程，使用品胜官方固件账号，免拆">
<meta property="og:locale" content="zh-CN">
<meta property="og:updated_time" content="2016-04-30T14:27:16.000Z">
<meta name="twitter:card" content="summary">
<meta name="twitter:title" content="WPR001N 和 WMM003N 刷入OpenWrt">
<meta name="twitter:description" content="WPR001N 和 WMM003N 刷不死Boot通用教程，使用品胜官方固件账号，免拆">






  <link rel="canonical" href="https://ifhw.github.io/2015/10/15/wpr001n-flash-firmware/"/>



<script type="text/javascript" id="page.configurations">
  CONFIG.page = {
    sidebar: "",
  };
</script>

  <title>WPR001N 和 WMM003N 刷入OpenWrt | Henry's Blog</title>
  




<script async src="https://www.googletagmanager.com/gtag/js?id=UA-69835848-1"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'UA-69835848-1');
</script>






  <noscript>
  <style type="text/css">
    .use-motion .motion-element,
    .use-motion .brand,
    .use-motion .menu-item,
    .sidebar-inner,
    .use-motion .post-block,
    .use-motion .pagination,
    .use-motion .comments,
    .use-motion .post-header,
    .use-motion .post-body,
    .use-motion .collection-title { opacity: initial; }

    .use-motion .logo,
    .use-motion .site-title,
    .use-motion .site-subtitle {
      opacity: initial;
      top: initial;
    }

    .use-motion {
      .logo-line-before i { left: initial; }
      .logo-line-after i { right: initial; }
    }
  </style>
</noscript>

</head>

<body itemscope itemtype="http://schema.org/WebPage" lang="zh-CN">

  
  
    
  

  <div class="container sidebar-position-left page-post-detail">
    <div class="headband"></div>

    <header id="header" class="header" itemscope itemtype="http://schema.org/WPHeader">
      <div class="header-inner"><div class="site-brand-wrapper">
  <div class="site-meta ">
    

    <div class="custom-logo-site-title">
      <a href="/" class="brand" rel="start">
        <span class="logo-line-before"><i></i></span>
        <span class="site-title">Henry's Blog</span>
        <span class="logo-line-after"><i></i></span>
      </a>
    </div>
    
      
        <p class="site-subtitle">漫漫开发路，悠悠笃行之。</p>
      
    
  </div>

  <div class="site-nav-toggle">
    <button aria-label="切换导航栏">
      <span class="btn-bar"></span>
      <span class="btn-bar"></span>
      <span class="btn-bar"></span>
    </button>
  </div>
</div>



<nav class="site-nav">
  
    <ul id="menu" class="menu">
      
        
        
        
          
          <li class="menu-item menu-item-home">
    <a href="/" rel="section">
      <i class="menu-item-icon fa fa-fw fa-home"></i> <br />首页</a>
  </li>
        
        
        
          
          <li class="menu-item menu-item-categories">
    <a href="/categories/" rel="section">
      <i class="menu-item-icon fa fa-fw fa-th"></i> <br />分类</a>
  </li>
        
        
        
          
          <li class="menu-item menu-item-archives">
    <a href="/archives/" rel="section">
      <i class="menu-item-icon fa fa-fw fa-archive"></i> <br />归档</a>
  </li>
        
        
        
          
          <li class="menu-item menu-item-about">
    <a href="/about/" rel="section">
      <i class="menu-item-icon fa fa-fw fa-user"></i> <br />关于</a>
  </li>

      
      
    </ul>
  

  

  
</nav>



  



</div>
    </header>

    


    <main id="main" class="main">
      <div class="main-inner">
        <div class="content-wrap">
          
            

          
          <div id="content" class="content">
            

  <div id="posts" class="posts-expand">
    

  

  
  
  

  

  <article class="post post-type-normal" itemscope itemtype="http://schema.org/Article">
  
  
  
  <div class="post-block">
    <link itemprop="mainEntityOfPage" href="https://ifhw.github.io/2015/10/15/wpr001n-flash-firmware/">

    <span hidden itemprop="author" itemscope itemtype="http://schema.org/Person">
      <meta itemprop="name" content="Henry">
      <meta itemprop="description" content="漫漫开发路，悠悠笃行之。">
      <meta itemprop="image" content="/images/avatar.jpg">
    </span>

    <span hidden itemprop="publisher" itemscope itemtype="http://schema.org/Organization">
      <meta itemprop="name" content="Henry's Blog">
    </span>

    
      <header class="post-header">

        
        
          <h1 class="post-title" itemprop="name headline">WPR001N 和 WMM003N 刷入OpenWrt
              
            
          </h1>
        

        <div class="post-meta">
          <span class="post-time">

            
            
            

            
              <span class="post-meta-item-icon">
                <i class="fa fa-calendar-o"></i>
              </span>
              
                <span class="post-meta-item-text">发表于</span>
              

              
                
              

              <time title="创建时间：2015-10-15 10:00:30" itemprop="dateCreated datePublished" datetime="2015-10-15T10:00:30+08:00">2015-10-15</time>
            

            
              

              
                
                <span class="post-meta-divider">|</span>
                

                <span class="post-meta-item-icon">
                  <i class="fa fa-calendar-check-o"></i>
                </span>
                
                  <span class="post-meta-item-text">更新于</span>
                
                <time title="修改时间：2016-04-30 22:27:16" itemprop="dateModified" datetime="2016-04-30T22:27:16+08:00">2016-04-30</time>
              
            
          </span>

          
            <span class="post-category" >
            
              <span class="post-meta-divider">|</span>
            
              <span class="post-meta-item-icon">
                <i class="fa fa-folder-o"></i>
              </span>
              
                <span class="post-meta-item-text">分类于</span>
              
              
                <span itemprop="about" itemscope itemtype="http://schema.org/Thing"><a href="/categories/OpenWrt/" itemprop="url" rel="index"><span itemprop="name">OpenWrt</span></a></span>

                
                
              
            </span>
          

          
            
          

          
          

          

          

          
              <div class="post-description">WPR001N 和 WMM003N 刷不死Boot通用教程，使用品胜官方固件账号，免拆</div>
          

        </div>
      </header>
    

    
    
    
    <div class="post-body" itemprop="articleBody">

      
      

      
        <h1 id="前言"><a href="#前言" class="headerlink" title="前言"></a>前言</h1><p>通常为了让路由器功能更丰富，我们会选择给路由器刷第三方的自定义固件。<br>我的目标是让路由自动登陆认证校园网，这里刷第三方固件只是第一步。<br>并不是所有的路由都能刷第三方固件的，现在政策对厂商要求越来越严格，以后可刷的估计越来越少了。<br>这两个路由和TP-Link的TL-WR703N路由模块硬件基本一样,可以使用TL-WR703N 的OpenWrt的固件。</p>
<p>本篇为入门级刷OpenWRT教程，会的可以无视了。<br>玩路由器，官方的Bootloader要是刷固件不小心给刷废了，那路由器就砖了<br>刷不死boot是玩路由的第一步，然后只要刷固件不刷boot分区就不会挂。</p>
<p>针对品胜的云路由WPR001N 和 WMM003N 我们需要先刷第三方Bootloader替换官方的。</p>
<p>我使用的是hackpascal开发的闭源Bootloader<br><a href="http://www.right.com.cn/forum/thread-161906-1-1.html" target="_blank" rel="noopener">http://www.right.com.cn/forum/thread-161906-1-1.html</a></p>
<p>文件名是breed-ar9331-pisen.bin<br>品胜云路由 (云座易充 WMM003N/无线音乐路由 WPR001N) 专用，波特率 115200，复位键 GPIO#12</p>
<h1 id="准备工作"><a href="#准备工作" class="headerlink" title="准备工作"></a>准备工作</h1><p>下载breed-ar9331-pisen.bin，复制到U盘根目录</p>
<h1 id="刷Bootloader"><a href="#刷Bootloader" class="headerlink" title="刷Bootloader"></a>刷Bootloader</h1><h2 id="telnet登陆到路由"><a href="#telnet登陆到路由" class="headerlink" title="telnet登陆到路由"></a>telnet登陆到路由</h2><p>利用路由器原始固件开放的telnet功能，刷入这个新的U-Boot文件。网线直接连接电脑和路由器，使用Telnet登陆到路由器。<br>Linux 终端直接输入telnet命令即可；<br>Windows telnet默认关闭的，在Windows功能里打开，具体自搜。<br>固件的默认账户：root，密码：ifconfig<br>连接命令：</p>
<pre><code>$ telnet 192.168.222.254
</code></pre><p>登陆后的默认位置<code>root@PISENWIFI:~#</code>  </p>
<h2 id="备份原分区文件"><a href="#备份原分区文件" class="headerlink" title="备份原分区文件"></a>备份原分区文件</h2><p><strong>以下所有命令均在登陆路由后的默认目录执行</strong></p>
<p>查看系统磁盘分区信息，可以看到<code>u-boot</code>和<code>art</code>分区</p>
<pre><code>$ cat /proc/mtd
</code></pre><p>备份原始u-boot和art到/tmp目录：</p>
<pre><code>$ dd if=/dev/mtd0 of=/tmp/uboot.bin
$ dd if=/dev/mtd4 of=/tmp/art.bin
</code></pre><p>插入U盘前查看文件系统的磁盘空间占用情况</p>
<pre><code>$ df
</code></pre><p>插入U盘后再执行 <code>df</code><br>可以发现多出一个 <code>/dev/sda4</code>就是U盘，挂载在 <code>/tmp/mnt/disk-a4</code></p>
<p>将备份的uboot.bin和art.bin移动到U盘</p>
<pre><code>$ mv /tmp/uboot.bin /tmp/mnt/disk-a4
$ mv /tmp/art.bin /tmp/mnt/disk-a4
</code></pre><p>看看是否备份成功</p>
<pre><code>$ ls /tmp/mnt/disk-a4
</code></pre><p>在列表里看是否有刚备份的u-boot.bin和art.bin</p>
<h2 id="刷breed替换原始u-boot"><a href="#刷breed替换原始u-boot" class="headerlink" title="刷breed替换原始u-boot"></a>刷breed替换原始u-boot</h2><p>把U盘里的breed-ar9331-pisen.bin复制到路由器/tmp目录</p>
<pre><code>$ cp /tmp/mnt/disk-a4/breed-ar9331-pisen.bin /tmp
</code></pre><p>刷入u-boot文件</p>
<pre><code>$ mtd -r write /tmp/breed-ar9331-pisen u-boot
</code></pre><p>执行完路由器会自动重启。<br>接下来就可以在 Breed Boot 控制台里刷固件了。</p>
<h1 id="刷Openwrt固件"><a href="#刷Openwrt固件" class="headerlink" title="刷Openwrt固件"></a>刷Openwrt固件</h1><p>进入控制台方式如下：<br>把路由断电，电脑设置成自动获取ip，给路由上电，迅速按住reset键，直到LED灯开始闪烁松手，电脑输入<a href="http://192.168.1.1" target="_blank" rel="noopener">http://192.168.1.1</a><br>就可以进入Breed控制台了。<br>注意在控制台的设置里看看MAC地址是否还是路由器的MAC，如果不是请改回来。（路由器MAC在机身说明部分）</p>
<p>在OpenWrt官网下载最新的Chaos_Calmer OpenWrt固件（2015.9），下载TL-WR 703N的固件就行，链接如下<br><a href="http://downloads.openwrt.org/chaos_calmer/15.05/ar71xx/generic/openwrt-15.05-ar71xx-generic-tl-wr703n-v1-squashfs-factory.bin" target="_blank" rel="noopener">http://downloads.openwrt.org/chaos_calmer/15.05/ar71xx/generic/openwrt-15.05-ar71xx-generic-tl-wr703n-v1-squashfs-factory.bin</a></p>
<p>在控制台的<strong>固件更新</strong>，勾选<strong>固件</strong>，选择下载的固件，然后上传，更新，建议使用Chrome或者FireFox浏览器。</p>
<h1 id="总结"><a href="#总结" class="headerlink" title="总结"></a>总结</h1><p>品胜的这两个路由带MicroUSB接口，可以使用通用的移动充电器或者移动电源供电，<br>在学校晚上断电，使用WPR001N 配移动电源就能在晚上宿舍断电后继续使用无线了！</p>

      
    </div>

    

    
    
    

    

    

    

    <footer class="post-footer">
      
        <div class="post-tags">
          
            <a href="/tags/OpenWrt/" rel="tag"># OpenWrt</a>
          
        </div>
      

      
      
      

      
        <div class="post-nav">
          <div class="post-nav-next post-nav-item">
            
              <a href="/2015/08/20/tar/" rel="next" title="Linux压缩与解压">
                <i class="fa fa-chevron-left"></i> Linux压缩与解压
              </a>
            
          </div>

          <span class="post-nav-divider"></span>

          <div class="post-nav-prev post-nav-item">
            
              <a href="/2015/10/16/wpr001n-mount-udisk/" rel="prev" title="品胜 WPR001N 路由器挂载U盘扩展磁盘空间">
                品胜 WPR001N 路由器挂载U盘扩展磁盘空间 <i class="fa fa-chevron-right"></i>
              </a>
            
          </div>
        </div>
      

      
      
    </footer>
  </div>
  
  
  
  </article>



    <div class="post-spread">
      
    </div>
  </div>


          </div>
          

  



        </div>
        
          
  
  <div class="sidebar-toggle">
    <div class="sidebar-toggle-line-wrap">
      <span class="sidebar-toggle-line sidebar-toggle-line-first"></span>
      <span class="sidebar-toggle-line sidebar-toggle-line-middle"></span>
      <span class="sidebar-toggle-line sidebar-toggle-line-last"></span>
    </div>
  </div>

  <aside id="sidebar" class="sidebar">
    
    <div class="sidebar-inner">

      

      
        <ul class="sidebar-nav motion-element">
          <li class="sidebar-nav-toc sidebar-nav-active" data-target="post-toc-wrap">
            文章目录
          </li>
          <li class="sidebar-nav-overview" data-target="site-overview-wrap">
            站点概览
          </li>
        </ul>
      

      <section class="site-overview-wrap sidebar-panel">
        <div class="site-overview">
          <div class="site-author motion-element" itemprop="author" itemscope itemtype="http://schema.org/Person">
            
              <img class="site-author-image" itemprop="image"
                src="/images/avatar.jpg"
                alt="Henry" />
            
              <p class="site-author-name" itemprop="name">Henry</p>
              <p class="site-description motion-element" itemprop="description">漫漫开发路，悠悠笃行之。</p>
          </div>

          
            <nav class="site-state motion-element">
              
                <div class="site-state-item site-state-posts">
                
                  <a href="/archives/">
                
                    <span class="site-state-item-count">22</span>
                    <span class="site-state-item-name">日志</span>
                  </a>
                </div>
              

              
                
                
                <div class="site-state-item site-state-categories">
                  <a href="/categories/index.html">
                    
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                    <span class="site-state-item-count">8</span>
                    <span class="site-state-item-name">分类</span>
                  </a>
                </div>
              

              
                
                
                <div class="site-state-item site-state-tags">
                  <a href="/tags/index.html">
                    
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                      
                    
                    <span class="site-state-item-count">17</span>
                    <span class="site-state-item-name">标签</span>
                  </a>
                </div>
              
            </nav>
          

          

          

          
          

          
          

          
            
          
          

        </div>
      </section>

      
      <!--noindex-->
        <section class="post-toc-wrap motion-element sidebar-panel sidebar-panel-active">
          <div class="post-toc">

            
              
            

            
              <div class="post-toc-content"><ol class="nav"><li class="nav-item nav-level-1"><a class="nav-link" href="#前言"><span class="nav-number">1.</span> <span class="nav-text">前言</span></a></li><li class="nav-item nav-level-1"><a class="nav-link" href="#准备工作"><span class="nav-number">2.</span> <span class="nav-text">准备工作</span></a></li><li class="nav-item nav-level-1"><a class="nav-link" href="#刷Bootloader"><span class="nav-number">3.</span> <span class="nav-text">刷Bootloader</span></a><ol class="nav-child"><li class="nav-item nav-level-2"><a class="nav-link" href="#telnet登陆到路由"><span class="nav-number">3.1.</span> <span class="nav-text">telnet登陆到路由</span></a></li><li class="nav-item nav-level-2"><a class="nav-link" href="#备份原分区文件"><span class="nav-number">3.2.</span> <span class="nav-text">备份原分区文件</span></a></li><li class="nav-item nav-level-2"><a class="nav-link" href="#刷breed替换原始u-boot"><span class="nav-number">3.3.</span> <span class="nav-text">刷breed替换原始u-boot</span></a></li></ol></li><li class="nav-item nav-level-1"><a class="nav-link" href="#刷Openwrt固件"><span class="nav-number">4.</span> <span class="nav-text">刷Openwrt固件</span></a></li><li class="nav-item nav-level-1"><a class="nav-link" href="#总结"><span class="nav-number">5.</span> <span class="nav-text">总结</span></a></li></ol></div>
            

          </div>
        </section>
      <!--/noindex-->
      

      
        <div class="back-to-top">
          <i class="fa fa-arrow-up"></i>
          
            <span id="scrollpercent"><span>0</span>%</span>
          
        </div>
      

    </div>
  </aside>


        
      </div>
    </main>

    <footer id="footer" class="footer">
      <div class="footer-inner">
        <div class="copyright">&copy; 2015 &mdash; <span itemprop="copyrightYear">2018</span>
  <span class="with-love" id="animate">
    <i class="fa fa-heart"></i>
  </span>
  <span class="author" itemprop="copyrightHolder">Henry</span>

  

  
</div>




  <div class="powered-by">由 <a class="theme-link" target="_blank" href="https://hexo.io">Hexo</a> 强力驱动 v3.7.1</div>



  <span class="post-meta-divider">|</span>



  <div class="theme-info">主题 &mdash; <a class="theme-link" target="_blank" href="https://github.com/theme-next/hexo-theme-next">NexT.Gemini</a> v6.3.0</div>




        








        
      </div>
    </footer>

    

    

  </div>

  

<script type="text/javascript">
  if (Object.prototype.toString.call(window.Promise) !== '[object Function]') {
    window.Promise = null;
  }
</script>


























  
  
    <script type="text/javascript" src="/lib/jquery/index.js?v=2.1.3"></script>
  

  
  
    <script type="text/javascript" src="/lib/velocity/velocity.min.js?v=1.2.1"></script>
  

  
  
    <script type="text/javascript" src="/lib/velocity/velocity.ui.min.js?v=1.2.1"></script>
  


  


  <script type="text/javascript" src="/js/src/utils.js?v=6.3.0"></script>

  <script type="text/javascript" src="/js/src/motion.js?v=6.3.0"></script>



  
  


  <script type="text/javascript" src="/js/src/affix.js?v=6.3.0"></script>

  <script type="text/javascript" src="/js/src/schemes/pisces.js?v=6.3.0"></script>



  
  <script type="text/javascript" src="/js/src/scrollspy.js?v=6.3.0"></script>
<script type="text/javascript" src="/js/src/post-details.js?v=6.3.0"></script>



  


  <script type="text/javascript" src="/js/src/bootstrap.js?v=6.3.0"></script>



  



	





  





  










  





  

  

  

  

  
  

  

  

  

  

  

</body>
</html>
