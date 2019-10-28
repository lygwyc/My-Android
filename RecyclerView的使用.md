# RecyclerView的使用
#Android
- - - -
1. 为app添加依赖
> 在**Add Library Dependency**界面的搜索栏中，键入**androidx.recyclerview**  
![](RecyclerView%E7%9A%84%E4%BD%BF%E7%94%A8/recyclerview%E6%B7%BB%E5%8A%A0%E4%BE%9D%E8%B5%96.png)

2. 在界面布局中引入 recyclerView控件
3. 写数据类
4. 写适配器
> 注意在自定义的适配器类中，还需要自定义一个ViewHolder内部类  
	* 新建一个Java类：FilmAdapter
	* 继承RecyclerView.Adapter
	* 定义一个内部属性List，即数据源
	* 生成一个构造方法，参数为数据源List
	* 定义static内部类ViewHolder，继承RecyclerView.ViewHolder
		* 定义内部类ViewHolder的属性，也就是显示在item中的控件元素
		* 生成内部类ViewHolde的构造方法
```
    static class ViewHolder extends RecyclerView.ViewHolder {
        TextView tvName;
        TextView tvPrice;
        TextView tvDate;

        public ViewHolder(@NonNull View itemView) {
            super(itemView);
            tvName = itemView.findViewById(R.id.item_film_name);
            tvPrice = itemView.findViewById(R.id.item_film_price);
            tvDate = itemView.findViewById(R.id.item_film_date);
        }
    }
```
	* 	修改FilmAdapter，使其继承RecyclerView.Adapter的同时，还要规定其范型为我们此前定义的ViewHolder
```
public class FilmAdapter extends RecyclerView.Adapter<FilmAdapter.ViewHolder>
```
	* 此时，Android Studio会出现红丝波浪线提示，按照提示操作，将会实现三个方法
		* public ViewHolder onCreateViewHolder
			* 利用LayoutInflater.from.inflate方法，生成View
			* 利用View，构造出ViewHolder
			* 将构造生成的ViewHolder，返回
		* public void onBindViewHolder
			* 进行item的内容设置
		* public int getItemCount
			* 返回类FilmAdapter的List的大小
	* 三个实现方法的具体内容如下
```
    @NonNull
    @Override
    public ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View       view       = LayoutInflater.from(parent.getContext()).inflate(R.layout.item_film, parent, false);
        ViewHolder viewHolder = new ViewHolder(view);
        return viewHolder;
    }

    @Override
    public void onBindViewHolder(@NonNull ViewHolder holder, int position) {
        Film film = mFilmList.get(position);
        holder.tvName.setText(film.getName());
        holder.tvPrice.setText(film.getPrice());
        holder.tvDate.setText(film.getDate());

    }

    @Override
    public int getItemCount() {
        return mFilmList.size();
    }
```
5. 在活动中为recyclerview初始化数据、配置布局管理器、适配器
	* 初始化数据
```
initDate();
```
	* 布局管理器
```
LinearLayoutManager layoutManager = new LinearLayoutManager(this);
mRecyclerView.setLayoutManager(layoutManager);
```
	* 初始化适配器
```
mAdapter = new FilmAdapter(mFilmList);
```
	* 设置适配器
```
mRecyclerView.setAdapter(mAdapter);
```