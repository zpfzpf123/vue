# 001 vue.js初体验

学习网站	https://www.bilibili.com/video/BV15741177Eh/

> ## 1.0 css
>
> ```html
> <div class="test">{{message}}</div>
> ```
>
> 
>
> //**{{}}相当于v-text vue能够识别**
>

## 1.1 vue代码

> ```js
> var test=new Vue({
> 
>       el:'.test',//里面包含了el属性 该属性决定了el挂载到那个元素上
> 
>       data:{
> 
>         message:'hello vue.js'//给挂载的元素内部message赋值
> 
>       }
> 
>     })
> 
>     test.message='hello vue.js 2'//可以改变message的值 页面也会发生改变
> 
> ```
>
> 

![image-20200919100715415](https://gitee.com/zpfzpf123/vue/raw/master/image-20200919100715415.png)

# 002 vue列表(v-for)

## 2.0 css

```css
<div class="test">
        <li v-for="item in movies">{{item}}</li>
    </div>
```



## 2.1 vue代码

> ```js
>     <li v-for="item in movies">{{item}}</li>
> 
>   </ul>
> 
> <script src="./vue.js"></script>
>     <script>
>         new Vue({
>             el:'.a',
>             data:{
>                 movies:['海王','诛仙','星际战警']
>             }
>         })
>     </script>
> ```
>
> 

## 2.3 理解

> v-for="item in movies"的意思是把movies里的每一个元素传给item 
>
> 由于是响应式  故而添加   app.movies.push('微微一笑很倾城') 网页会实时更新
>

## 2.4 v-for遍历数组

- 没有下标的遍历

  	<ul class="a">
	  <li v-for="item in movies">{{item}}</li>
  
	  </ul>



​    

  

- 有下标的遍历

  <ul class="a">
  <li v-for="(item,index) in movies">{{index+1}}:{{item}}</li>
  
  </ul>
  
    <script src="./vue.js"></script>

    <script>


​        <script>


  ​    new Vue({

  ​      el:'.a',

  ​      data:{

  ​        movies:['海王','诛仙','星际战警']

  ​      }

  ​    })

    </script>

  ![image-20200915093612995](https://gitee.com/zpfzpf123/vue/raw/master/image-20200915093612995.png)

  2.5 v-for遍历对象

  代码格式

  v-for="(value,key,index in object)"

  2.6 v-for 加key

  ![image-20200915095637604](https://gitee.com/zpfzpf123/vue/raw/master/image-20200915095637604.png)

  加key的好处是让代码效率更高

  <li v-for="(item,index) in movies" :key="item">{{index+1}}:{{item}}</li>

# 003 事件监听（v-on）

## 3.0 计数器例子

### 3.0.1 代码

<div class="test">
        <h2>count:{{digital}}</h2>
        <button @click="add">+</button>
        <button @click="sub">-</button>
    </div>

const app = new Vue({

​      el: '.test',

​      data:{

​        digital:0

​      },

​      methods: {

​        add:function(){

​          this.digital++;

​          console.log('digital加一');

​        }, 

​        sub:function(){

​          this.digital--;

​          console.log('digital减一');

​        }

​      },

​    })

### 3.0.2理解

> @click="add"（等于v-on:click="add"） 含义为 当点击此事件时 将会执行add   
>
>   methods: {
>
> ​        add:function(){
>
> ​          this.digital++;
>
> ​          console.log('digital加一');
>
> ​        }, 
>
> add在vue里 methods里被定义为函数 点击后将会执行此函数 **注意此处需要用this指正指向app内部 不然会在全局找digital 那样是找不到的**
>

## 3.1 v-on参数问题

> 比如说计数器例子中的**@click="add"** 这里的add函数执行是没有加()的，因为当事件处理时如果不需要参数，
>
> 我们可以不加小括号，如果事件需要参数，比如说 add(aa){
>
> ​            this.a++
>
> ​            console.log(aa);
>
> ​          }而我们加了小括号，那么控制台会提示**undefined**，因为没有传入参数，系统默认为underfined
>
> 如果事件本身需要一个参数，而我们没加小括号，系统会默认传入vue的事件对象
>
> 也就是css:@click="add"
>
> vue:  add(aa){
>
> ​            this.a++
>
> ​            console.log('------'+aa);
>
> ​          }
>
> ![image-20200914163156365](https://gitee.com/zpfzpf123/vue/raw/master/image-20200914163156365.png)
>
> 
>
> 
>
> 如果又需要传入参数，又需要获取event，我们可以这样写
>
> @click="add('123',$event)"
>
> 
>
> methods: {
>
> ​          add(aa,event){
>
> ​            this.a++
>
> ​            console.log('------'+aa+event);
>
> ​          }
>
> ​        },
>
> 当然，如果@click后面不加(),系统会默认第一个参数为event(没有$event时)
>

## 3.2 v-on修饰符

![image-20200914164311983](https://gitee.com/zpfzpf123/vue/raw/master/image-20200914164311983.png)

> 举个例子.stop
>
> 代码如下
>
> <div class="test"@click='wai'>
>     <button @click='li'>1</button>
> </div>
> 
>
>
>  new Vue({
>
> ​      el:'.test',
>
> ​      methods: {
>
> ​        wai(){
>
> ​          console.log('wai');
>
> ​        },
>
> ​        li(){
>
> ​          console.log('li');
>
> ​        }
>
> ​      },
>
> ​    })
>
> 
>
> 运行效果
>
> ![image-20200914165656363](C:\Users\周鹏飞\AppData\Roaming\Typora\typora-user-images\image-20200914165656363.png)
>
> 如果我们把button事件监听改为@click.stop='li'
>
> 我们再来看一下运行效果
>
> ![image-20200914165804766](C:\Users\周鹏飞\AppData\Roaming\Typora\typora-user-images\image-20200914165804766.png)
>
> 这样就能成功阻止冒泡事件的发生
>

# 004 vue生命周期

![img](https://mmbiz.qpic.cn/mmbiz/T0zd7NEbcXSHC2uZ4IBL3icVDvfCwlWv70Z63BDmS2FaaaIL9aVcUY6ysxAHcMIsibfX6HOU30C25ODOeiacNsNPg/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

# 005 vue MVVM

![image-20200911144111305](C:\Users\周鹏飞\AppData\Roaming\Typora\typora-user-images\image-20200911144111305.png

![image-20200911144143439](https://gitee.com/zpfzpf123/vue/raw/master/image-20200911144143439.png)

![image-20200911144111305](https://gitee.com/zpfzpf123/vue/raw/master/image-20200911144111305.png)

# 006 vue插值操作

## 6.0 mustache语法

### 6.0.1代码

<div class="test">
        <h3>{{a+' '+b}}</h3>
        <h3>{{counter*2}}</h3>
    </div>

new Vue({

​      el:'.test',

​      data:{

​        a:'hello',

​        b:'world',

​        counter:100

​      }

​    })

### 6.0.2 解释

{{}}里面可以是两个参数相加 也可以数值计算

## 6.1 v-once

### 6.1.1 代码

 <div class="test">
        <h3>{{a}}</h3>
        <h3 v-once>{{a}}</h3>
    </div>

let app = new Vue({

​      el: '.test',

​      data: {

​        a: 'hello',

​      }

​    })

​    app.a='world'

### 6.1.2 解释

加入v-once后 标签里的值不会随着数据的改变而改变

## 6.2 v-html

### 6.2.1 代码

<div class="test">
        <h3>{{a}}</h3>
        <h3 v-html="a"></h3>
    </div>

 let app = new Vue({

​      el: '.test',

​      data: {

​        a: '<a href="http://www.baidu.com">百度一下</a>',

​      }

​    })

![image-20200911151902082](https://gitee.com/zpfzpf123/vue/raw/master/image-20200911151902082.png)

### 6.2.2 解释

v-html 可以解析字符串使其变为html代码展示出来

## 6.3 v-pre

### 6.3.1 代码

<div class="test">
        <h3>{{a}}</h3>
        <h3 v-pre>{{a}}</h3>
    </div>

let app = new Vue({

​      el: '.test',

​      data: {

​        a: '你好',

​      }

​    })

![image-20200911152530099](https://gitee.com/zpfzpf123/vue/raw/master/image-20200911152530099.png)

### 6.3.2 解释

加入 v-pre的代码不会解析内部语言  是什么就在页面上展示什么

## 6.4 v-cloak

### 6.4.1 代码

<div class="test">
        <h3>{{a}}</h3>
        <h3 v-cloak>{{a}}</h3>
    </div>

let app = new Vue({

​      el: '.test',

​      data: {

​        a: '你好',

​      }

​    })

### 6.4.2  解释

v-cloak作用相当于先解析出来vue代码 再显示到页面上  防止vue代码还没执行成功页面上会显示其它内容

# 007 vue绑定属性(v-bind)

## 7.0 v-bind基本使用

<div class="test">
        <img v-bind:src="a" alt="" srcset="">
    </div>

let app = new Vue({

​      el: '.test',

​      data: {

​        a: 'https://  .sogoucdn.com/2020/09/02/kel7hmnm.jpg',

​      }

​    })

![image-20200911155026584](https://gitee.com/zpfzpf123/vue/raw/master/image-20200911155026584.png)

### 7.0.1 解释

v-bind可以动态绑定数据  如 图片链接src  网站链接href等等

v-bind:src="a"可以简写成 :src="a"

## 7.1 v-bind动态绑定class(对象语法)

### 7.1.1 代码

<!DOCTYPE html>

<html lang="en">



<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Document</title>

</head>

<style>

  .active{

​    color: red;

  }

  .b{

​    color: aquamarine;

  }



</style>

<body>

    <div class="test">

        <div v-bind:class="{active:isactive,b:isb}">

​      {{message}}

​    </div>

​    <button @click='btnclick'>

​      按钮

​    </button>

  </div>

  

    <script src="./vue.js"></script>

    <script>

​    let app = new Vue({

​      el: '.test',

​        data:{

​          message:'hello world',

​          isactive:true,

​          isb:false

​        },

​        methods: {

​          btnclick:function(){

​            this.isactive=!this.isactive

​          }

​      }

​    })

  </script>

</body>



</html>

### 7.1.2 解释

v-bind:class="{active:isactive,b:isb}"   class对象语法  创建一个对象  对象格式为{class:boolean,class:boolean}   

若boolean=true  表示该标签为boolean前的class属性   也就会应用该 class的style

### 7.1.3 补充

v-bind:class="{active:isactive,b:isb}" 可以改为

v-bind:class="getclass()"  然后在vue中添加方法

方法为 methods:{

​		getclass:function(){

​				return "{active:this.isactive,b:this.isb}"

}

}

## 7.2v-bind动态绑定class(数组语法)

### 7.2.1 代码

<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Document</title>

</head>

<body>

    <div class="test" :style="[styles]">

​    {{message}}

  </div>

    <script src="./vue.js"></script>

    <script>

​    new Vue({

​      el:'.test',

​      data:{

​        message:'你好',

​        styles:{

​          backgroundColor:'red',

​          fontSize:'50px'

​        }

​      }

​    })

  </script>

</body>

</html>

### 7.2.2 解释

:style="[styles]"   和 styles:{

​          backgroundColor:'red',

​          fontSize:'50px'

​        }

组成了数组语法  不常用  一般用数组语法

## 7.3 v-bind绑定style

### 7.3.1 代码

<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Document</title>

</head>

<body>

    <div class="test" :style="{fontSize:finalsize}">

​    {{message}}

  </div>

    <script src="./vue.js"></script>

    <script>

​    new Vue({

​      el:'.test',

​      data:{

​        message:'你好',

​        finalsize:'50px'

​      }

​    })

  </script>

</body>

</html>

### 7.3.2 解释

:style="{fontSize:finalsize}" 绑定格式:style="{css类名:css属性值}" **类名使用驼峰命名法**

# 008 v-on v-bind v-for 运用

## 8.0 需求

点击哪一行  哪一行就显示红色 其他行数不显示

## 8.1 代码

<!DOCTYPE html>
<html lang="en">



<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Document</title>

    <style>

​    .colors {

​      color: red;

​    }

  </style>

</head>

<div class="test">

  <ul>

​    <li v-for='(m,index) in movies' @click="btnclick(index)" :class="{colors:index===currentindex}">{{m}}</li>

  </ul>

</div>



<body>

    <script src="./vue.js"></script>

    <script>

​    let app = new Vue({

​      el: '.test',

​      data: {

​        movies:["海王","诛仙","轩辕剑"],

​        currentindex:0

​      },

​      methods: {

​        btnclick:function(index){

​          this.currentindex=index

​        }

​      },

​    })

  </script>

</body>



</html>

## 8.2 解释

:class="{colors:index===currentindex} 如果:index===currentindex 就为true  对应的index行数就会显示为红色

# 009 计算属性（computed）

## 9.0 简单代码例子

<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Document</title>

</head>

<body>

    <div class="test">

​    {{fullname}}

  </div>

    <script src="./vue.js"></script>

    <script>

​    new Vue({

​      el:'.test',

​      data:{

​        beginname:'克里斯蒂亚诺',

​        lastname:'罗纳尔多'

​      },

​      computed: {

​        fullname:function(){

​          return this.beginname+" "+this.lastname

​        }

​      },

​    })

  </script>

</body>

</html>

## 9.1 代码例子

<!DOCTYPE html>
<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Document</title>

</head>

<body>

    <div class="test">

​    总价格:{{fullPrice}}

  </div>

    <script src="./vue.js"></script>

    <script>

​    new Vue({

​      el:'.test',

​      data:{

​        books:[

​          {name:'linux技术',price:110},

​          {name:'java技术',price:117},

​          {name:'计算机组成原理',price:150},

​          {name:'c语言',price:113}

​        ]

​      },

​      computed: {

​        fullPrice:function(){

​          let result=0;

​          for(let i=0;i<this.books.length;i++){

​            result+=this.books[i].price

​          }

​          return result

​        }

​      },

​    })

  </script>

</body>

</html>

### 9.1.1 解释

计算书籍总价格可以用computed进行计算 当然也可以用methods  不过computed可以进行缓存  多次调用只使用一次

  for(let i=0;i<this.books.length;i++) **注意这里别写成i<=this.books.length 不然找不到result**

## 9.2 计算属性的get和set方法

### 9.2.1代码

<div class="test">
    {{fullname}}
</div>

<script src="./vue.js"></script>
    <script>
        const app = new Vue({
            el: '.test',
            data: {
                fistname: '你好',
                lastname: 'vue'
            },
            computed: {
                fullname:{
                    set: function() {
                        console.log('使用·set后调用set函数');
                    },
                    get: function() {
                        return this.fistname+' '+this.lastname
                    }
                }
            }
        })
    </script>

### 9.2.2 解释

computed方法里面包含get与set两种函数  不过我们一般不会设置set函数  故而再写computed函数的时候我们都会省略掉set方法

当set方法如果要被调用

我们可以改变fullname的值 从而调用set函数

![image-20200914104604931](https://gitee.com/zpfzpf123/vue/raw/master/image-20200914104604931.png) 

## 9.3 计算属性和methods的对比

总的来说  computed和methods的根本区别就在于computed可以进行缓存  在重复使用函数时  只会调用一次

而methods使用一次就会调用一次 浪费时间

开发过程中能用computed就用computed

# 010 v-if v-else-if v-else的使用

## 10.1代码

![image-20200914171439004](https://gitee.com/zpfzpf123/vue/raw/master/image-20200914171439004.png)

<div class="test">
        <h1 v-if='score>=90'>优秀</h1>
        <h1 v-else-if='score<90&&score>60'>良好</h1>
        <h1 v-else="score<=60">不及格</h1>
    </div>

new Vue({

​      el:'.test',

​      data:{

​        score:100

​      }

​    })

![image-20200914172229378](https://gitee.com/zpfzpf123/vue/raw/master/image-20200914172229378.png)

### 10.1.1解释

判断和if 		else if		else一样  如果为true 就显示h1里的内容

如果为false 就不显示

## 10.2切换类型小案例

### 代码

 <div class="test">
        <span class="testa" v-if="isuser">
            <label for="a">用户账号</label>
            <input type="number" id="a" placeholder="用户账号">
        </span>
        <span class="testb" v-else>
            <label for="b">用户邮箱</label>
            <input type="email" id="b" placeholder="用户邮箱">
        </span>
        <button @click="isuser=!isuser">切换类型</button>
    </div>
    <script src="./vue.js"></script>
    <script>
        new Vue({
            el:'.test',
            data:{
                isuser:true
            }
        })
    </script>

### 注意

![image-20200915091234478](https://gitee.com/zpfzpf123/vue/raw/master/image-20200915091234478.png)

### 解决方案

加key

<input type="number" id="a" placeholder="用户账号" key="usrname">

<input type="email" id="b" placeholder="用户邮箱" key="useremail">

## 10.3 v-show和v-if的区别

- 用法一样  

区别是v-if为false时对应元素会直接从dom上消失

而v-show为false时知识添加了display:none属性

- ![image-20200915092602684](https://gitee.com/zpfzpf123/vue/raw/master/image-20200915092602684.png)

# 011  购物车的应用

<!DOCTYPE html>

<html lang="en">



<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Document</title>

</head>

<style>

  table {

​    border: 1px solid black;

​    width: 100%;

  }



  td,

  th {

​    border-bottom: 1px solid whitesmoke;

  }



  td {

​    height: 50px;

​    text-align: center;

  }



  span {

​    text-align: center;

​    font-size: 100px;

​    color: green;

​    margin: 0 auto;

​    display: block;

  }

</style>



<body>

    <div class="test">

        <table>

​      <tr>

​        <th>商品名称</th>

​        <th>商品价格</th>

​        <th>数量</th>

​        <th>操作</th>

​      </tr>

​      <tr v-for="xiaomi in xiaomis">

​        <td>{{xiaomi.name}}</td>

​        <td>{{xiaomi.price}}</td>

​        <td>

​          <button v-bind:disabled="xiaomi.count===0" @click="xiaomi.count-=10">-10</button>

​          <button v-bind:disabled="xiaomi.count===0" @click="xiaomi.count-=1">-</button>

​          {{xiaomi.count}}

​          <button @click="xiaomi.count+=1">+</button>

​          <button @click="xiaomi.count+=10">+10</button>

​        </td>

​        <td>

​          <button @click="xiaomi.count=0">移除</button>

​        </td>

​      </tr>

​    </table>

​    <span>总金额:{{values()}}</span>



  </div>

    <script src="./vue.js"></script>

    <script src="../jquery/jquery-3.5.1.min.js"></script>

    <script>

​    var aa = new Vue({

​      el: ".test",

​      data: {

​        xiaomis: [{

​          name: "小米10",

​          price: 3699,

​          count: 0

​        },

​        {

​          name: "小米10pro",

​          price: 4699,

​          count: 0

​        },

​        {

​          name: "小米10至尊纪念版",

​          price: 5299,

​          count: 0

​        }],

​      },

​      methods: {

​        values: function () {

​          var a = 0;

​          for (i = 0; i < this.xiaomis.length; i++) {

​            a += this.xiaomis[i].price * this.xiaomis[i].count;

​          }

​          return a;

​        },

​      },

​    })

  </script>

</body>



</html>

![image-20200915110054864](https://gitee.com/zpfzpf123/vue/raw/master/image-20200915110054864.png)

# 012 v-model双向绑定表单

## 12.0 代码例子

<div class="test">
        <input type="text" v-model="message">
        <h1>{{message}}</h1>
    </div>
    <script src="./vue.js"></script>
    <script>
        new Vue({
            el:'.test',
            data:{
                message:'你好'
            }
        })
    </script>

### 12.0.1 解释

当双向绑定表单之后，无论修改表单的value还是data的值 两个都会同时发生改变

![image-20200915153441809](https://gitee.com/zpfzpf123/vue/raw/master/image-20200915153441809.png)

![image-20200915153523907](https://gitee.com/zpfzpf123/vue/raw/master/image-20200915153523907.png)

## 12.1 v-model结合checkbox radio使用

### 代码（CheckBox）

<div class="radio">
        <label>
            <input type="checkbox" name='a' value="男" v-model='sex'>
            男
        </label>
            <label>
                <input type="checkbox" name='a' value="女" v-model="sex">
               女
            </label>
        <h1>你选择的性别是{{sex}}</h1>
    </div>
    <script src="./vue.js"></script>
    <script>
        new Vue({
            el:'.radio',
            data:{
                sex:[]
            }


        })

### 代码(radio)

div class="radio">

​    <label>

​      <input type="radio" name='a' value="男" v-model='sex'>

​      男

​    </label>

​      <label>

​        <input type="radio" name='a' value="女" v-model="sex">

​        女

​      </label>

​    <h1>你选择的性别是{{sex}}</h1>

  </div>

    <script src="./vue.js"></script>

    <script>

​    new Vue({

​      el:'.radio',

​      data:{

​        sex:''

​      }

​    })

  </script>

### 解释

和radio结合使用时候如果v-model绑定的是同一个属性  那么只能选择一个radio

checkbox可以选择多个

## 12.2 v-model结合select

![image-20200915163624617](https://gitee.com/zpfzpf123/vue/raw/master/image-20200915163624617.png)

加一个multiple就可以实现多选

## 12.3v-model修饰符

![image-20200915165224853](https://gitee.com/zpfzpf123/vue/raw/master/image-20200915165224853.png)

# 013 组件化思想

## 13.0 什么是组件化

![image-20200916083138892](https://gitee.com/zpfzpf123/vue/raw/master/image-20200916083138892.png)

## 13.1 注册组件的基本步骤

![image-20200916084152884](https://gitee.com/zpfzpf123/vue/raw/master/image-20200916084152884.png)

### 13.1.1代码

<div class="test">
<my-cpn></my-cpn>
</div>
<body>
    <my-cpn></my-cpn>

    <script src="./vue.js"></script>
    <script>
        //1 创建组件
        const cpns = Vue.extend({
            template: `
            <div class="a">
            <p>撒大大</p>
            <p>梵蒂冈</p>
            <p>个人复合弓</p>
            </div>
            `
        })
        //注册组件
        Vue.component('my-cpn', cpns)
        new Vue({
            el:'.test'
        })
    </script>


### 13.1.2 解释

首先要是用组件化必须先让vue绑定到相应的元素上，元素内的是能用组件化的范围，

然后使用Vue.extend创建一个组件

然后注册它Vue.component('my-cpn', cpns)    my-cpn是注册的标签名 cpns是创建的组件

最后在范围内使用组件化标签

<my-cpn></my-cpn>

就可以显示我们的组件模板

![image-20200916091439196](https://gitee.com/zpfzpf123/vue/raw/master/image-20200916091439196.png)

## 13.2 全局组件和局部组件

像13.1.1里的例子就是全局组件 

可以在多个vue实例中使用 而局部组件只能在对应的vue实例使用  代码如下

 

```html
new Vue({

      el:'.test',

      components:{

        cpn:cpns

      }

    })

```

cpn就是标签名  cpns就是创建的组件  创建组件可以不写在vue实例中

## 13.3 父子组件

### 代码

<div class="test">
<cpn2></cpn2>
</div>
<body>
    <script src="./vue.js"></script>
    <script>
        //1 创建组件
        const cpns1 = Vue.extend({
            template: `
            <div class="a">
            <p>撒大大</p>
            <p>梵蒂冈</p>
            <p>个人复合弓</p>
            </div>
            `
        })
        const cpns2 = Vue.extend({
            template: `
            <div class="a">
            <p>撒大大</p>
            <p>梵蒂冈</p>
            <cpn1></cpn1>
            <p>个人复合弓</p>
            </div>
            `,
            components:{
                cpn1:cpns1
            }
        })
        //注册组件
        /* Vue.component('my-cpn', cpns */
        new Vue({
            el:'.test',
            components:{
                cpn2:cpns2
            }
        })
    </script>

### 解释

代码之中  我们可以看到cpns1组件在cpns2中被定义    并且应用在了cpns2的template中     

这个时候我们称cpns1为子组件 cpns2为父组件   并且cpns1是不能单独使用的

除非在vue实例中给cpns1注册

## 13.4 全局组件和局部组件的语法糖

### 13.4.1 全局组件语法糖

*//注册组件*

​    Vue.component('my-cpn', {

​      template: `

            <div class="a">

            <p>撒大大</p>

            <p>梵蒂冈</p>

​      <cpn1></cpn1>

            <p>个人复合弓</p>

​      </div>

​      `})

### 13.4.2  局部组件语法糖

 new Vue({

​      el: '.test',

​      components: {

​      'my-cpn': {

​      template: `

            <div class="a">

            <p>撒大大</p>

            <p>梵蒂冈</p>

​      <cpn1></cpn1>

            <p>个人复合弓</p>

​      </div>

​      `}

​      }

​    })

## 13.5 模板分离写法

### 13.5.1 text/template 写法

<div class="test">
        <cpn></cpn>
    </div>
    <script type="text/x-template" id="a">
            <el-divider></el-divider>>
            <p>撒大大</p>
            <p>梵蒂冈</p>
            <cpn1></cpn1>
            <p>个人复合弓</p>
            </div>
    </script>
    <script src="./vue.js"></script>
    <script>
        new Vue({
            el:'.test',
            components:{
            'cpn':{
                template:'#a'
            }
        }
        })
    </script>

### 13.5.2  template写法

 <div class="test">
        <cpn></cpn>
    </div>
    <template id="a">
        <div>
            <p>撒大大</p>
            <p>梵蒂冈</p>
            <cpn1></cpn1>
            <p>个人复合弓</p>
        </div>
    </template>
    <script src="./vue.js"></script>
    <script>
        new Vue({
            el:'.test',
            components:{
            'cpn':{
                template:'#a'
            }
        }
        })
    </script>

## 13.6 组件访问数据

### 13.6.1 组件访问vue属性

![image-20200916105656944](https://gitee.com/zpfzpf123/vue/raw/master/image-20200916105656944.png)

***不能访问***

### 13.6.2 组件数据存放

```html
<div class="test">
        <cpn></cpn>
    </div>
    <template id="a">
        <div>
            <p>撒大大</p>
            {{message}}
            <p>梵蒂冈</p>
            <cpn1></cpn1>
            <p>个人复合弓</p>
        </div>
    </template>
    <script src="./vue.js"></script>
    <script>
        new Vue({
            el:'.test',
            components:{
            'cpn':{
                template:'#a',
                data() {
                    return {
                        message:'组件数据存放在组件里的data函数里的返回值对象中'
                    }
                },
            }
        }
        })
    </script>
```

**组件数据存放在组件里的data函数里的返回值对象中**

- #### 为什么这里的data是一个函数

> ***如果我们多次使用这个组件   调用其中的data   如果data是一个数据  那么当其中一个组件的data发生改变的时候   其它组件也会发生改变***
>
> ***但我们并不想这样  解决方法就是把data变为一个函数  这样没饿组件使用的都是一个独立的data  因为函数是独立的有自己空间的  互不干扰***

## 13.7 父子组件的通信

![image-20200916114401272](https://gitee.com/zpfzpf123/vue/raw/master/image-20200916114401272.png)

### 13.7.1 父组件数据传给子组件(props)

#### 代码

> <!DOCTYPE html>
> <html lang="en">
>
> 
>
> <head>
>
>     <meta charset="UTF-8">
>
>     <meta name="viewport" content="width=device-width, initial-scale=1.0">
>
> <title>Document</title>
>
> </head>
>
> <div class="aa">
> <cpn :messages="message"></cpn>
></div>
> 
><template id="a">
> 
>    <div>
> 
>​    <h2>组件标题</h2>
> 
>        <p>我是组件的内容</p>
> 
>​    <h2>{{messages}}</h2>
> 
></div>
> 
></template>
> 
>
> 
><body>
> 
>    <script src="./vue.js"></script>
> 
>    <script>
> 
>​    const app = new Vue({
> 
>​      el: '.aa',
> 
>​      data: {
> 
>​        message: 'asasas'
> 
>​      },
> 
>​      components: {
> 
>​        'cpn': {
> 
>​          template: '#a',
> 
>​          props: ['messages']
> 
>​        }
> 
>​      }
> 
>​    })
> 
>
> 
></script>
> 
></body>
> 
>
> 
></html>

#### 解释

> 首先new Vue是作为一个父组件的  而cpn是作为一个子组件的
>
> 如果我们想把父组件里面的属性message给我们的子组件使用  不加方法是不能用的  在前面我们已经说到  每个组件都有自己的属性  是不能混为一谈的
>
> 首先我们得给子组件添加props 格式为  props: ['代替父组件属性的元素名']
>
> 然后  在使用组件时 我们这样写<cpn :messages="message"></cpn>  这里的messages就是代替父组件属性的元素名  message就是父组件属性的元素名 
>
> 表示我们把父组件的属性动态绑定到了子组件之中
>
> 这样我们就能在子组件中使用这个父组件的属性了
>
> 这里有个提示：子组件
>
> <template id="a">
>
>     <div>
>
> ​    <h2>组件标题</h2>
>
>         <p>我是组件的内容</p>
>
> ​    <h2>{{messages}}</h2>
>
> </div>
>
> </template>
>
> **这里只能用id作为标识  不能用class  原因不明**



#### props可传入类型

![image-20200916162140469](https://gitee.com/zpfzpf123/vue/raw/master/image-20200916162140469.png)

### 13.7.2 子组件传父组件 this.$emit('自定义事件名',传入的子组件参数)

#### 代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>

<body>

    <!--父组件模板-->
    <div id="app">
        <cpn @clicks='cpnclick'></cpn>
    </div>

    <!--子组件模板-->
    <template id="cpn">
        <div>
            <button v-for="item in categories" @click='btnclick(item)'>
                {{item.name}}
            </button>
        </div>
    </template>

    <script src="./vue.js"></script>
    <script>

        // 1.子组件
        const cpn = {
            template: '#cpn',
            data() {
                return {
                    categories: [
                        { id: 'aaa', name: '热门推荐' },
                        { id: 'bbb', name: '手机数码' },
                        { id: 'ccc', name: '家用家电' },
                        { id: 'ddd', name: '电脑办公' },
                    ]
                }
            },
            methods: {
                btnclick(item) {
                    this.$emit('clicks', item)
                }
            },

        }
        // 2.父组件
        const app=new Vue({
            el: '#app',
            data: {
                message: '你好啊'
            },
            components: {
                cpn
            },
            methods: {
                cpnclick(item) {
                    console.log(item.name);
                }
            }
        })
    </script>

</body>

</html>
```

#### 解释

```html
methods: {

        btnclick(item) {

          this.$emit('clicks', item)

        }

      }

```

```
@click='btnclick(item)'
```

> 子组件添加方法btnclick(item)  然后 this.$emit可以让子组件元素(item)绑定到父组件上   给子组件添加点击事件@click='btnclick(item)'

```
methods: {
                cpnclick(item) {
                    console.log(item.name);
                }
            }
```

> 给父组件添加方法 cpnclick  从而接受从子组件传过来的数据

```html
<!--父组件模板-->
    <div id="app">
        <cpn @clicks='cpnclick'></cpn>
    </div>
```

> 最重要的一步  在父组件模板添加点击事件  把父组件的cpnclick赋值给子组件的clicks  这样就可以实现子传父了

#### 例子2

> 计数器的实现

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="a">
        <cpn @add="change" @sub='change'></cpn>
        <h1>{{message}}</h1>
    </div>
    <template id="test">
        <div>
            <button @click="methodadd">+</button>
            <button @click="methodsub">-</button>
        </div>      
    </template>
    <script src="./vue.js"></script>
    <script>
        let cpn={
            template:'#test',
            methods: {
                methodadd(){    
                    this.digital++             
                    this.$emit('add',this.digital)
                },
                methodsub(){ 
                    this.digital--                 
                    this.$emit('sub',this.digital)
                }
            },
            data() {
                return {
                    digital:0
                }
            },
        }
        new Vue({
            el:'#a',
            data:{
                message:0
            },
            components:{
                cpn
            },
            methods:{
                change(digital){
                    this.message=digital
                },
                
            }
        })
    </script>
</body>

</html>
```

#### 参考图片

![image-20200917095342468](https://gitee.com/zpfzpf123/vue/raw/master/image-20200917095342468.png)

### 13.7.3 最终例子代码(看懂就行 花了半个多小时敲出来)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div class="test">
        <cpn :number1="num1" :number2="num2" @num1change="num1change" @num2change="num2change"
        @changes1="changes1"
        ></cpn>
    </div>
    <template id="a">
        <div>
            <h1>props:{{number1}}</h1>
            <h1>data:{{dnumber1}}</h1>
            <!-- <input type="text" v-model="dnumber1"> -->
            <input type="text" :value="dnumber1" @input="num1input">
            <h1>props:{{number2}}</h1>
            <h1>data:{{dnumber2}}</h1>
            <!-- <input type="text" v-model="dnumber2"> -->
            <input type="text" :value="dnumber2" @input="num2input">
        </div>
    </template>
    <script src="./vue.js"></script>
    <script>
        new Vue({
            el:'.test',
            data:{
                num1:1,
                num2:2
            },
            methods: {
                num1change(value){
                    this.num1=value
                },
                num2change(value){
                    this.num2=value
                },
                changes1(value){
                    this.num2=value*100
                }
            },
            components: {
                cpn:{
                    template:'#a',
                    data() {
                        return {
                            dnumber1:this.number1,
                            dnumber2:this.number2    
                        }
                    },
                    props:{
                        number1:Number,
                        number2:Number
                    },
                    methods:{
                        num1input(event){
                            this.dnumber1=event.target.value,
                            this.$emit('num1change',this.dnumber1)
                            this.$emit('changes1',this.dnumber1)
                            this.dnumber2=this.dnumber1*100
                        },
                        num2input(event){
                            this.dnumber2=event.target.value,
                            this.$emit('num2change',this.dnumber2)
                            this.dnumber1=parseInt(this.dnumber2/2)
                        }
                    }
                }
            }
        })
    </script>
</body>
</html>
```

![01-组件通信案例的画图分析](https://gitee.com/zpfzpf123/vue/raw/master/01-组件通信案例的画图分析.png)

## 13.8 组件之间的访问(不局限于属性  还有对象等)

### 13.8.1 父组件访问子组件



- 代码

  ```html
  
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Title</title>
  </head>
  <body>
  
  <div id="app">
    <cpn></cpn>
    <cpn></cpn>
  
    <my-cpn></my-cpn>
    <y-cpn></y-cpn>
  
    <cpn ref="aaa"></cpn>
    <button @click="btnClick">按钮</button>
  </div>
  
  <template id="cpn">
    <div>我是子组件</div>
  </template>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好啊'
      },
      methods: {
        btnClick() {
          // 1.$children
          // console.log(this.$children);
          // for (let c of this.$children) {
          //   console.log(c.name);
          //   c.showMessage();
          // }
          // console.log(this.$children[3].name);
  
          // 2.$refs => 对象类型, 默认是一个空的对象 ref='bbb'
          console.log(this.$refs.aaa.name);
        }
      },
      components: {
        cpn: {
          template: '#cpn',
          data() {
            return {
              name: '我是子组件的name'
            }
          },
          methods: {
            showMessage() {
              console.log('showMessage');
            }
          }
        },
      }
    })
  </script>
  
  </body>
  </html>
  ```

  **解释**

  > 可以用children或者refs两种方法  推荐使用refs  这样方便我们以后的修改
  >
  > console.log(this.$children)表示输出一个数组 数组里的每个对象就是子组件  里面包含子组件的·各种属性方法等等
  >
  > console.log(this.$refs.aaa.name);
  >
  > <cpn ref="aaa"></cpn>
  >
  > 这种方法更加好  可以直接锁定到具体一个子组件中去，如果用chidren还需要提供键值  而且不方便后期的一个修改
  >
  > 

### 13.8.2 子组件访问父组件

- 代码

  ```html
  
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Title</title>
  </head>
  <body>
  
  <div id="app">
    <cpn></cpn>
  </div>
  
  <template id="cpn">
    <div>
      <h2>我是cpn组件</h2>
      <ccpn></ccpn>
    </div>
  </template>
  
  <template id="ccpn">
    <div>
      <h2>我是子组件</h2>
      <button @click="btnClick">按钮</button>
    </div>
  </template>
  
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好啊'
      },
      components: {
        cpn: {
          template: '#cpn',
          data() {
            return {
              name: '我是cpn组件的name'
            }
          },
          components: {
            ccpn: {
              template: '#ccpn',
              methods: {
                btnClick() {
                  // 1.访问父组件$parent
                  // console.log(this.$parent);
                  // console.log(this.$parent.name);
  
                  // 2.访问根组件$root
                  console.log(this.$root);
                  console.log(this.$root.message);
                }
              }
            }
          }
        }
      }
    })
  </script>
  
  </body>
  </html>
  ```

- 解释

> 在子组件中console.log(this.$parent);这样我们就能访问到我们的父组件
>
> 或者访问根组件$root  这样我们可以访问到最高级最外层的哪一个父组件

## 13.9 插槽(slot)

### 13.9.1 为什么使用插槽

![image-20200918084059277](https://gitee.com/zpfzpf123/vue/raw/master/image-20200918084059277.png)

### 13.9.2 代码(基本使用)

```html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>

<!--
1.插槽的基本使用 <slot></slot>
2.插槽的默认值 <slot>button</slot>
3.如果有多个值, 同时放入到组件进行替换时, 一起作为替换元素
-->

<div id="app">
  <cpn></cpn>

  <cpn><span>哈哈哈</span></cpn>
  <cpn><i>呵呵呵</i></cpn>
  <cpn>
    <i>呵呵呵</i>
    <div>我是div元素</div>
    <p>我是p元素</p>
  </cpn>

  <cpn></cpn>
  <cpn></cpn>
  <cpn></cpn>
  <cpn></cpn>
</div>


<template id="cpn">
  <div>
    <h2>我是组件</h2>
    <p>我是组件, 哈哈哈</p>
    <slot><button>按钮</button></slot>
    <!--<button>按钮</button>-->
  </div>
</template>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    components: {
      cpn: {
        template: '#cpn'
      }
    }
  })
</script>

</body>
</html>
```

### 13.9.3 解释

> 在模板里面加入插槽 <slot></slot>
>
> 后面使用模板标签的时候  我们可以在标签里插入我们想要的东西
>
> 比如 插入一个
>
> <cpn><span>哈哈哈</span></cpn>
>
> 插入多个
> <cpn>
>     <i>呵呵呵</i>
>
>     <div>我是div元素</div>
>     <p>我是p元素</p>
>   </cpn>
>
> 如果标签里不插入   而插槽里有默认属性  比如
>
> <slot><button>按钮</button></slot>
>
> 那么标签会自动显示插槽里的内容

### 13.9.4 具名插槽(添加name属性)

- 代码

  ```
  
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Title</title>
  </head>
  <body>
  
  <div id="app">
    <cpn><span slot="center">标题</span></cpn>
    <cpn><button slot="left">返回</button></cpn>
  </div>
  
  
  <template id="cpn">
    <div>
      <slot name="left"><span>左边</span></slot>
      <slot name="center"><span>中间</span></slot>
      <slot name="right"><span>右边</span></slot>
    </div>
  </template>
  
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好啊'
      },
      components: {
        cpn: {
          template: '#cpn'
        }
      }
    })
  </script>
  
  </body>
  </html>
  ```

  

- 解释

  当给插槽添加name后 就可以在指定插槽里添加内容 

  如

  ```
  <div>
      <slot name="left"><span>左边</span></slot>
      <slot name="center"><span>中间</span></slot>
      <slot name="right"><span>右边</span></slot>
    </div>
  ```

  ```
  <cpn><button slot="left">返回</button></cpn>
  ```

  因为名字都是left 所以值会改变成左边  其它的标签内容不改变

# 014 编译作用域

- 代码

```

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>

<div id="app">
  <cpn v-show="isShow"></cpn>
  <cpn v-for="item in names"></cpn>
</div>

<template id="cpn">
  <div>
    <h2>我是子组件</h2>
    <p>我是内容, 哈哈哈</p>
    <button v-show="isShow">按钮</button>
  </div>
</template>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      isShow: true
    },
    components: {
      cpn: {
        template: '#cpn',
        data() {
          return {
            isShow: false
          }
        }
      },
    }
  })
</script>

</body>
</html>
```

- 解释

>  <cpn v-show="isShow"></cpn>这里的isshow在子组件的isshow还是父组件的isshow？
>
> 答案是父组件  我们找isshow的作用域是**看它的父元素的指向 而不是看标签**
>
> 这里父元素<div id="app">是vue的实例
>
> 所以我们应该去vue的data里找isshow 这里的isshow为true 故而网页上能显示<cpn></cpn>

- 作用域插槽

![image-20200918113508487](https://gitee.com/zpfzpf123/vue/raw/master/image-20200918113508487.png)

```html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>

<div id="app">
  <cpn></cpn>

  <cpn>
    <!--目的是获取子组件中的pLanguages-->
    <template slot-scope="slot">
      <!--<span v-for="item in slot.data"> - {{item}}</span>-->
      <span>{{slot.data.join(' - ')}}</span>
    </template>
  </cpn>

  <cpn>
    <!--目的是获取子组件中的pLanguages-->
    <template slot-scope="slot">
      <!--<span v-for="item in slot.data">{{item}} * </span>-->
      <span>{{slot.data.join(' * ')}}</span>
    </template>
  </cpn>
  <!--<cpn></cpn>-->
</div>

<template id="cpn">
  <div>
    <slot :data="pLanguages">
      <ul>
        <li v-for="item in pLanguages">{{item}}</li>
      </ul>
    </slot>
  </div>
</template>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    components: {
      cpn: {
        template: '#cpn',
        data() {
          return {
            pLanguages: ['JavaScript', 'C++', 'Java', 'C#', 'Python', 'Go', 'Swift']
          }
        }
      }
    }
  })
</script>


</body>
</html>
```

# 015 模块化

> ## 15.1 普通方法
>
> 如果html里面要导入多个js  我们就会发现一些问题  比如两个js文件里有些全局变量命名一样  这样就会导致之后再使用这个全局变量的时候可能和我们预设的值不太一样
>
> 解决方式
>
> ![image-20200918143449942](https://gitee.com/zpfzpf123/vue/raw/master/image-20200918143449942.png)

> 我们可以使用闭包函数去除这种问题 

## 15.2 commonjs

![image-20200918144355680](https://gitee.com/zpfzpf123/vue/raw/master/image-20200918144355680.png)

## 15.3 module

- 代码

**index.html**

```

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>

<script src="aaa.js" type="module"></script>
<script src="bbb.js" type="module"></script>
<script src="mmm.js" type="module"></script>
</body>
</html>
```

**aaa.js**

```
var name = '小明'
var age = 18
var flag = true

function sum(num1, num2) {
  return num1 + num2
}

if (flag) {
  console.log(sum(20, 30));
}

// 1.导出方式一:
export {
  flag, sum
}

// 2.导出方式二:
export var num1 = 1000;
export var height = 1.88


// 3.导出函数/类
export function mul(num1, num2) {
  return num1 * num2
}

export class Person {
  run() {
    console.log('在奔跑');
  }
}

// 5.export default
// const address = '北京市'
// export {
//   address
// }
// export const address = '北京市'
// const address = '北京市'
//
// export default address

export default function (argument) {
  console.log(argument);
}







```

**bbb.js**

```
import {sum} from './aaa.js'

var name = '小红'
var flag = false

console.log(sum(100, 200));

```

**mmm.js**

```html
// 1.导入的{}中定义的变量
import {flag, sum} from "./aaa.js";

if (flag) {
  console.log('小明是天才, 哈哈哈');
  console.log(sum(20, 30));
}

// 2.直接导入export定义的变量
import {num1, height} from "./aaa.js";

console.log(num1);
console.log(height);

// 3.导入 export的function/class
import {mul, Person} from "./aaa.js";

console.log(mul(30, 50));

const p = new Person();
p.run()

// 4.导入 export default中的内容
import addr from "./aaa.js";

addr('你好啊');

// 5.统一全部导入
// import {flag, num, num1, height, Person, mul, sum} from "./aaa.js";

import * as aaa from './aaa.js'

console.log(aaa.flag);
console.log(aaa.height);

```

> - **解释**
>
> 如上述代码所示 导出的方式有好几种 其中export default我们需要注意一下
>
> ![image-20200918161217359](https://gitee.com/zpfzpf123/vue/raw/master/image-20200918161217359.png)

> 导入的时候如果导出的数据太多，我们可以用这种方式来解决
>
> ```
> import * as aaa from './aaa.js'
> 
> console.log(aaa.flag);
> ```

# 016 webpack的使用

## 16.0 webpack打包简单例子

webpack可以把我们多个js文件打包成一个js 左后我们可以应用这个新生成的js文件  可以解决模块化问题  因为它在打包的时候会自动将模块化语言解析成浏览器能够认识的语言 不需要我们处理

- 安装webpack前需要安装node.js 然后执行npm install webpack --save-dev
-  --save就是保存到package.json里面 -dev就表示开发时使用这个包而生产环境不使用这个包
- ![image-20200919170108547](https://gitee.com/zpfzpf123/vue/raw/master/image-20200919170108547.png)



![image-20200919141934784](https://gitee.com/zpfzpf123/vue/raw/master/image-20200919141934784.png)

## 16.1 webpack打包配置

> 在前面打包的例子我们可以看到我们是在终端执行了![image-20200919152617108](https://gitee.com/zpfzpf123/vue/raw/master/image-20200919152617108.png)这样一条命令
>
> 不过这有点麻烦，我们可以这样来做
>
> 1.建立这个文件
>
> webpack.config.js
>
> 2.在终端输入这条命令
>
> ```
> npm init -y //初始化本地仓库 生成package.json
> ```
>
> 3.配置 webpack.config.js
>
> ```
> const path=require('path');//path是node里的 这里默认添加
> module.exports={
>   entry:"./src/math.js",//需要打包的文件路径
>   output:{
>     path:path.resolve(__dirname,'./disk'),//__dirname是node里的 默认添加  ./disk是你要打包到那个文件夹里去
>     filename:"bundle.js"//打包后的名称
>   }
> }
> ```
>
> 4.终端执行
>
> ```
> webpack/npm run build //(要执行npm run build必须在package.js里添加 "scripts": {
>   	build:webpack
>   })
> ```
>
> 5.注意
>
> 有时候我们需要用到别人的打包文件 如果两者的webpack版本不同会导致出错
>
> 我们也有解决办法
>
> 首先 我们要知道 在终端执行webpack是执行的全局webpack 而不是局部的 
>
> 我们可以在终端输入以下代码
>
> ```
> npm install webpack@对应的版本号 --save-dev
> ```
>
> 然后在package.js中添加
>
> ```
> "scripts": {
>   	build:webpack
>   	}
> ```
>
> 最后在终端执行就会执行本地配置的webpack
>
> ```
> npm run build
> ```
>
> 当然你也可以直接在终端执行你刚下载的本地webpack的相对路径 如
>
> ```
> ./src/webpack
> ```

## 16.2 webpack-loader

### 16.2.1 什么是loader

![image-20200919154908864](https://gitee.com/zpfzpf123/vue/raw/master/image-20200919154908864.png)

### 16.2.2 css-loader和style-loader的下载与使用

下载与配置官网很详细

- style-loader https://www.webpackjs.com/loaders/style-loader/
- css-loader    https://www.webpackjs.com/loaders/css-loader

如下

```
const path=require('path');
module.exports={
  entry:"./src/main.js",
  output:{
    path:path.resolve(__dirname,'./disk'),
    filename:"bundle.js"
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['style-loader','css-loader']
      }
    ]
  }
}
```

然后main.js导入css文件

```
require("./css/normal.css")
```

最后再npm run build 就可以实现css代码打包

- 注意   use: ['style-loader','css-loader']的读取顺序是从右到左的

### 16.2.3 less-loader和less的下载

- 见官网 	https://www.webpackjs.com/loaders/less-loader/

### 16.2.4 url-loader和file-loader

#### 16.2.4.1 图片配置

如下

```
{
      test: /\.(png|jpg|gif)$/,
      use: [
        {
          loader: 'url-loader',
          options: {
            limit: 8192//图片文件代销如果超过8192b 就不用url-loader  使用file-loader  小于8192b 就会使用url-loader 对图片进行base64编码
          }
        }
      ]
    }
```

- 注意  使用file-loader 后  直接运行是不会显示图片的 我们还需要这样做 在webpack.config.js文件里面的output添加公共路径

(也就是使用file-loader后生成新的编码的图片路径)如

```
publicPath: 'disk/'
```

- 这个时候再运行就没有问题了

#### 16.2.4.2 图片文件处理(系统生成的图片名字太长 不易找到源文件)

- 如下

![image-20200921093600303](https://gitee.com/zpfzpf123/vue/raw/master/image-20200921093600303.png)

- 代码

```
options: {
            limit: 8192,
            name:'img/[name].[hash:8].[ext]'//在disk文件夹下创建一个img文件夹 [name]是编码前的图片名 [hash:8]添加8位hash码 防止图片名字重复 [.ext]保留原有的扩展名
          },
```

- 效果展示

![image-20200921094225805](https://gitee.com/zpfzpf123/vue/raw/master/image-20200921094225805.png)



### 16.2.5 ES6转ES5语法

- 如下

![image-20200921095936769](https://gitee.com/zpfzpf123/vue/raw/master/image-20200921095936769.png)

- 目前基本所有的浏览器都支持ES6语法 只有少数的浏览器不支持 为了满足少数的浏览器 我们就可以使用这样的插件

## 16.3 webpack使用Vue的配置

- 下载Vue

输入指令

```
npm install vue@版本号 --save
```

- 我们安装好以后在 js文件里写入

```
import Vue from 'vue'
const app=new Vue({
  el:"#a",
  data:{
    message:"hello world"
  }
})
```

- 再在html文件写入

```
<div id="a">
    {{message}}
  </div>
```

- 最后运行 我们会发现没有显示 控制台会报错

![image-20200921144600150](https://gitee.com/zpfzpf123/vue/raw/master/image-20200921144600150.png)

- 解决办法

１.因为我们在引用Vue时 系统默认是runtime-only版本 如图所示

![image-20200921144758029](https://gitee.com/zpfzpf123/vue/raw/master/image-20200921144758029.png)

２.要想变成第二种版本 我们需要在 webpack.config.js文件里面这样配置 在module.exports里面添加

```
resolve:{
      alias: {
        'vue$':'vue/disk/vue.esm.js'//找到vue.esm.js文件的路径
      }
    }
```

3.我们再次运行 问题解决

## 16.4 webpack使用Vue

1. 在写Vue代码我们不希望频繁改动index.html代码

2. 我们可以这样解决 在new vue里弥漫添加template模板

   如下

   ```
   const app=new Vue({
     el:"#a",
     data:{
       message:"hello world"
     },
     template:
     `<h1>{{message}}</h1>`
   })
   ```

   最后也能在浏览器运行成功

3. 最终方案

1. 创建一个vue文件 如下

```vue
<template>
  <div>
    <h1 class="aa">{{message}}</h1>
  </div>
</template>

<script>
  export default {
    name:"App",
    data() {
      return {
        message:"hello world"
      }
    },
  }
</script>

<style scoped>
.aa{
  color: cornflowerblue;
}
</style>
```

2.在js文件里导入vue

```vue
import App from '../vue/App.vue'
new Vue({
  el:"#a",
  template:'<app></app>',
  components:{
    App
  }
})
```

3.下载vue-loader和vue-template-compiler(注意版本兼容)

```
npm install vue-loader vue-template-compiler --save-dev
```

4.运行成功

## 16.5 webpack插件plugin

- 认识插件

  ![image-20200922145025263](https://gitee.com/zpfzpf123/vue/raw/master/image-20200922145025263.png)

### 1.添加版权声明

![image-20200922145816271](https://gitee.com/zpfzpf123/vue/raw/master/image-20200922145816271.png)

### 2.打包html的plugin

![image-20200922150509938](https://gitee.com/zpfzpf123/vue/raw/master/image-20200922150509938.png)

### 3.js压缩的plugin

![image-20200922151945631](https://gitee.com/zpfzpf123/vue/raw/master/image-20200922151945631.png)

### 4.搭建本地的服务器

![image-20200922152459867](https://gitee.com/zpfzpf123/vue/raw/master/image-20200922152459867.png)

# 017 Vue cli(脚手架)的使用

## 17.1 什么是脚手架

![image-20200922170401734](https://gitee.com/zpfzpf123/vue/raw/master/image-20200922170401734.png)

## 17.2 cnpm的安装

![image-20200922171032696](https://gitee.com/zpfzpf123/vue/raw/master/image-20200922171032696.png)

![image-20200922171049149](https://gitee.com/zpfzpf123/vue/raw/master/image-20200922171049149.png)

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

## 17.3 脚手架的安装

- 见官网	https://cli.vuejs.org/zh/guide/installation.html

  ```
  cnpm install -g @vue/cli
  ```

  

- 拉取旧版本 https://cli.vuejs.org/zh/guide/creating-a-project.html#%E4%BD%BF%E7%94%A8%E5%9B%BE%E5%BD%A2%E5%8C%96%E7%95%8C%E9%9D%A2

```bash
npm install -g @vue/cli-init
```

- vue-cli2和vue-cli3生成项目

![image-20200922173718402](https://gitee.com/zpfzpf123/vue/raw/master/image-20200922173718402.png)

- vue-cli2详解

![image-20200923082305805](https://gitee.com/zpfzpf123/vue/raw/master/image-20200923082305805.png)

- 目录结构详解

![image-20200923091123371](https://gitee.com/zpfzpf123/vue/raw/master/image-20200923091123371.png)

- vue-cli3的配置

![image-20200923110346708](https://gitee.com/zpfzpf123/vue/raw/master/image-20200923110346708.png)

## 17.4 runtime-compiler和runtime-only的区别

- vue程序运行过程

  ![image-20200923104355775](https://gitee.com/zpfzpf123/vue/raw/master/image-20200923104355775.png)

- runtime-compiler

template-->ast-->render-->virtual dom-->ui

- runtime-only

render-->virtual dom-->ui

- runtime-only运行速度更快 代码更少

- 二者区别在于main.js

- runtime-compiler的main.js

  ```js
  // The Vue build version to load with the `import` command
  // (runtime-only or standalone) has been set in webpack.base.conf with an alias.
  import Vue from 'vue'
  import App from './App'
  
  Vue.config.productionTip = false
  
  /* eslint-disable no-new */
  new Vue({
    el: '#app',
    components: { App },
    template: '<App/>'
  })
  
  ```

  runtime-only的main.js

  ```js
  import Vue from 'vue'
  import App from './App'
  
  Vue.config.productionTip = false
  
  /* eslint-disable no-new */
  new Vue({
    el: '#app',
    render: h => h(App)
  })
  
  ```

- render函数可以直接跳过template-->ast的过程直接渲染 效率更快

## 17.5 ui的启动(查看配置文件)

- 输入指令

```
vue ui
```

- 可以在这里修改一些配置 或者启动或者打包都可以 甚至还可以创建vue脚手架 是一个可视化的图形界面

## 17.6 vue-router(路由的使用)

### 17.6.1什么是路由

![image-20200923153941960](https://gitee.com/zpfzpf123/vue/raw/master/image-20200923153941960.png)

### 17.6.2前端渲染与后端渲染  前端路由与后端路由

![01-后端路由阶段](https://gitee.com/zpfzpf123/vue/raw/master/01-后端路由阶段.png)

![](https://gitee.com/zpfzpf123/vue/raw/master/01-后端路由阶段.png)

![03-SPA页面页面的阶段](https://gitee.com/zpfzpf123/vue/raw/master/03-SPA页面页面的阶段.png)

![04-前端路由中url和组件的关系](https://gitee.com/zpfzpf123/vue/raw/master/04-前端路由中url和组件的关系.jpg)

### 17.6.3 url的hash和html5的history模式

- hash模式(页面不会刷新)

![image-20200923165816649](https://gitee.com/zpfzpf123/vue/raw/master/image-20200923165816649.png)

- history模式(页面也不会刷新)

1. ![image-20200923170135105](https://gitee.com/zpfzpf123/vue/raw/master/image-20200923170135105.png)
2. ![image-20200923170223374](https://gitee.com/zpfzpf123/vue/raw/master/image-20200923170223374.png)
3. ![image-20200923170318338](https://gitee.com/zpfzpf123/vue/raw/master/image-20200923170318338.png)

### 17.6.4 vue-router的使用

- 首先配置路由

![image-20200923184235658](https://gitee.com/zpfzpf123/vue/raw/master/image-20200923184235658.png)

- 首先在components创建两个vue

- page.vue


```js
<template>
  <div>
    <h1>我是首页</h1>
    <h2>sdsfsaf</h2>
  </div>
</template>
<script>
  export default {
    name:'page'
  }
</script>
<style>

</style>

```

- Pages.vue


```js
<template>
  <div>
    <h1>我是首页2</h1>
    <p>sdasdswd</p>
  </div>
</template>
<script>
  export default {
    name:'Pages'
  }
</script>
<style>

</style>

```

- 在router里的index.js添加配置


```js
import Vue from 'vue'
import Router from 'vue-router'
import page from '../components/page.vue'
import Pages from '../components/Pages.vue'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/page',
      component: page
    },
    {
      path:'/Pages',
      component: Pages
    }
  ]
})

```

- 在main.js引入路由


```js
import Vue from 'vue'
import App from './App.vue'
import router from './router'

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  render: h => h(App)
})

```

- 在App.vue展示


```js
<template>
  <div id="app">
    <router-link to="./page">shouye</router-link>
    <router-link to="./Pages">附页</router-link>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App',

}
</script>

<style>

</style>

```

### 17.6.5 路由的默认路径

- 我们如果想改变默认路径，也就是进入网站能展示router-view的内容 我们可以这样做

在router下的index.js中配置

```js
const routes[
	{
		path:'',		//默认路径
  	redirect:'/page'		//重定向 进入网站默认的路径
	}
]
```

### 17.6.6 修改默认路径模式为html5的history模式

- 在index.js添加mode:'history'

```json
import Vue from 'vue'
import Router from 'vue-router'
import page from '../components/page.vue'
import Pages from '../components/Pages.vue'
import normal from '../components/normal.vue'


Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/page',
      component: page
    },
    {
      path:'/Pages',
      component: Pages
    },
    {
      path:'/normal',
      component:normal
    },
    {
      path:'',
      redirect:'/page'
    }
  ],
  mode:'history'
})

```

### 17.6.7 router-link的补充

![image-20200924142847064](https://gitee.com/zpfzpf123/vue/raw/master/image-20200924142847064.png)

- 如下

```
<template>
  <div id="app">
    <router-link to="./page" tag="button" replace active-class='active'>shouye</router-link>
    <router-link to="./Pages" replace>附页</router-link>
    <router-link to="./normal" replace>normal页</router-link>
    <router-view></router-view>
  </div>
</template>

```

![](https://gitee.com/zpfzpf123/vue/raw/master/image-20200924143612630.png)

### 17.6.8	通过代码跳转路由

- 代码如下

```js
<template>
  <div id="app">
    <button @click="pageclick">首页</button>
    <button @click="pagesclick">附页</button>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App',
  methods: {
    pageclick(){
      this.$router.push('./page')
    },
    pagesclick(){
      this.$router.push('./Pages')
    }
  },
}
</script>

<style>
.active{
  color:rgba(0, 255, 13, 0.541)
}
</style>

```

- 通过绑定两个button来进行跳转路由
- 在pageclick和pagesclick上面添加this.$router.push('路由路径')进行跳转
- 当然可以用push()，自然也可以用replace() 其它同理

### 17.6.9 动态路由

- 为什么要使用动态路由

![image-20200924201031189](https://gitee.com/zpfzpf123/vue/raw/master/image-20200924201031189.png)

- 使用方法 代码如下 App.vue

```js
<template>
  <div id="app">
    <router-link to="/page" tag="button" >shouye</router-link>
    <router-link to="/Pages" tag="button">附页</router-link>
    <router-link :to=" '/normal/' +zpf">normal</router-link>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      zpf:'zhoupengfei'
    }
  },
}
</script>

<style>

</style>

```

- normal.vue

```js
<template>
  <div>
    <p>我是normal</p>
    {{message}}
    <p>{{zpf}}</p>
  </div>
</template>

<script>
  export default {
    name:'normal',
    data() {
      return {
        message:'你好我是message'
      }
    },
    computed: {
      zpf(){
        return this.$route.params.zpf
      }
    },
  }
</script>

<style>
  p{
    color: red;
  }
</style>

```

- index.js

```js
import Vue from 'vue'
import Router from 'vue-router'
import page from '../components/page.vue'
import Pages from '../components/Pages.vue'
import normal from '../components/normal.vue'


Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/page',
      component: page
    },
    {
      path:'/Pages',
      component: Pages
    },
    {
      path:'/normal/:zpf',
      component:normal
    },
  ],
  mode:'history'
})

```

- 首先在index.js里面添加如下代码(表示normal后面多了一个变量zpf)

```js
{
      path:'/normal/:zpf',
      component:normal
    },
```

- 在normal.vue中添加代码(表示返回活跃路由器的变量名zpf)

```js
 computed: {
      zpf(){
        return this.$route.params.zpf
      }
    },
```

- 最后在App.vue中显示 效果如下

![image-20200924205946880](https://gitee.com/zpfzpf123/vue/raw/master/image-20200924205946880.png)

### 17.6.10 vue-router打包文件的分析

- #### 打包文件分析

![image-20200925091141098](https://gitee.com/zpfzpf123/vue/raw/master/image-20200925091141098.png)

如图所示

- app.css把所有的css代码整合到了一起
- app.js包括了我们写的所有业务代码
- vendor.js包括了我们使用的所有第三方 比如 vue vue-router
- mainifest.js包括了所有为我们底层做支撑的代码

### 17.6.11 认识路由的懒加载

- #### 认识路由的懒加载

> 我们知道 webpack会帮我们把多个文件进行打包  最后渲染出来 但是这样做会导致包过大  渲染速度慢	我们可以把路由分为不同的模块进行分割 当路由被访问的时候 才加载相应的组件 从而提高加载速度

- #### 路由懒加载的使用

![image-20200925092721518](https://gitee.com/zpfzpf123/vue/raw/master/image-20200925092721518.png)

- #### 懒加载的方式

![image-20200925093008977](https://gitee.com/zpfzpf123/vue/raw/master/image-20200925093008977.png)

**我采用方式三**

- 代码如下

```js
const page=()=>import('../components/page.vue')
const Pages=()=>import('../components/Pages.vue')
const normal=()=>import('../components/normal.vue')
```

- 重新打包我们会发现多了几个js打包的代码 这几个js代码就是懒加载的代码 当我们触发到相应的路由的时候 对应的js代码才会执行 

### 17.6.12 嵌套路由的使用

#### 认识嵌套路由

![image-20200925095310838](https://gitee.com/zpfzpf123/vue/raw/master/image-20200925095310838.png)

#### 使用嵌套路由

- 创建两个子组件如下
- normalnew.vue

```vue
<template>
  <div>
    <ul>
      <li>消息1</li>
      <li>消息2</li>
      <li>消息3</li>
      <li>消息4</li>
    </ul>
  </div>
</template>
<script>
  export default {
    name:'normalnew'
  }
</script>
<style>

</style>

```

- normalmy.vue

```vue
<template>
  <div>
    <ul>
      <li>1我的</li>
      <li>2我的</li>
      <li>3我的</li>
      <li>4我的</li>
    </ul>
  </div>
</template>
<script>
  export default {
    name:'normalmy'
  }
</script>
<style>

</style>

```

- 在index.js注册子组件

```js
import Vue from 'vue'
import Router from 'vue-router'
/* import page from '../components/page.vue'
import Pages from '../components/Pages.vue'
import normal from '../components/normal.vue' */
const page=()=>import('../components/page.vue')
const Pages=()=>import('../components/Pages.vue')
const normal=()=>import('../components/normal.vue')
const normalnew=()=>import('../components/normalnew.vue')
const normalmy=()=>import('../components/normalmy.vue')
Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/page',
      component: page
    },
    {
      path:'/Pages',
      component: Pages
    },
    {
      path:'/normal',
      component:normal,
      children:[
        {
          path:'',
          redirect:'normalnew'
        },
        {
          path:'normalnew',
          component:normalnew
        },
        {
          path:'normalmy',
          component:normalmy
        }
      ]
    },
  ],
  mode:'history'
})

```

- 在normal.vue里应用子组件

```vue

+
+<template>
  <div>
    <p>我是normal</p>
    <p>{{message}}</p>
    <router-link to="/normal/normalnew">新闻</router-link>
    <router-link to="/normal/normalmy">我的</router-link>
    <router-view></router-view>
  </div>
</template>

<script>
  export default {
    name:'normal',
    data() {
      return {
        message:'你好我是message'
      }
    },
  }
</script>

<style>
  p{
    color: red;
  }
</style>

```

- 展示效果如下

![image-20200925103242319](https://gitee.com/zpfzpf123/vue/raw/master/image-20200925103242319.png)

### 17.6.13 vue-router的参数传递

#### 参数传递的方式

![image-20200925171042389](https://gitee.com/zpfzpf123/vue/raw/master/image-20200925171042389.png)

- params前面已经提到过  query写法如下

```js
<router-link :to="{path:'/normal',query:{name:18,height:188}}">normal</router-link>
```

- 我们也可以这样写

```js
<button @click='normalclick'>normal</button>
```

```js
 normalclick(){
      this.$router.push({
        path:'/normal',
        query:{
          name:'zpf',
          age:21,
          height:188
        }
      })
    }
```

### 17.6.14	$router和$route的区别

`Vue Router`是`Vue.js`的路由管理器，路由就是`SPA`单页应用的访问路径，在`Vue`实例内部，可以通过`$router`访问路由实例，即在路由定义文件中`export default`的`new Router(/*...*/)`路由实例，通过`$route`可以访问当前激活的路由的状态信息，包含了当前`URL`解析得到的信息，还有`URL`匹配到的路由记录，可以将`$router`理解为一个容器去管理了一组`$route`，而`$route`是进行了当前`URL`和组件的映射。

#### $router对象属性

- `$router.app`: 配置了`router`的`Vue`根实例。
- `$router.mode`: 路由使用的模式。
- `$router.currentRoute`: 当前路由对应的路由信息对象。

#### $router对象方法

- `$router.beforeEach(to, from, next)`: 全局前置守卫，守卫是异步解析执行，此时导航在所有守卫`resolve`完之前一直处于等待中状态，守卫方法接收三个参数: `to: Route`即将要进入的目标路由对象、`from: Route`: 当前导航正要离开的路由、`next: Function`: 调用该方法来`resolve`这个钩子，执行效果依赖`next`方法的调用参数，例如`next()`、`next(false)`、`next('/')`、`next({path:'/',name:'home',replace:true,query:{q:1}})`、`next(error)`等，通常在`main.js`中`import`的`Vue Router`实例中直接定义导航守卫，当然也可在`Vue`实例中访问`$router`来定义。
- `$router.beforeResolve(to, from, next)`: 全局解析守卫，在`beforeRouteEnter`调用之后调用，同样接收`to`、`from`、`next`三个参数。
- `$router.afterEach(to, from)`: 全局后置钩子，进入路由之后调用，接收`to`、`from`两个参数。
- `$router.push(location[, onComplete[, onAbort]])`: 编程式导航，使用`$router.push`方法导航到不同的`URL`，此方法会向`history`栈添加一个新的记录，当点击浏览器后退按钮时，则回到之前的`URL`。
- `$router.replace(location[, onComplete[, onAbort]])`: 编程式导航，跟`$router.push`很像，唯一的不同就是，其不会向`history`添加新记录，而是跟它的方法名一样替换掉当前的`history`记录。
- `$router.go(n)`: 编程式导航，这个方法的参数是一个整数，意思是在`history`记录中向前或者后退多少步，类似`window.history.go(n)`。
- `$router.back()$router.back`: 编程式导航，后退一步记录，等同于`$router.go(-1)`。
- `$history.forward()`: 编程式导航，前进一步记录，等同于`$router.go(1)`。
- `$router.getMatchedComponents([location])`: 返回目标位置或是当前路由匹配的组件数组 ，是数组的定义或构造类，不是实例，通常在服务端渲染的数据预加载时使用。
- `$router.resolve(location[, current[, append]])`: 解析目标位置，格式和`<router-link>`的`to prop`相同，`current`是当前默认的路由，`append`允许在`current`路由上附加路径，如同 `router-link`。
- `$router.addRoutes(route)`: 动态添加更多的路由规则，参数必须是一个符合`routes`选项要求的数组。
- `$router.onReady(callback[, errorCallback])`: 该方法把一个回调排队，在路由完成初始导航时调用，这意味着它可以解析所有的异步进入钩子和路由初始化相关联的异步组件，这可以有效确保服务端渲染时服务端和客户端输出的一致，第二个参数`errorCallback`会在初始化路由解析运行出错时被调用。
- `$router.onError(callback)`: 注册一个回调，该回调会在路由导航过程中出错时被调用，被调用的错误必须是下列情形中的一种，错误在一个路由守卫函数中被同步抛出、错误在一个路由守卫函数中通过调用`next(err)`的方式异步捕获并处理、渲染一个路由的过程中需要尝试解析一个异步组件时发生错误。

#### $route对象属性

- `$route.path`: 返回字符串，对应当前路由的路径，总是解析为绝对路径。
- `$route.params`: 返回一个`key-value`对象，包含了动态片段和全匹配片段，如果没有路由参数，就是一个空对象。
- `$route.query`: 返回一个`key-value`对象，表示`URL`查询参数。
- `$route.hash`: 返回当前路由的带`#`的`hash`值，如果没有`hash`值，则为空字符串。
- `$route.fullPath`: 返回完成解析后的`URL`，包含查询参数和`hash`的完整路径。
- `$route.matched`: 返回一个数组，包含当前路由的所有嵌套路径片段的路由记录，路由记录就是`routes`配置数组中的对象副本。
- `$route.name`: 如果存在当前路由名称则返回当前路由的名称。
- `$route.redirectedFrom`: 如果存在重定向，即为重定向来源的路由的名字。

### 17.6.15 导航守卫

#### 全局导航守卫

+ ![image-20200926101503031](https://gitee.com/zpfzpf123/vue/raw/master/image-20200926101503031.png)

+ 比如我们想在切换组件的时候，我们想要更改title名，我们可以这样做

  - 在main.js中创建函数`router.beforeEach()`(**前置钩子**)

  ```js
  router.beforeEach((to, from, next) => {
    document.title=to.matched[0].meta.title,//把当前页面的title给title
    next()//页面刷新
  })
  ```

  ```js
  routes: [
      {
        path: '/page',
        component: page,
        meta:{
          title:'首页'//添加title属性
        }
      },
      {
        path:'/Pages',
        component: Pages,
        meta:{
          title:'附页'
        }
      },
      {
        path:'/normal',
        component:normal,
        meta:{
          title:'消息'
        },
        children:[
          {
            path:'',
            redirect:'normalnew'
          },
          {
            path:'normalnew',
            component:normalnew
          },
          {
            path:'normalmy',
            component:normalmy
          }
        ]
      },
    ],
  ```

  - 执行效果

  ![image-20200926100948164](https://gitee.com/zpfzpf123/vue/raw/master/image-20200926100948164.png)

![](https://gitee.com/zpfzpf123/vue/raw/master/image-20200926100948164.png)

![image-20200926101008910](https://gitee.com/zpfzpf123/vue/raw/master/image-20200926101008910.png)

+ afterEach(to,from) [后置钩子 不需要next() 会在跳转完页面之后执行]

  - 如下

    ```js
    router.afterEach((to,from)=>{
      console.log('我是后置组件');
    })
    
    ```

    

  - 如图所示

    ![image-20200926103121535](https://gitee.com/zpfzpf123/vue/raw/master/image-20200926103121535.png)

#### 路由独享守卫和组件内守卫

+ 见官网 https://router.vuejs.org/zh/guide/advanced/navigation-guards.html#%E5%85%A8%E5%B1%80%E5%90%8E%E7%BD%AE%E9%92%A9%E5%AD%90

### 17.6.16 keep-alive

+ 需求:比如我们在点击一个路由的子组件的消息时，然后又换到了其它路由，然后我们再次回到原来的路由时，这时候原来的路由就会重置到我们设定的默认路径,但是我们想不让他重置，而是保持我们原有的点击状态，这个时候我们可以使用keep-alive解决这个问题
+ 首先在App.vue中插入如下代码

```vue
<keep-alive>
      <router-view></router-view>
</keep-alive>//保持活跃  避免清理缓存
```

+ 然后再normal.vue中插入以下代码

```vue
<template>
  <div>
    <p>我是normal</p>
    <p>{{message}}</p>
    <router-link to="/normal/normalnew">新闻</router-link>
    <router-link to="/normal/normalmy">我的</router-link>
    <p v-for="item in $route.query">{{item}}</p>
    <router-view></router-view>

  </div>
</template>

<script>
  export default {
    name:'normal',
    data() {
      return {
        message:'你好我是message',
        path:'/normal/normalnew'
      }
    },
    created(){
      console.log('created');//组件被创建时执行
    },
    destroyed() {
      console.log('destroyed');//组件被销毁执行 这里不会执行 因为keep-alive在生效
    },
    activated() {
      console.log('avtivated');//路由处于活跃状态时执行
      this.$router.push(this.path)//处于活跃状态把当前路径Push上去
    },
    beforeRouteLeave (to, from, next) {
      this.path=this.$route.path//离开路径以前把当前路由路径上传给this.path 保证下一次回来当前路径可以保留原有保存路径
      console.log(this.path);
      next()
  }
  }
</script>

<style>
  p{
    color: red;
  }
</style>

```

+ 通过上面的例子 我们不难发现  每个组件都会在点击后处于活跃状态，不会被销毁，如果我们希望一个组件能够被频繁的创建和销毁，我们可以这样做
+ keep-alive有两个重要属性
  - include -- 字符串或者正则表达式，只有匹配的组件会被缓存
  - exclude -- 字符串或者正则表达式，任何匹配的组件都不会被缓存

+ 例子如下

```vue
<keep-alive exclude="page">
      <router-view></router-view>
</keep-alive>
```

> 这里表示name:page的组件不会被缓存，也就是可以重复创建和销毁

#  018	项目tabbar的实现

## 	构建思路

![image-20200926142033563](https://gitee.com/zpfzpf123/vue/raw/master/image-20200926142033563.png)

## 组件化思想

我们把下面的导航栏可以看做一个大的组件，而里面有四个图标和文字，我们可以把这些图标和文字运用插槽的思想把他们添加进去，方便我们后期的修改和维护，代码如下

> App.vue

```vue
<template>
  <div id="app">
    <tabbar>
        <tabbaritem>
          <img slot='item-icon' src="./assets/img/tabbar/home.svg" alt="">
          <div slot='item-text'>首页</div>
        </tabbaritem>

        <tabbaritem>
          <img slot='item-icon' src="./assets/img/tabbar/category.svg" alt="">
          <div slot='item-text'>购物车</div>
        </tabbaritem>

        <tabbaritem>
          <img slot='item-icon' src="./assets/img/tabbar/shopcart.svg" alt="">
          <div slot='item-text'>分类</div>
        </tabbaritem>

        <tabbaritem>
          <img slot='item-icon' src="./assets/img/tabbar/profile.svg" alt="">
          <div slot='item-text'>我的</div>
        </tabbaritem>
    </tabbar>
  </div>
</template>

<script>
import tabbar from './components/tabbar/tabbar.vue'
import tabbaritem from './components/tabbar/tabbar-item.vue'
export default {
  name: 'App',
  components: {
    tabbar,
    tabbaritem
  }
}
</script>

<style>
@import './assets/css/base.css'
</style>

```

> tabbar.vue

```vue
<template>
  <div class="tabbar">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'tabbar',
  }
</script>

<style>
  .tabbar {
    display: flex;

    background-color: #f6f6f6;

    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;

    box-shadow: 0px -5px 1px rgba(100, 100, 100, .1);
  }
  .tabbar img {
    width: 24px;
    height: 24px;
    margin-top: 3px;
    vertical-align: middle;
  }
</style>

```

> tabbar-item.vue

```vue
<template>
  <div class="tab-bar-item">
    <slot name="item-icon"></slot>
    <slot name="item-text"></slot>
  </div>

</template>

<script>
  export default {
    name: 'tabbaritem'
  }
</script>

<style>


  .tab-bar-item {
    flex: 1;
    text-align: center;
    height: 49px;
    font-size: 14px;
  }


</style>

```



> 记住，我们在使用组件化思想的时候，衡多东西不要写死，而是要动态的决定它，这个是狗建议使用插槽，不如这里我们给`tabbar`添加一个插槽，给`tabbar-item`添加两个插槽,tabbar的插槽用来给tabbar-item插入东西,tabbar-item的插槽用来给图片和文字插入，这就是组件化思想

## 路由封装

> 我们需要在每个组件上面封装一个路由，代码如下

home.vue

```vue
<template>
  <div>
    home
  </div>
</template>

<script>
  export default{
    name:'home'
  }
</script>

<style>
</style>

```

> 其它category.vue profile.vue shopcart.vue 同理

index.js

```js
import Vue from 'vue'
import Router from 'vue-router'
const home=()=>import('../view/home/home.vue')
const category=()=>import('../view/category/category.vue')
const profile=()=>import('../view/profile/profile.vue')
const shopcart=()=>import('../view/shopcart/shopcart.vue')
Vue.use(Router)

export default new Router({
  routes: [
    {
      path:'',
      redirect:'/home'
    },
    {
      path:'/home',
      component:home,
    },
    {
      path:'/category',
      component:category,
    },
    {
      path:'/shopcart',
      component:shopcart,
    },
    {
      path:'/profile',
      component:profile,
    },
  ]
})

```

App.vue

```vue
<template>
  <div id="app">
    <tabbar>
      <tabbaritem path="/home">
        <img slot='item-icon' src="./assets/img/tabbar/home.svg" alt="">
        <img slot='item-icons' src="./assets/img/tabbar/home_active.svg" alt="">
        <div slot='item-text'>首页</div>
      </tabbaritem>

      <tabbaritem path="/category">
        <img slot='item-icon' src="./assets/img/tabbar/category.svg" alt="">
        <img slot='item-icons' src="./assets/img/tabbar/category_active.svg" alt="">
        <div slot='item-text'>购物车</div>
      </tabbaritem>

      <tabbaritem path="/shopcart">
        <img slot='item-icon' src="./assets/img/tabbar/shopcart.svg" alt="">
        <img slot='item-icons' src="./assets/img/tabbar/shopcart_active.svg" alt="">
        <div slot='item-text'>分类</div>
      </tabbaritem>

      <tabbaritem path="profile">
        <img slot='item-icon' src="./assets/img/tabbar/profile.svg" alt="">
        <img slot='item-icons' src="./assets/img/tabbar/profile_active.svg" alt="">
        <div slot='item-text'>我的</div>
      </tabbaritem>
    </tabbar>
    <router-view></router-view>
  </div>

</template>

<script>
  import tabbar from './components/tabbar/tabbar.vue'
  import tabbaritem from './components/tabbar/tabbar-item.vue'
  export default {
    name: 'App',
    components: {
      tabbar,
      tabbaritem
    }
  }
</script>

<style>
  @import './assets/css/base.css'
</style>

```

tabbar-item.vue

```vue
<template>
  <div class="tab-bar-item" @click="btnclick">
    <div v-if="activtive">
      <slot name="item-icon"></slot>
    </div>
    <div v-else>
      <slot name='item-icons'></slot>
    </div>
    <div @click="clickactive" :class="{active:!activtive}">
      <slot name="item-text"></slot>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'tabbaritem',
    props:{
      path:String
    },
    data() {
      return {
        activtive: true
      }
    },
    methods: {
      clickactive() {
        this.activtive = !this.activtive
      },
        btnclick() {
          this.$router.push(this.path)
      }
    }
  }
</script>

<style>
  .tab-bar-item {
    flex: 1;
    text-align: center;
    height: 49px;
    font-size: 14px;
  }

  .active {
    color: red;
  }
</style>

```

> 我们通过props给每个路由添加路径，然后添加点击事件动态切换路由

## 动态绑定style和决定组件颜色

>  代码如下

**tabbar-item.vue**

```vue
<template>
  <div class="tab-bar-item" @click="btnclick">
    <div v-if="!activtive"> //如果activtive为true,这里就为false，那么图标就会显示红色，也就是活跃路由组件图标显示为红色
      <slot name="item-icon"></slot>
    </div>
    <div v-else>
      <slot name='item-icons'></slot>
    </div>
    <div :style="activeStyle"> //动态绑定style属性
      <slot name="item-text"></slot>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'tabbaritem',
    props: {
      path: String,
      activeColor:{
        type:String,
        default:'red' //给activeColor定义为字符串，初值为red
      }
    },
    computed: {
      activtive() {
        return this.$route.path.indexOf(this.path) !== -1//如果点击的路由为当前活跃路由，那么返回true
      },
      activeStyle() {
        return this.activtive ? {
          color: this.activeColor //如果activtive为true，给style动态绑定color属性，也就是活跃路由组件的文字加上颜色，如果false就传空属性
        } : {}
      }
    },
    methods: {
      btnclick() {
        this.$router.push(this.path)
      }
    }
  }
</script>

<style>
  .tab-bar-item {
    flex: 1;
    text-align: center;
    height: 49px;
    font-size: 14px;
  }
</style>

```

**App.vue**

```vue
<template>
  <div id="app">
    <tabbar>
      <tabbaritem path="/home"> //这里不加activeColor表示默认为初值红色
        <img slot='item-icon' src="./assets/img/tabbar/home.svg" alt="">
        <img slot='item-icons' src="./assets/img/tabbar/home_active.svg" alt="">
        <div slot='item-text'>首页</div>
      </tabbaritem>

      <tabbaritem path="/category" activeColor='blue'>
        <img slot='item-icon' src="./assets/img/tabbar/category.svg" alt="">
        <img slot='item-icons' src="./assets/img/tabbar/category_active.svg" alt="">
        <div slot='item-text'>购物车</div>
      </tabbaritem>

      <tabbaritem path="/shopcart" activeColor='yellow'>
        <img slot='item-icon' src="./assets/img/tabbar/shopcart.svg" alt="">
        <img slot='item-icons' src="./assets/img/tabbar/shopcart_active.svg" alt="">
        <div slot='item-text'>分类</div>
      </tabbaritem>

      <tabbaritem path="/profile" activeColor='green'>
        <img slot='item-icon' src="./assets/img/tabbar/profile.svg" alt="">
        <img slot='item-icons' src="./assets/img/tabbar/profile_active.svg" alt="">
        <div slot='item-text'>我的</div>
      </tabbaritem>
    </tabbar>
    <router-view></router-view>
  </div>

</template>

<script>
  import tabbar from './components/tabbar/tabbar.vue'
  import tabbaritem from './components/tabbar/tabbar-item.vue'
  export default {
    name: 'App',
    components: {
      tabbar,
      tabbaritem
    }
  }
</script>

<style>
  @import './assets/css/base.css'
</style>

```

## 路径起别名配置

+ 在webpack.config.js里面添加别名

```js
resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      '@': resolve('src'),
      'assets':resolve('src/assets')
    }
  },
```

+ 在App.vue里运用,***注意加~号***

```vue
<img slot='item-icon' src="~assets/img/tabbar/home.svg" alt="">
<img slot='item-icons' src="~/assets/img/tabbar/home_active.svg" alt="">
```

# 019 promise

+ 什么是promise

![image-20200929110148401](https://gitee.com/zpfzpf123/vue/raw/master/image-20200929110148401.png)

![image-20200929110449517](https://gitee.com/zpfzpf123/vue/raw/master/image-20200929110449517.png)

## 打印例子

```js
new Promise((resolve, reject) => {
				setTimeout(() => {//第一次网络请求的代码
					resolve()
				}, 1000)
			}).then(() => {//第一次网络请求后处理的代码
				console.log("hello 1");
				console.log("hello 1");
				console.log("hello 1");

				return new Promise((resolve, reject) => {//第二次网络请求的代码
					setTimeout(() => {
						resolve()
					}, 1000)
				})
			}).then(() => {//第二次网络请求后处理的代码
				console.log("hello time2");
				console.log("hello time2");
				console.log("hello time2");

				return new Promise((resolve, reject) => {//第三次网络请求的代码
					setTimeout(() => {
						resolve()
					}, 1000)
				})
			}).then(() => {//第三次网络请求后处理的代码
				console.log("hello time3");
				console.log("hello time3");
				console.log("hello time3");
				console.log("hello time3");
			})
```

> 上述代码所示 首先promise是一个对象，我们先new promise一个对象，然后里面有一个函数，函数里有两个参数一个是resolve一个是reject,这两个参数也是函数，然后在外层函数里我们可以添加方法，然后执行resolve后就会跳转到then(),then里面也是一个函数，函数内部是我们要实现的代码功能，我们可以在没内部继续return一个new promise对象，后面写法与前面同理，这样的代码比我们直接写嵌套的代码来的条理清晰很多。。。

***运行结果如下所示***

![image-20201001144428076](https://gitee.com/zpfzpf123/vue/raw/master/image-20201001144428076.png)

## promise三种状态

![image-20201001145850944](https://gitee.com/zpfzpf123/vue/raw/master/image-20201001145850944.png)

**代码如下所示**

```js
new Promise((resolve,reject)=>{
				resolve('hello resolve')
				reject('hello err')
			}).then(data=>{
				console.log(data);
			},
			err=>{
				console.log(err);
			})
```

> 当我们调用了resolve函数我们就会执行then(函数1,函数2)中的函数1，如果注释掉resolve，调用reject函数，我们就会执行函数2

## promose的链式调用

**代码如下**

```js
new Promise((resolve)=>{
				setTimeout(()=>{
					resolve('aaa')
				},1000)
			}).then((data)=>{
				console.log(data,'第一行');
				return new Promise((resolve)=>{
					resolve(data+'111')
				})
			}).then(data=>{
				console.log(data,'第二行')
				return Promise.resolve(data+'222')
			}).then((data)=>{
				console.log(data,'第三行');
				return data+'333'
			}).then((data)=>{
				console.log(data,'第四行');
				/* return Promise.reject('err') */
				throw 'err message'
			}).catch((err)=>{
				console.log(err);
			})
```

> 我们可以把
>
> return new Promise((resolve)=>{
> 					resolve(data+'111')
> 				}
>
> 简写成
>
> return Promise.resolve(data+'111')
>
> 还可以简写成
>
> return data+'111'

> 我们可以把return new Promise((reject)=>{
> 					reject(data+'111')
> 				}
>
> 简写成return Promise.reject('err')
>
> 或者throw 'err'

## promise.all的使用

**如果我们想实现这个需求，比如说我们想让某个需求在两个网络请求完成后再运行，我们可以这样做**

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
	  <script>
		  Promise.all([
			new Promise((resolve,reject)=>{
				setTimeout(()=>{
					resolve('hello zpf')
				},2000)
			}),
			new Promise((resolve,reject)=>{
				setTimeout(()=>{
					resolve('hello zpfs')
				},1000)
			})
			
		 ]).then((data)=>{
			  console.log(data);
		  })
	  </script>
	</body>
</html>

```

> **Promise.all函数可以帮我们实现上面的需求，我们在all里面创建了两个Promise，当两个promise的resolve()执行完成后，我们就会执行后面的then()函数，而then()函数就是我们要实现的某个需求。**

# 020 vuex的使用

## 20.1 vuex作用

![image-20201003151101932](https://gitee.com/zpfzpf123/vue/raw/master/image-20201003151101932.png)

![image-20201002103857725](https://gitee.com/zpfzpf123/vue/raw/master/image-20201002103857725.png)

## 20.2 vuex的运用

**代码如下**

store/index.js

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    counter:0//共享数据 无论在哪个组件都能用 可以看做全局变量
  },
  mutations: {
    increment(state){
      state.counter++ //方法，可以对共享数据进行操作
    },
    decrement(state){
      state.counter--
    }
  },
  actions: {
  },
  modules: {
  }
})

```

App.vue

```js
<template>
  <div id="app">
    <h1>App.vue------</h1>
    <h1>{{$store.state.counter}}</h1>
    <button @click="add()">+</button>
    <button @click="sub()">-</button>
    <learnvuex></learnvuex>
  </div>
</template>
<script>
import learnvuex from "./components/learnvuex";
  export default {
    name:'App',
    components:{
      learnvuex
    },
    methods:{
      add(){
        this.$store.commit('increment')//提交store里的increment方法
      },
      sub(){
        this.$store.commit('decrement')
      }
    }
  }
</script>
<style>

</style>

```

> 我们修改共享数据最好在mutations对象里添加方法进行修改，这样方便我们以后检查代码，确定代码的改变位置等等，可以更加明确的追踪状态的变化
>
> 如下
>
> ![image-20201002173451652](https://gitee.com/zpfzpf123/vue/raw/master/image-20201002173451652.png)

## 20.3 vuex store单一状态树

![image-20201002174453055](https://gitee.com/zpfzpf123/vue/raw/master/image-20201002174453055.png)

## 20.4 vuex getters使用(类似vue里的computed)

### 基本使用

**代码如下**

**vuex/index.js**

```js
getters:{
    more20stu(state){
      return state.student.filter(s=>s.age>=24)
    }
  },
```

**App.vue**

```vue
<p>{{$store.getters.more20stu}}</p>
```

**显示效果**

![image-20201002180021930](https://gitee.com/zpfzpf123/vue/raw/master/image-20201002180021930.png)

> 上述代码我们如果还想获取满足条件的数组的个数，我们还可以在getters里面调用getters的操作，比如这样

```js
 getters:{
    more20stu(state){
      return state.student.filter(s=>s.age>24)
    },
    more20stulength(state,getters){
      return getters.more20stu.length
    }
  },
```

>  我们也可以直击去设定age年龄 

```js
moreagestu(state){
      return function (age) {
        return state.student.filter(s=>s.age>age)
      }
    }
```

## 20.5 vuex mutations(类似vue的methods)(不要再里面定义异步操作函数方法)

我们可以给mutation传递参数，**如下**

**vuex/index.js**

```js
incrementfive(state,count){
      state.counter+=count
    },
addstudent(state,stu){
      state.student.push(stu)
    }
```

**App.vue**

```js
addint(count){
  this.$store.commit('incrementfive',count)
},
addstu(stu){
  /*const stu={id:4,name:'zpf',age:28}*/
  this.$store.commit('addstudent',stu)
```

```js
<button @click="addint(5)">+5</button>
<button @click="addstu({id:4,name:'zpf',age:25})">添加学生</button>
```

### **mutations**的两种提交风格

第一种

```js
this.$store.commit('incrementfive',count)
```

第二种

```js
this.$store.commit({
  type:"incrementfive",
  count
})
```

两种count对应的值是不一样的

第一种是参数，第二种是返回对象，我们分别打印

![image-20201002231526042](https://gitee.com/zpfzpf123/vue/raw/master/image-20201002231526042.png)

### vuex的响应式规则

![image-20201003142148186](https://gitee.com/zpfzpf123/vue/raw/master/image-20201003142148186.png)

### vue mutatin方法写法

> 我们知道在mutation里面是定义横很多方法的，然后我们要在其它组件运用这些方法的时候，再添加一个方法，这中间方法太多，我们很容易把变量写错，我们可以这样做，新建一个vuex-mutation.js如下

```js
export const INCREMENT='increment'
```

我们分别在store/index.js和要使用的组件里导入

```vue
import {INCREMENT} from "./store/store-mutations";
```

我们在index.js这样使用

```js
[INCREMENT](state){
  state.counter++
},
```

在组件方法里这样使用

```vue
add(){
  this.$store.commit(INCREMENT)
},
```

这样我们就可以避免错误

## 20.6 vuex Actions (异步操作的方法)

> 我们如果在mutation里面执行异步操作的一些方法，从表面上看确实能够执行成功，但是其实是有问题的，它会导致我们的真是数据与我们state上的数据不同，也就是说页面上的数据会改变，但是存储在state中的数据没有改变，这个时候我们就需要用到actions方法，方法如下

store/index.js

**mutation里**

```js
setadress(state){
  Vue.set(state.teacher,'adress','chinese')
}
```

**actions里**

```js
actions: {
  asetaddress(context){
    setTimeout(()=>{
      context.commit('setadress')
    })
  }
```

**组件里**

```vue
setadress(){
        this.$store.dispatch('asetaddress')
      }
```

> 我们先在mutation里把方法定义好，然后放到actions里，这里的context相当于store，也就是这里把setadress方法提交到了actions，最后在组件里使用dispatch方法把actions里的异步操作提交,这样才能成功让state和

20.7 module的使用

module**的作用**

![image-20201005173332052](https://gitee.com/zpfzpf123/vue/raw/master/image-20201005173332052.png)

## 20.7 vuex module

见官网

20.8 vuex 目录结构

**如下图**

![image-20201005213452889](https://gitee.com/zpfzpf123/vue/raw/master/image-20201005213452889.png)

