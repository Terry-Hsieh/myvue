### 一個PCHOME的畫面應該會有那些資料需要創建
```bash
    <script>
        let data ={
            msg:'hello vue'
        }
        let pokemon = {
            img: 'src',
            img:{
                src: 'str',
                alt: 'str'
            },
            title: 'str / html',
            description: 'str / html',
            price: 'number',
            price:{
                type: 'str',
                count: 'number',
            },
            inventory: 'number',   
        }
        let vm = new Vue({
            el:'#app',
            data,
        })
    </script>
```
![](https://raw.githubusercontent.com/Terry-Hsieh/myvue/master/imgstore/1.jpg "picture")

### object freeze
```bash
    <script>
        let data ={
            msg:'hello vue'
        }

        object.freeze(data) #加了object.freeze的話 就沒有相關響應功能了

        let vm = new Vue({
            el:'#app',
            data,
        })
    </script>
```
![](https://raw.githubusercontent.com/Terry-Hsieh/myvue/master/imgstore/2.jpg "picture")
