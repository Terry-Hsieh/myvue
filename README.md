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
<a v-bind:href="link.src" v-bind:target="link.target">{{ link.content }}</a> #加了v-bind他就會幫我加上那個link了 沒有加他不知道要連動 = 做了template
相等於 <a :href="link.src" :target="link.target">{{ link.content }}</a> #v-bind縮寫就是" : "
```
![](https://raw.githubusercontent.com/Terry-Hsieh/myvue/master/imgstore/4.jpg "xss")
![](https://raw.githubusercontent.com/Terry-Hsieh/myvue/master/imgstore/6.jpg "用物件管理樣式")
![](https://raw.githubusercontent.com/Terry-Hsieh/myvue/master/imgstore/7.jpg "物件管理樣式範例2")

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

### instances & templates
```bash
1. html template + el option #根據life cycle 有el 沒有 template 就去compile html裡的template >>> {{ html }}
   html:
   <p>{{ html }} 1231321</p>
   el:
   <script>
    let vm = new Vue({
            el:'#app',
            data:{
                html:"1231321313",
            },          
        })
    </script>
2. el option + template option(selector) #根據life cycle 有el 有 template 就去render , 會少一層 會只剩<span>  <div>不見ㄌ 整個取代
   顯示:
   <body>
    <div>
        <p>{{ html }} 1231321</p>
    </div>
   </body>
   el+template:
   let vm = new Vue({
            el:'#app',
            template:'<span style="color: red">This {{ msg }} be red.</span>',
            data:{
                msg:'564654 vue',
            },
        })
3. template option(selector) + vm.$mount("#app") #根據life cycle 沒有el 看mount 有mount後 看有沒有template
   templtae設定(沒有el)
   let vm = new Vue({
            template:'#page-tmeplate',
                data:{ 
                    msg:'564654 vue',
             }
    vm.$mount('#app')
    寫script id 對上
    <script type="text/x-template" id="page-tmeplate">
        <span style="color: red">This {{ msg }} be red.</span>
    </script>
```
![](https://raw.githubusercontent.com/Terry-Hsieh/myvue/master/imgstore/5.jpg "lifecycle")

### computed&methods&watch
```bash
如果是資料變動去影響資料,可以往computed去想
methods=>會一直重複執行，呼叫一次就做一次
computed=>資料沒變動,就會做為變數存起來,需求幾次就回傳幾次一樣的.computed cache,對於複雜的好用,資料產生資料 資料觸發資料
watch=>資料產生行為 資料觸發行為,資料連動觸發行為(api去資料庫更新再回傳新的)
***不是說methods就不會連動,只要有呼叫就會連動,因為畫面重新renderㄌ,掃vitural DOM看有沒有需要更新ㄉ***
***methods也可以連動,取決於是不是用在畫面***

物件型寫法
 computed:{
                fullname:{
                    get:function(){
                        return this.firstName + ' ' + this.lastName
                    },
                    set:function(newval){
                        var names = newval.split(' ')
                        this.firstName = names[0]
                        this.lastName = names[names.length - 1]
                    },
                },
 }    
 寫get,set 較複雜的資料盡量不要,切割回送這種也要自己考慮一下
```

### 封裝
```bash
;(function({
 #封裝 用f12看ROOT 可以拿到vue實體
}))
```

