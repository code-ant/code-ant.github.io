---
title: 我的书单
date: 2020-01-26 20:00:40
type: booklist
---


<style>
.hexo-douban-tabs {
    margin-bottom: 15px;
    margin-top: 15px;
}

.hexo-douban-tab {
    padding: 5px;
}

.hexo-douban-active {
    background: #657b83;
    color: #fff;
}

.hexo-douban-active:hover{
    background: #657b83;
    color: red;
}

.hexo-douban-item {
    padding-bottom: 10px;
    position: relative;
    clear: both;
    min-height: 170px;
    padding: 10px 0;
    border-bottom: 1px #ddd solid;
}

@media screen and (max-width: 600px) {
    .hexo-douban-item {
        width: 100%;
    }
}

.hexo-douban-picture {
    position: absolute;
    left: 0;
    top: 10px;
    width: 100px;
}

.hexo-douban-info {
    padding-left: 120px;
}

.hexo-douban-meta {
    font-size: 12px;
    padding-right: 10px;
}

.hexo-douban-comments {
    font-size: 12px;
}

.hexo-douban-pagination {
    margin-top: 15px;
    text-align: center;
    margin-bottom: 10px;
}

.hexo-douban-button {
    padding: 5px;
}

.hexo-douban-button:hover {
    background: #657b83;
    color: #fff;
}

.hexo-douban-hide {
    display: none;
}

.hexo-douban-show {
    display: block;
}

.hexo-douban-picture img{
    width:92px;
    height:131px
}
</style>


<!-- Main Content start-->
<div class="container">
<!-- <h1>这里是我的书籍清单</h1> -->
<blockquote>
    <p>{{ site.data.bookstj.booknote }}</p>
</blockquote>

<div class="hexo-douban-tabs">
    <a class="hexo-douban-tab" id="hexo-douban-tab1" href="javascript:;" rel="external">
        在读
        ({{ site.data.bookstj.zdnum }})</a>
    <a class="hexo-douban-tab" id="hexo-douban-tab2" href="javascript:;" rel="external">
        想读
        ({{ site.data.bookstj.xdnum }})</a>
    <a class="hexo-douban-tab" id="hexo-douban-tab3" href="javascript:;" rel="external">
        已读
        ({{ site.data.bookstj.ydnum }})</a>
</div>

<div>
  <!-- 在读 start -->
  <div id="hexo-douban-item1">
    <!-- 在读000开始 -->
    {% for book in site.data.bookszd %}
    <div class="hexo-douban-item">
      <div class="hexo-douban-picture"><img src="{{ book.bookimg }}" data-src="{{ book.bookimg }}" referrerpolicy="no-referrer"></div>
      <div class="hexo-douban-info">
          <div class="hexo-douban-title"><a target="_blank" href="{{ book.doubanurl }}"> {{ book.name }}</a></div>
          <div class="hexo-douban-meta">
            {{ book.author }} | {{ book.press }} | {{ book.publishdate }} | {{ book.price }}
          </div>
          <div class="hexo-douban-meta">{{ book.readdate }} 在读 | {{ book.booktag }}</div>
          <div class="hexo-douban-comments"></div>
      </div>
    </div>
    {% endfor %}
    <!-- 在读000结束 -->
    
   <!-- 分页 开始 -->
   <div class="hexo-douban-pagination">
      <a class="hexo-douban-button hexo-douban-firstpage" href="javascript:;"> 首页</a>
      <a class="hexo-douban-button hexo-douban-previouspage" href="javascript:;">上一页</a>
      <span class="hexo-douban-pagenum">2 / 3</span>
      <a class="hexo-douban-button hexo-douban-nextpage" href="javascript:;">下一页</a>
      <a class="hexo-douban-button hexo-douban-lastpage" href="javascript:;">尾页</a>
    </div>
   <!-- 分页 结束 -->
    
  </div>
  <!-- 在读 end -->

  <!-- 想读 start -->
  <div id="hexo-douban-item2">
    <!-- 想读000开始 -->
    {% for book in site.data.booksxd %}
    <div class="hexo-douban-item">
      <div class="hexo-douban-picture"><img src="{{ book.bookimg }}" data-src="{{ book.bookimg }}" referrerpolicy="no-referrer"></div>
      <div class="hexo-douban-info">
          <div class="hexo-douban-title"><a target="_blank" href="{{ book.doubanurl }}"> {{ book.name }}</a></div>
          <div class="hexo-douban-meta">
            {{ book.author }} | {{ book.press }} | {{ book.publishdate }} | {{ book.price }}
          </div>
          <div class="hexo-douban-meta">{{ book.readdate }} 想读 | {{ book.booktag }}</div>
          <div class="hexo-douban-comments"></div>
      </div>
    </div>
    {% endfor %}
    <!-- 想读000结束 -->
    
   <!-- 分页 开始 -->
   <div class="hexo-douban-pagination">
      <a class="hexo-douban-button hexo-douban-firstpage" href="javascript:;"> 首页</a>
      <a class="hexo-douban-button hexo-douban-previouspage" href="javascript:;">上一页</a>
      <span class="hexo-douban-pagenum">2 / 3</span>
      <a class="hexo-douban-button hexo-douban-nextpage" href="javascript:;">下一页</a>
      <a class="hexo-douban-button hexo-douban-lastpage" href="javascript:;">尾页</a>
   </div>
   <!-- 分页 结束 -->
    
  </div>
  <!-- 想读 end -->

  <!-- 已读 start -->
  <div id="hexo-douban-item3">
    <!-- 已读000开始 -->
    {% for book in site.data.booksyd %}
    <div class="hexo-douban-item">
      <div class="hexo-douban-picture"><img src="{{ book.bookimg }}" data-src="{{ book.bookimg }}" referrerpolicy="no-referrer"></div>
      <div class="hexo-douban-info">
          <div class="hexo-douban-title"><a target="_blank" href="{{ book.doubanurl }}"> {{ book.name }}</a></div>
          <div class="hexo-douban-meta">
            {{ book.author }} | {{ book.press }} | {{ book.publishdate }} | {{ book.price }}
          </div>
          <div class="hexo-douban-meta">{{ book.readdate }}
            读过 | {{ book.booktag }} | {{ book.stars }} {{ book.rate }}</div>
          <div class="hexo-douban-comments">我的书评：{{ book.review }}</div>
      </div>
    </div>
    {% endfor %}
    <!-- 已读000结束 -->
    
   <!-- 分页 开始 -->
   <div class="hexo-douban-pagination">
     <a class="hexo-douban-button hexo-douban-firstpage" href="javascript:;"> 首页</a>
     <a class="hexo-douban-button hexo-douban-previouspage" href="javascript:;">上一页</a>
     <span class="hexo-douban-pagenum">2 / 3</span>
     <a class="hexo-douban-button hexo-douban-nextpage" href="javascript:;">下一页</a>
     <a class="hexo-douban-button hexo-douban-lastpage" href="javascript:;">尾页</a>
   </div>
   <!-- 分页 结束 -->
    
  </div>
  <!-- 已读 end -->

</div>

   <!-- 书单统计 开始 -->
   <div align="center">
    在读书单共 <script language="JavaScript">
    var numitem1 = document.getElementById('hexo-douban-item1').getElementsByClassName('hexo-douban-item').length;
    document.write(numitem1)
</script> 本；
    想读书单共 <script language="JavaScript">
    var numitem2 = document.getElementById('hexo-douban-item2').getElementsByClassName('hexo-douban-item').length;
    document.write(numitem2)
</script> 本；
    已读书单共 <script language="JavaScript">
    var numitem3 = document.getElementById('hexo-douban-item3').getElementsByClassName('hexo-douban-item').length;
    document.write(numitem3)
</script> 本
    </div>
    <!-- 书单统计 结束 -->

</div>
<script type="text/javascript" src="/js/booklist.js"></script>

