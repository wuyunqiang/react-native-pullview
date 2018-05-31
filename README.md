# PullView
scrollview&amp;&amp;FlatList Pull refresh and loadmore

参考react-native-pull和RefreshListDemo。<br>
android&&ios都可以使用。<br>
# new
android可以使用原生的下拉刷新效果会更好 如下使用：<br>
/**
 * PullScroll => scrollview
 * PullList =>flatlist
 * Key 每一个实例唯一不能重复
 * Android_Native 是否使用android原生下拉刷新组件 true开启
 * ****/
 
如果开启原生属性 需要android引入原生模块
具体建议参考：[RNApp](https://github.com/wuyunqiang/RNApp)<br>
```
       <PullScroll
            Key={'PullScroll'}
            Android_Native={true}//是否使用原生下拉刷新 仅对android生效 iOS无效果
            onPullRelease={this.onPullRelease}
            style={{flex:1,backgroundColor:Color.background}}>
            {this.renderView()}
        </PullScroll>
        
        
        
        <PullList
            Android_Native={true} 
            Key={'list'}//每一个实例不能重复
            ref={(list) => this.pullList = list}
            onEndReachedThreshold={20}
            onPullRelease={this.onPullRelease}
            onEndReached={this.loadMore}
            renderItem={this.renderRowView}
            getItemLayout={(data, index) => ({length:230, offset:230 * index, index})}
            numColumns={1}
            ItemSeparatorComponent={() => {
                return null;
            }}
            initialNumToRender={5}
            renderLoading = {()=>{return null;}}
        />
```


或者参考：[AndroidToRN](https://github.com/wuyunqiang/AndroidToRN)<br>
效果图：<br>
 ![image](https://github.com/wuyunqiang/PullView/raw/master/Images/pullview.gif)
 
![pullviewtoutiao.gif](http://upload-images.jianshu.io/upload_images/3353755-696b57268d529a57.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

使用方式直接拷贝到文件目录下，导入组件即可：
pulllist=>使用flatlist
```
 onPullRelease = (resolve) => {
        //请求数据然后执行 
          this.list && this.list.setData(result);
          resolve()
        }
        
render() {
        return (<PullList
            style={{width: WIDTH,backgroundColor:'#f5f5f5'}}
            ref={(list)=> this.list = list}
            onPullRelease={this.onPullRelease}
            onEndReached={()=>{ this.list&&this.list.addData([]);}}
            renderItem={this.item}
            numColumns={1}
            initialNumToRender={5}
            key={'list'}
        />)}
```
pullview=>使用scrollview
```
 onPullRelease = (resolve) => {
        //请求数据然后执行 
          resolve()
        }
        
    render() {
        return (
            <PullView
                style={{width: WIDTH,backgroundColor:'#f5f5f5'}}
                onPullRelease={this.onPullRelease}
            >
             //一些组件
            </PullView>
        )
    }
```
下拉上拉在iOS上，不会出现空白现象。




