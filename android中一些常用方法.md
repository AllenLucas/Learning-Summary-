###android中一些常用方法
* 跑马灯效果
* 在布局文件的TextView中添加如下代码
	 ```javascript
android:singleLine="true"   
android:ellipsize="marquee"   
android:focusable="true"  
 android:focusableInTouchMode="true"  
```
	
* ListView滑动下拉效果
	* 创建一个类继承ListView并重写方法；
	 ```javascript
public class MyListView extends ListView {
    public MyListView(Context context) {
        super(context);
    }

    public MyListView(Context context, AttributeSet attrs) {
        super(context, attrs);
    }

    public MyListView(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
    }

    @Override
    protected boolean overScrollBy(int deltaX, int deltaY, int scrollX, int scrollY, int scrollRangeX, int scrollRangeY, int maxOverScrollX, int maxOverScrollY, boolean isTouchEvent) {
        return super.overScrollBy(deltaX, deltaY, scrollX, scrollY, scrollRangeX, scrollRangeY, maxOverScrollX, 100, isTouchEvent);
    }
}； 
```
在layout布局文件中添加的是mylistview而不是ListView；
在最后一个方法中。。倒数第二个设置为100，则成为下拉效果的方式；
* 
