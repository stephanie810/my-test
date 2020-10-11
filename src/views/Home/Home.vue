<template>
 <div id="home" class="wrapper">
   <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
   <home-swiper :banners="banners"></home-swiper>
   <recommend-view :recommends="recommends"></recommend-view>
   <feature-view></feature-view>
   <tab-control class="tab-control"
                :titles="['流行','新款','精选']"
                @tabClick="tabClick">
   </tab-control>
   <goods-list :goods="showGoods"></goods-list>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>11</h3>
     <h3>22</h3>
 </div>
</template>

<script>
  import NavBar from '@/components/common/navbar/NavBar';
  import GoodsList from "@/components/content/goods/GoodsList";
  import TabControl from "@/components/content/tabControl/TabControl";

  import { getHomeMultidata, getHomeGoods } from "@/network/home";

  import RecommendView from "./childComps/RecommendView";
  import HomeSwiper from './childComps/HomeSwiper';
  import FeatureView from "./childComps/FeatureView";

  export default {
    name: "Home",
    components:{
      NavBar,
      HomeSwiper,
      RecommendView,
      FeatureView,
      GoodsList,
      TabControl
    },
    data(){
      return {
        banners:[],
        recommends:[],
        goods:{
          'pop':{page:0,list:[]},
          'new':{page:0,list:[]},
          'sell':{page:0,list:[]}
        },
        currentType:'pop'
      }
    },
    computed:{
      showGoods(){
        return this.goods[this.currentType].list
      }
    },
    created(){
      //1.请求多个数据
       this.getHomeMultidata()

      //2.请求商品数据
      this.getHomeGoods('pop')
      this.getHomeGoods('new')
      this.getHomeGoods('sell')

    },

    methods:{
      getHomeMultidata() {
        //1.请求多个数据(首页只需要面向函数)
        getHomeMultidata().then(res => {
          console.log(res);
          this.banners = res.data.data.banner.list;
          this.recommends = res.data.data.recommend.list;
        })
      },
      getHomeGoods(type){
        const page = this.goods[type].page + 1
        getHomeGoods(type,page).then(res=>{
          this.goods[type].list.push(...res.data.data.list)
          this.goods[type].page += 1
        })
      },
      tabClick(index){
        switch(index){
          case 0:
            this.currentType = 'pop'
            break
          case 1:
            this.currentType = 'new'
            break
          case 2:
            this.currentType = 'sell'
            break
        }
      }
    }
  }
</script>

<style scoped>
  /*#home{*/
  /*  height: 100vh;*/


  /*  position: relative;*/
  /*}*/
 .home-nav{
   background-color:var(--color-tint);
   color:#ffffff;

   position:fixed;
   left:0;
   right: 0;
   top:0;
   z-index:9;
 }

  .tab-control{
    position: sticky;
    top:44px;
    z-index:9;
  }
</style>
