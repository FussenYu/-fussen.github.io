---
layout: post
title: 我的第一篇文章啊
date: 2017-03-04
categories: blog
tags: [写作,千字文]
description: 多写一点，有好处啊

---




<article id="post-3552" class="no-featured-image post-3552 post type-post status-publish format-standard hentry category-3 tag-672 tag-620 tag-673 tag-286">
						
				<div class="">

				    	<h1 class="entry-title">
					为什么微信必须做付费订阅及可能怎么做			</h1>

				    <div class="entry-content">
				    
					    <p>



## 说明
现在市场的应用都会有查看头像或者照片墙的功能，很简单的一个功能，但是呢，你可以打开市场上的应用比较一下，其实微信的查看图片功能做的非常不错，今天就实现类似于微信的查看图片的功能
## 效果

## 实现思路
1. 拿到每个条目的矩形区域在屏幕中的坐标，并且保存到集合中
2. 缩放比例的计算
3. 播放缩放动画
4. 图片展示

## 代码展示
1. 获取点击区域坐标

	 		// If there's an animation in progress, cancel it immediately and proceed with this one.
	        if (mCurrentAnimator != null) {
	            mCurrentAnimator.cancel();
	        }
	
	        // set adapter and change current item
	
	        viewPager.setAdapter(pagerAdapter);
	        viewPager.setCurrentItem(position);
	
	        //prepare points
	        if (mData.size() > 1) {
	            preparePoints(position);
	        }
	
	        // Calculate the starting and ending bounds for the zoomed-in item view(ImageView).
	        final Rect startBounds = new Rect();
	        final Rect finalBounds = new Rect();
	        final Point globalOffset = new Point();
	
	        // The start bounds are the global visible rectangle of the view, and the
	        // final bounds are the global visible rectangle of the container view. Also
	        // set the container view's offset as the origin for the bounds, since that's
	        // the origin for the positioning animation properties (X, Y).
	
	        view.getGlobalVisibleRect(startBounds);
	
	        container.getGlobalVisibleRect(finalBounds, globalOffset);
	
	        startBounds.offset(-globalOffset.x, -globalOffset.y);
	        finalBounds.offset(-globalOffset.x, -globalOffset.y);

2. 计算缩放比例

		 		// Adjust the start bounds to be the same aspect ratio as the final bounds using the
		        // "center crop" technique. This prevents undesirable stretching during the animation.
		        // Also calculate the start scaling factor (the end scaling factor is always 1.0).
		        float startScale;
		        if ((float) finalBounds.width() / finalBounds.height()
		                > (float) startBounds.width() / startBounds.height()) {
		            // Extend start bounds horizontally
		            startScale = (float) startBounds.height() / finalBounds.height();
		            float startWidth = startScale * finalBounds.width();
		            float deltaWidth = (startWidth - startBounds.width()) / 2;
		            startBounds.left -= deltaWidth;
		            startBounds.right += deltaWidth;
		        } else {
		            // Extend start bounds vertically
		            startScale = (float) startBounds.width() / finalBounds.width();
		            float startHeight = startScale * finalBounds.height();
		            float deltaHeight = (startHeight - startBounds.height()) / 2;
		            startBounds.top -= deltaHeight;
		            startBounds.bottom += deltaHeight;
		        }


3. 设置动画并且播放，展示图片
	
			// Hide the view(ImageView) and show the zoomed-in view. When the animation begins,
	
	        viewPager.setVisibility(View.VISIBLE);
	
	        firstClickView.setVisibility(View.INVISIBLE);
	
	        // Set the pivot point for SCALE_X and SCALE_Y transformations to the top-left corner of
	        // the zoomed-in view (the default is the center of the view).
	        viewPager.setPivotX(0f);
	        viewPager.setPivotY(0f);
	
	        // Construct and run the parallel animation of the four translation and scale properties
	        // (X, Y, SCALE_X, and SCALE_Y).
	        // and change the backgroud color
	
	        ObjectAnimator backgroundColor = ObjectAnimator.ofInt(viewPager, "backgroundColor", Color.TRANSPARENT, Color.BLACK);
	
	        backgroundColor.setEvaluator(new ArgbEvaluator());
	
	        AnimatorSet set = new AnimatorSet();
	        set
	                .play(ObjectAnimator.ofFloat(viewPager, View.X, startBounds.left,
	                        finalBounds.left))
	                .with(ObjectAnimator.ofFloat(viewPager, View.Y, startBounds.top,
	                        finalBounds.top))
	                .with(ObjectAnimator.ofFloat(viewPager, View.SCALE_X, startScale, 1f))
	                .with(ObjectAnimator.ofFloat(viewPager, View.SCALE_Y, startScale, 1f))
	                .with(backgroundColor);
	        set.setDuration(mShortAnimationDuration);
	        set.setInterpolator(new DecelerateInterpolator());
	        set.addListener(new AnimatorListenerAdapter() {
	            @Override
	            public void onAnimationEnd(Animator animation) {
	                points.setVisibility(View.VISIBLE);
	                mCurrentAnimator = null;
	                isZooming = false;
	            }
	
	            @Override
	            public void onAnimationCancel(Animator animation) {
	                points.setVisibility(View.GONE);
	                mCurrentAnimator = null;
	                isZooming = false;
	            }
	        });
	        set.start();
	        mCurrentAnimator = set;


## 项目地址 