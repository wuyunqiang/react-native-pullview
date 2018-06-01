# PullView
scrollview&amp;&amp;FlatList Pull refresh and loadmore

参考react-native-pull和RefreshListDemo。<br>
android&&ios都可以使用。<br>
# new
android可以使用原生的下拉刷新效果会更好 如下使用：<br>
/**
 * PullScroll => scrollview
 * PullList =>flatlist
 * Android_Native 是否使用android原生下拉刷新组件 true开启
 * ****/
 
如果开启原生属性 需要android引入原生模块<br>
下拉刷新数据传送的方式有两种<br>
### method:1
view实例的方式 Key有没有都可以 也不需要js监听事件 只需要复写onPullRelease即可以使用
debug测试可以使用但是在release模式下会有收不到消息的情况，官方原因并不稳定<br>
### method:2 
原生广播的方式想rn发送数据 ### 因此Key必须有切唯一不重复 ### 需要rn端写事件监听 稳定暂时未发现bug<br>
具体建议参考：[RNApp](https://github.com/wuyunqiang/RNApp)<br>
![iosrnapp.gif](https://upload-images.jianshu.io/upload_images/3353755-e6a3dd8b7f3f54e3.gif?imageMogr2/auto-orient/strip)
![androidgif.gif](https://upload-images.jianshu.io/upload_images/3353755-6dcb27c69b2b345d.gif?imageMogr2/auto-orient/strip)
```
       <PullScroll
            method={2}
            Key={'PullScroll'}
            Android_Native={true}//是否使用原生下拉刷新 仅对android生效 iOS无效果
            onPullRelease={this.onPullRelease}
            style={{flex:1,backgroundColor:Color.background}}>
            {this.renderView()}
        </PullScroll>
        
        
        
        <PullList
            method={2}
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
