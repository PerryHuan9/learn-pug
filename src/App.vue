<template lang="pug">
 
    
    div
        p 我是文本
        | 这是文本
        p.
            这是文本
        #id #id不指定标签时，默认是div
        .id .id不指定默认是div
        p#p1 建立id为p1的p元素
        p.p1 建立class为p1的p元素
        h2.h2#h2 建立id为h2，class也为p2的h2元素
        
        //其它属性
        a(href="http://www.baidu.com" target='_blank') baidu
        -let show=true
        p(class=show ? 'trueShow' : 'falseShow') 引入js
        input(
        type='checkbox'
        name="input"
        checked
        )
        div(my-field="abc" style="color:white;background:blue")&attributes({align: 'center'}) 自定义属性和公有属性
        -let attr={class:'baz',style:{color:'red'}}
        div(data="mydata")&attributes(attr) 引入js属性对象
        
        
        //注释
        //-在编译后的html文件中也不会显示的注释
        <!--直接可以写html中的注释-->
        //
            块注释
        
        //case语句
        -let num=888;
        case num
            when 111
                p 这是111
            when 222
                - break
            when 888
                p 我是#{num}
        
        //循环
        ul
            -var n=0
            while n < 4
                li= n++
        //   ul
                - for(var x=0;x<3;x++)
                <!--li item#{x}-->
        ol
            -var list=[1,2,3,4,5,6]
            each item in list
                li=item
        
        //条件语句
        -var user={foo:'this is foo'}
        -var bar='baz'
        #user
            if user.foo
                h2.green foo
                p.foo=user.foo
            else if bar
                h2.blue bar
                p.foo.
                    User has no foo
            else
                h2.red foo
                p.foo user has no foo
        unless user.isFoo
            p 等同于： if !user.Foo
        
        
        //mixin创建重用的代码
        mixin list
            ul
                li foo
                li bar
                li baz
        //使用重用的代码块
        +list
        +list
        
        
        //mixin支持传参
        mixin article(title)
            .article
                .article-wrapper
                    h3=title
                    if block
                        block
                    else
                        p No content provided
        +article('Hello word')
        +article('hello pug')
            //以下是模块的内容
            p this is my
            p Amazing article
        //另外
        +article('my friend')(class='art')
            | 自定义的代码块相当于一个模块也可以为起增加class
        
        mixin myhref(href,name)
            a(class!=attributes.class  href=href target='_blank' )= name
        +myhref('http://www.yilin.pro','Yilin Resume')(class='btn')
     
        
        //传多个参数
        mixin abc(id,...items)
            ul(id=id)
                each item in items
                    li=item
        +abc('abc','龙腾虎啸','潜龙在渊','韬光养晦')
        
        
      
        
        
        //include引入pug文件
        include extends.pug
        
        
        

</template>

<script>

    export default {
        name: 'app',


    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
