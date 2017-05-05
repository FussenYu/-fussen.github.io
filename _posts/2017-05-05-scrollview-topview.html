---
layout: post
title: Android在Scrollview里固定头布局
date: 2017-05-05
categories: blog
tags: [技巧]
description: 相信很多人都会遇到这个需求，需要将一个布局固定在view的最顶部，这个时候，我们的整个页面的最外层可能是Scrollview，整个页面是可以滑动的，我看了下市面上也有好多种做法，其中有一种，写了两套布局，监听scrollview的滑动，当这个布局滑到顶部的时候，让没有显示的布局显示出来，正好就实现了固定头布局的功能，但是这样做局限性太大，如果说这个要被固定的布局有自己状态，怎么办？那岂不是很麻烦了，所以为此，咱们换一种思路，既要实现固定的功能，也要保存被固定布局里的状态不被改变。
src: http://ww4.sinaimg.cn/large/006tNbRwgy1ffafjsk0foj31hc0vnawf.jpg
---



    <!-- 头像固定格式 -->
    <section label="fussen" style="margin-top: 0.5em; margin-bottom: 0.5em; box-sizing: border-box;">

                        <center>
                            <section style="box-sizing: border-box;width: 4em;height: 4em;display: inline-block;vertical-align: bottom;border-radius: 100%;background-image: url(&quot;https://ww2.sinaimg.cn/large/006tKfTcgy1fdba6o441fj30qo0zktqi.jpg&quot;);background-size: cover;background-position: 50% 50%;background-repeat: no-repeat;" class="">
                                <br  />
                            </section>

                            <p>
                                <span style="font-size: 14px;color: rgb(102, 204, 197);line-height: 1.6;"><a href="http://fussen.cc/about">Fussen</a>
                                </span>
                            </p>
                        </center>
      </section>
<div class="entry-content">


    <!-- 标题统一格式 -->
    <h1 class="entry-title">Android在Scrollview里固定头布局</h1>

<h2>前言</h2>

<p>相信很多人都会遇到这个需求，需要将一个布局固定在view的最顶部，这个时候，我们的整个页面的最外层可能是Scrollview，整个页面是可以滑动的，我看了下市面上也有好多种做法，其中有一种，写了两套布局，监听scrollview的滑动，当这个布局滑到顶部的时候，让没有显示的布局显示出来，正好就实现了固定头布局的功能，但是这样做局限性太大，如果说这个要被固定的布局有自己状态，怎么办？那岂不是很麻烦了，所以为此，咱们换一种思路，既要实现固定的功能，也要保存被固定布局里的状态不被改变。</p>

<h2>效果</h2>

<p>
  <img  height="400" src="http://ww4.sinaimg.cn/large/006tNbRwgy1ffaai9yg57g30940gbq9l.gif" width="100" />
</p>
<p>大家可以看到，上面被固定的布局里也有他自己的状态。</p>

<h2>实现思路</h2>

<ol>
	<li>最外层的布局是FrameLayout容器，大家要知道他的特性，是层级显示的，谁后被添加的就会显示在最上层，然后遮挡住底层布局。</li>
	<li>FrameLayout里第一层的布局就是LinearLayout，也就是上面显示的布局，LinearLayout里面又放的是上面三个布局，分别是头布局，要被固定的布局，下面是滑动的内容区域。</li>
	<li>还有一点，就是LinearLayout添加子view的顺序，也就是子view在LinearLayout中的角标大家一定要清楚，第一个被添加的，角标就是0，一次类推。</li>
	<li>这个时候，好像不能滑动啊，没有说Scrollview啊，其实，当FrameLayout加载完成后，才开始创建Scrollview的，然后将LinearLayout添加到了Scrollview里。</li>
	<li>Scrollview是自定义的，在Scrollview里监听滑动，当滑到头部的高度时，这时候就需要固定topview(需要被固定的布局)了,固定的方式就是先将topview保存下来，从LinearLayout容器中删除，然后直接添加到最外层的FrameLayout容器中去，这个时候，FrameLayout容器里就有了2个子view，topview在最上层。</li>
	<li>当Scrollview向下滑动时，当滑动到头布局的高度时，这个时候就将topview从FrameLayout中删除，然后又添加到LinearLayout中去，注意，这个时候要向LinearLayout中添加元素的时候，要注意子view在容器中的角标，LinearLayout中以前有3个元素，删去一个就剩下了2个，我们要将topview添加到LinearLayout的中间去，那这个时候的角标自然是2了。LinearLayout是垂直布局。</li>
	<li>以上的做法也就实现了我们想要的功能，这只是一种思路，具体如何运用，那就要看大家的想象力了。</li>
</ol>

<h2>部分代码</h2>

<p>
	

```
 /**
	 * 必须要放到post中去   这是Android4.4以下的bug 为的只是防止并发操作view
	 * @param scrollY
	 */
	private void onScroll(final int scrollY) {

		post(new Runnable() {
			@Override
			public void run() {
				if (mTopView == null) return;

				if (scrollY >= mTopViewTop && mTopView.getParent() == mContentView) {

					mContentView.removeView(mTopView);
					addView(mTopView);

				} else if (scrollY < mTopViewTop && mTopView.getParent() == SmartScrollView.this) {
					removeView(mTopView);
					//添加到LinearLayout角标为1处
					mContentView.addView(mTopView,1);
				}
			}
		});


	}
```

</p>


<p><strong>如果不将删除view和添加view的操作放到post中去就会报错</strong></p>

<blockquote>
<p>android.view.ViewGroup.dispatchDraw</p>
</blockquote>

<p>这是因为删除和添加的动作没有在一个线程工作，出现了并发操作，在绘制view的时候，4.4以下系统没有判断是否为空。</p>

<h2>获取源码</h2>

<ol>
	<li>在微信公众号AppCode里回复关键字：“固定”即可拿到源码下载链接。</li>
	<li>扫描下面二维码即可关注AppCdoe.</li>
</ol>

<p>
 <img  height="200" src="http://upload-images.jianshu.io/upload_images/3267943-35cf55f437d712a9.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" width="200" />
</p>


</div>

