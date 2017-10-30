# PullView
scrollview&amp;&amp;FlatList Pull refresh and loadmore

参考react-native-pull和react-native-refreshable-flatlist。

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
      
