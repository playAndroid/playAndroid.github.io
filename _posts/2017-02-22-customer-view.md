---
layout: post
title: 自定义索引View
date: 2016-02-22
categories: 
tags: [记录]
description: 自定义索引View
---
不论天气如何变化,该撸码还是要撸的.近期打算好好学习一下自定义View的知识.

![这里写图片描述](http://img.blog.csdn.net/20170222225736325?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGF0YV9obGs=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

这是一个自定义的索引条目,虽然网上很多教程,但是纸上来的终觉浅,还是自己写一下.体会深刻,也会学到更多知识.

废话不说,代码以下

```
public class SpeedIndexView extends View {

    private String[] letters = {"A", "B", "C", "D",
            "E", "F", "G", "H",
            "I", "J", "K", "L",
            "M", "N", "O", "P",
            "Q", "R", "S", "T",
            "U", "V", "W", "X",
            "Y", "Z"};
    private Paint paint;//画笔
    private Rect rect;
    private int width;
    private float letterLength;
    private int lastIndex = -1;
    private TouchIndexListener onIndexListener;

    public SpeedIndexView(Context context) {
        this(context, null);
    }

    public SpeedIndexView(Context context, AttributeSet attrs) {
        this(context, attrs, 0);
    }

    public SpeedIndexView(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
        //抗锯齿
        paint = new Paint(Paint.ANTI_ALIAS_FLAG);
        paint.setColor(Color.WHITE);
        //字体
        paint.setTypeface(Typeface.DEFAULT_BOLD);
        paint.setTextSize(DimensUtils.dip2px(context, 16));
        rect = new Rect();
    }

    @RequiresApi(api = Build.VERSION_CODES.LOLLIPOP)
    public SpeedIndexView(Context context, AttributeSet attrs, int defStyleAttr, int defStyleRes) {
        super(context, attrs, defStyleAttr, defStyleRes);
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        //尽量不要做创建对象的操作,防止内存频繁回收,造成界面卡顿
        for (int i = 0; i < letters.length; i++) {
            paint.getTextBounds(letters[i], 0, letters[i].length(), rect);
            float measureText = paint.measureText(letters[i]);//获取字符串的宽度
            float x = width / 2.0f - measureText / 2.0f;
            float y = letterLength + letterLength * i;
            canvas.drawText(letters[i], x, y, paint);
        }
    }

    @Override
    protected void onSizeChanged(int w, int h, int oldw, int oldh) {
        super.onSizeChanged(w, h, oldw, oldh);
        //View的Size变化时被调用
        //在onDraw中无法获得准确的宽高
//        width = getMeasuredWidth();
//        height = getMeasuredHeight();
        width = w;
        Log.d("view", "w" + w + "h" + h + "oldw" + oldw + "oldh" + oldh);
        //每个字符串的高度
        letterLength = h * 1.0f / letters.length;
    }

    @Override
    public boolean onTouchEvent(MotionEvent event) {
        switch (event.getAction()) {
            case MotionEvent.ACTION_DOWN:
                measuerAndWhitch(event);
                break;
            case MotionEvent.ACTION_MOVE:
                measuerAndWhitch(event);
                break;
            case MotionEvent.ACTION_UP:
                lastIndex = -1;
                break;
        }
        return true;
    }

    private void measuerAndWhitch(MotionEvent event) {
        float y = event.getY();
        int index = (int) (y / letterLength);
        Log.d("view", "" + index);
        //与上次触摸不同
        if (lastIndex != index) {
            if (index >= 0 && index < letters.length) {
                if (onIndexListener != null)
                    onIndexListener.onTouchindexListener(letters[index]);
            }
            lastIndex = index;
        }

    }

    public void setOnTouchIndexListener(TouchIndexListener indexListener) {
        this.onIndexListener = indexListener;

    }

    public interface TouchIndexListener {
        void onTouchindexListener(String letter);
    }
}
```

> 1, 继承View,重写3个构造方法,第四个构造方法需要api21以上可以使用,具体每个构造方法先不深究.
> 
> 2, 初始画笔,设置画笔
> 
> 3,在onDraw中,使用canvas.drawText方法,传入内容,x,y坐标,和画笔.需要注意的是这个x和y是字体左下角的坐标,并不是中心点
> 
> 4,要计算出每个字母的位置,可以使用画笔去测量这个字符串的宽度.
> 
> 5,在onDraw中尽量不要创建过多的对象,因为onDraw过程中创建过多的对象,会造成界面的卡顿.
> 
> 6,重写onTouchEvent方法,返回true,拦截事件,处理点击事件和滑动以及抬起事件.
> 
> 7,回调接口,将选中的字符串传递出去,以便调用时对选中的字符串进行其他处理,比如ListView选项.
> 
> Tips:该自定义View可以熟悉自定义View的流程,画笔,画布的使用等.还可以经过修改使其动态显示右侧列表选项,但是要注意在数据返回设置给View之前,不能让View进行显示.否则会产生Null.
