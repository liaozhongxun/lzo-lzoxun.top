<template>
    <div class="PointDoc">
        <div class="container">
            <div class="menu" style="position:fixed;right:30px;top:300px;"></div>
            <div id="content">
                <h2 class='section'>摘要</h2>
                <div style="height:800px;">说明</div>
                <h3 class='section'>第1天</h3>
                <div style="height:800px;">第1天内容</div>
                <h3 class='section'>第2天</h3>
                <div style="height:800px;">第2天内容</div>
                <h3 class='section'>第3天</h3>
                <div style="height:800px;">第3天内容</div>
                <h3 class='section'>第4天</h3>
                <div style="height:800px;">第4天内容</div>
                <h3 class='section'>第5天</h3>
                <div style="height:800px;">第5天内容</div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name:'PointDoc',
    data(){
        return {
            scroll: '',
        }
    },
    methods: {
        dataScroll: function () {
            this.scroll = document.documentElement.scrollTop || document.body.scrollTop;
            console.log(this.scroll)
        },
        loadSroll: function () {
            var self = this;
            var $navs = $(".nav1");
            console.log($navs);
            var sections = document.getElementsByClassName('section');
            console.log(sections);
            for (var i = sections.length - 1; i >= 0; i--) {
                if (self.scroll >= sections[i].offsetTop - 95) {
                    $navs.eq(i).addClass("current").siblings().removeClass("current")
                    break;
                }
            }
        }
    },
    watch: {
        scroll: function () {
            this.loadSroll()
        }
    },
    mounted() {
        window.addEventListener('scroll', this.dataScroll);
        $("#content").children().each(function(index, element) { //变量容器内所有直接子元素
            var tagName=$(this).get(0).tagName; //获取标签名称
            console.log(tagName)
            if(tagName.substr(0,1).toUpperCase()=="H"){ //如果标签名称第一个字符是h或H 
                var contentH=$(this).html();//获取h标签里的内容
                var markid="mark-"+tagName+"-"+index.toString(); //创建一个标志作为锚点名称
                $(this).attr("id",markid);//为当前h标签id设置成这个标签
                var classList = 'nav1';
                
                if(tagName.substr(0,2).toUpperCase()=="H2"){
                    classList = 'nav1 h2nav';
                }else if(tagName.substr(0,2).toUpperCase()=="H3"){
                    classList = 'nav1 h3nav';
                }
                $(".menu").append("<a class='"+classList+"' href='#"+markid+"'>"+contentH+"</a>");//在目标DIV中添加内容,创建锚点菜单  
            }  
        });
    }
}
</script>
<style lang="scss">
.section{
    width: 100%;
}
.nav1 {
    display: block;
    width: 100px;
    height: 40px;
    text-align: center;
    line-height: 40px;
    background: #eee;
    margin: 10px 0;
}
.h2nav{
    color:#f00;
}
.current {
    color: #fff;
    background: red;
}
</style>