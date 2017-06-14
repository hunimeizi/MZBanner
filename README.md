# MZBannerView 仿魅族Banner
# 总览 </br>

  ![github](https://raw.githubusercontent.com/hunimeizi/MZBanner/master/app/src/main/res/mipmap-xhdpi/mzbanner.png "github")

# 使用方法 </br>



### 自定义属性

	| 属性名      | 属性意义   |  取值  |
	| --------   | -----:   | :----: |
	| open_mz_mode       | 是否开启魅族模式     |   true 为魅族Banner效果，false 则普通Banner效果   |
	| canLoop        | 是否轮播     |   true 轮播，false 则为普通ViewPager   |
	| indicatorPaddingLeft        | 设置指示器距离左侧的距离      |   单位为 dp 的值     |
	| indicatorPaddingRight        | 设置指示器距离右侧的距离     |     单位为 dp 的值  |
	| indicatorAlign        | 设置指示器的位置      |   有三个取值：left 左边，center 剧中显示，right 右侧显示   |

#### 通过`open_mz_mode `和`canLoop `这两个属性来控制MZBannerView 是用作Banner还是普通ViewPager,有4种组合方式**

	1，仿魅族BannerView(默认的模式)
	 java
	app:open_mz_mode="true"
	app:canLoop="true"
 
	2, 普通BannerView
	java
    app:open_mz_mode="false"
    app:canLoop="true"

	3 ,普通ViewPager (有魅族Banner的切换动画)
	java
	app:open_mz_mode="true"
	app:canLoop="false"
 
	4, 普通ViewPager
	java
	app:open_mz_mode="false"
	app:canLoop="false"
		
	
##### 1. xml布局文件

            <mzbannerview.com.mzbanner.view.MZBannerView
                android:id="@+id/banner"
                android:layout_width="match_parent"
                android:layout_height="200dp"
                android:layout_marginTop="10dp"
                app:canLoop="true"
                app:indicatorAlign="center"
                app:indicatorPaddingLeft="10dp"
                app:open_mz_mode="true" />

##### 2. activity中代码：

		 mMZBanner = (MZBannerView) view.findViewById(R.id.banner);
     
        // 设置数据
        mMZBanner.setPages(list, new MZHolderCreator<BannerViewHolder>() {
            @Override
            public BannerViewHolder createViewHolder() {
                return new BannerViewHolder();
            }
        });

		public static class BannerViewHolder implements MZViewHolder<Integer> {
        private ImageView mImageView;
        @Override
        public View createView(Context context) {
            // 返回页面布局
            View view = LayoutInflater.from(context).inflate(R.layout.banner_item,null);
            mImageView = (ImageView) view.findViewById(R.id.banner_image);
            return view;
        }

        @Override
        public void onBind(Context context, int position, Integer data) {
            // 数据绑定
            mImageView.setImageResource(data);
        }
    }

##### 3. 当Banner使用，注意在onResume 中调用start()方法，在onPause中调用 pause() 方法。
		
		@Override
        public void onPause() {
    	    super.onPause();
    	    mMZBanner.pause();//暂停轮播
    	}

    	@Override
    	public void onResume() {
        	super.onResume();
        	mMZBanner.start();//开始轮播
    	}

##### 其他对外API

	/******************************************************************************************************/
    /**                                            对外API                                               **/
    /******************************************************************************************************/
    //开始轮播
     start()
    //停止轮播
     pause()

    //设置BannerView 的切换时间间隔
     setDelayedTime(int delayedTime)
    // 设置页面改变监听器
    addPageChangeLisnter(ViewPager.OnPageChangeListener onPageChangeListener)

    //添加Page点击事件
     setBannerPageClickListener(BannerPageClickListener bannerPageClickListener)
    //设置是否显示Indicator
    setIndicatorVisible(boolean visible)
    // 获取ViewPager
    ViewPager getViewPager()
    // 设置 Indicator资源
    setIndicatorRes(int unSelectRes,int selectRes)
    //设置页面数据
    setPages(List<T> datas,MZHolderCreator mzHolderCreator)
    //设置指示器显示位置
    setIndicatorAlign(IndicatorAlign indicatorAlign)
    //设置ViewPager（Banner）切换速度
    setDuration(int duration)
