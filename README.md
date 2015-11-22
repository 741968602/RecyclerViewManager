# RecyclerViewManager
With RecyclerViewManager supports PullToRefresh and LoadMore, U can also add headers or footers for RecyclerView.
Also supports onItemClickEvent.

![](http://7xn4z4.com1.z0.glb.clouddn.com/RecyclerViewManager.gif)

Layout:

	<space.sye.z.library.widget.RefreshRecyclerView
        android:id="@+id/recyclerView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

Usage in Activity or some others:

	RecyclerViewManager.with(myAdapter, new LinearLayoutManager(this))
                .setMode(RecyclerMode.BOTH)
                .addHeaderView(header)
                .addHeaderView(header2)
                .addFooterView(footer)
                .setOnRefreshListener(new OnBothRefreshListener() {
                    @Override
                    public void onPullDown() {
                        //模拟网络请求
                        Message msg = new Message();
                        msg.what = PULL_DOWN;
                        mHandler.sendMessageDelayed(msg, 2000);
                    }

                    @Override
                    public void onLoadMore() {
                        //模拟网络请求
                        Message msg = new Message();
                        msg.what = LOAD_MORE;
                        mHandler.sendMessageDelayed(msg, 2000);
                    }
                })
                .setOnItemClickListener(new RefreshRecyclerViewAdapter.OnItemClickListener() {
                    @Override
                    public void onItemClick(RecyclerView.ViewHolder holder, int position) {
                        Toast.makeText(MainActivity.this, "item" + position, Toast.LENGTH_SHORT).show();
                    }
                })
                .into(recyclerView, this);
