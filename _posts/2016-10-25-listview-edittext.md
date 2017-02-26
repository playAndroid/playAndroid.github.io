---
layout: post
title: ListView中Item为EditText获取与保存数据
date: 2016-10-25
categories: 
tags: [记录]
description: ListView中Item为EditText获取与保存数据
---
> 近期有个需求需要在ListView中使用EditView填写数据,并且保存到服务器上,而在实现的过程中,确实是遇到了一些坑
> 1,首先数据获取的问题,由于数据在adapter中,要获取所有的数据,并且上传到服务器.
> 2,数据更新的问题,填写完数据,添加一条空item的时候,数据总是对不上.
> 3,每输入一次数据都需要对输入的数据进行网络监察,是否存在数据已上传的情况.
> 4,在获取数据后,要去除重复的数据再上传服务器.

#####以下代码为Adapter中处理点击焦点时,数据实时更新.
```
public class MyListAdapter extends BaseAdapter {

    private final Context mContext;
    private final HashMap<Integer, String> mData;
    private int mTouchItemPosition = -1;
    private OnChangedTextListener onChangedTextListener;
    public MyListAdapter(Context context, HashMap<Integer, String> data) {
        this.mContext = context;
        this.mData = data;
    }

    @Override
    public int getCount() {
        return mData.size();
    }

    @Override
    public Object getItem(int position) {
        return mData.get(position);
    }

    @Override
    public long getItemId(int position) {
        return position;
    }
    
    public HashMap<Integer, String> getmData() {
        return mData;
    }
    
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        ViewHolder viewHolder;
        if (convertView == null) {
            viewHolder = new ViewHolder();
            convertView = LayoutInflater.from(mContext).inflate(R.layout.item_list, null);
            viewHolder.editText = (EditText) convertView.findViewById(R.id.item_edit);
            viewHolder.mTextWatcher = new MyTextChangeWatch();
            //设置数据监听
            viewHolder.editText.addTextChangedListener(viewHolder.mTextWatcher);
            viewHolder.upDataPosition(position);
            convertView.setTag(viewHolder);
        } else {
            viewHolder = (ViewHolder) convertView.getTag();
            viewHolder.upDataPosition(position);
        }
        viewHolder.editText.setText(mData.get(position));
        viewHolder.editText.setTag(position);
        viewHolder.editText.setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch(View v, MotionEvent event) {
            //使用getTag 记录position
                mTouchItemPosition = (int) v.getTag();
                return false;
            }
        });
        /**
         * 解决焦点问题
         * 当editView获取焦点时,listview会重新绘制,致使editView的焦点光标失去
         */
        if (mTouchItemPosition == position) {
            viewHolder.editText.requestFocus();
            viewHolder.editText.setSelection(viewHolder.editText.getText().length());
        } else {
            viewHolder.editText.clearFocus();
        }
        return convertView;
    }

    class ViewHolder {
        EditText editText;
        MyTextChangeWatch mTextWatcher;
		//记录position,防止数据复用时,错乱
        public void upDataPosition(int position) {
            mTextWatcher.upDataPosition(position);
        }
    }

    class MyTextChangeWatch implements TextWatcher {
        private int position;

        public void upDataPosition(int position) {
            this.position = position;
        }

        @Override
        public void beforeTextChanged(CharSequence s, int start, int count, int after) {

        }

        @Override
        public void onTextChanged(CharSequence s, int start, int before, int count) {

        }

        @Override
        public void afterTextChanged(Editable s) {
            mData.put(position, s.toString());
            if(onChangedTextListener !=null){
            //使用回调将数据传递出去,进行数据检测
                onChangedTextListener.onChangedTextListener(position, s.toString());
            }
        }
    }
    public void setOnChangedTextListener(OnChangedTextListener onChangedTextListener) {
        this.onChangedTextListener = onChangedTextListener;
    }
    interface OnChangedTextListener {
        void onChangedTextListener(int position, String str);
    }
}
```

感谢大神的分享,同时在学习的时候要根据个人的项目实际需求进行适当的更改.
参考学习文章:  [Listview结合EditText使用实例中遇到的那些坑](http://www.jb51.net/article/86939.htm)