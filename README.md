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
