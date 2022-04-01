#### Introduction

> kotlin 作为Android开发的官方语言，可以说标榜的是未来android 的方向。重要程度无需言语，近两年谷歌推出的框架几乎都是基于kotlin 的拓展。

示例1

```kotlin
fun main(){
   print(I like kotlin and I like java too ".")
}
```

示例2

```kotlin
recyclerView.sliver {
            datas = ComponentEnum.values().asList()
            item<ComponentEnum> {
                layoutId = R.layout.item_main_menu
                itemContent = { item, position, holder ->
                               //TODO bind item
                    holder.getView<TextView>(R.id.tv).text = item.title
                }
            }
            itemClick = {viewHolder, position,relalPosition->
                //todo click event
            }
        }
```

示例2同样用java 实现

```java
public class MyAdapter extends RecyclerView.Adapter<MyAdapter.MyViewHolder> {

    @NonNull
    @Override
    public MyViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        return null;
    }

    @Override
    public void onBindViewHolder(@NonNull MyViewHolder holder, int position) {

    }

    @Override
    public int getItemCount() {
        return 0;
    }

    class MyViewHolder extends RecyclerView.ViewHolder{

        public MyViewHolder(@NonNull View itemView) {
            super(itemView);
        }
    }
}

```

很明显，当当一个adapter 的工作量就比过 上方 kotlin 实现。



示例3 

```java
// dp2px in java
SizeUtil.dp2px(context,size)
```

```kotlin
// in kotlin
size.dp
```







由上例子，大概的可以知道，kotlin 是一门 好像有趣，也挺高效的语言。
