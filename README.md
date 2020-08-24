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
![](https://raw.githubusercontent.com/Terry-Hsieh/myvue/master/imgstore/2.jpg "object.freeze")

### 箭頭function與普通function
```bash
let vm = new Vue({
            el:'#app',
            data,
            // created: function(){     #使用普通function可以拿到vue實體
            //     console.log(this)
            // }
            created: () =>{             #使用箭頭function可以拿到window實體
                console.log(this)
            },
        })
```
![](https://raw.githubusercontent.com/Terry-Hsieh/myvue/master/imgstore/3.jpg "arrowfunction")

### Directives
```bash
<p v-once>{{ msg }}</p> #指定這個DOM只處理預設的第一次，之後不再重新render(文章等等)
<p>{{ html }} 1231321</p> #使用雙大括號可以對內容做組合
<p v-html="html"></p> #會取代掉<p>12313</p> 12313變成vue指定的html值,容易觸發XSS攻擊 ,假設我塞的資料長 test:'<img src="aaa.jpg" onerror="window.alert(`omg`)"/>',
<p v-text="html"></p> #會顯示vue指定的html的字串
```
![](https://raw.githubusercontent.com/Terry-Hsieh/myvue/master/imgstore/4.jpg "xss")

### 陳述/表達式
```bash
function XXX(){
    #陳述式
}

let yyy = function(){
    #表達式
}

全域參數可以在template使用 但是僅限白名單內 像是day1的Date
```

