<template>
  <section class="sc-portfolio"> 
    <h1>Porfolio</h1>
    <carousel 
      class="slide-portfolio" 
      :perPage="4" :perPageCustom="[[320, 1], [360, 1], [375, 1], [420, 1], [768, 2], [1024, 3], [1300, 4]]"
      :paginationActiveColor="'#86baa3'"
      :paginationColor="'#d0e0d9'"
      :navigationEnabled="false"
      >
      <slide 
        v-for="(value, key) in items.coding" 
        v-bind:key="'coding-'+key">
        <div class="item coding">
          <div class="box-img" :style="{'background-image': 'url(' + require('@/assets/img/portfolio/'+ value.img +'.jpg') + ')'}">
            <p>coding</p>
          </div>
          <div class="box-detail">              
            <h2>
              <a :href="value.link" target="_blank">
                {{value.name}}
              </a>
            </h2>
            <h3>{{ value.type }}</h3>
            <span>{{ value.company}}</span>
            <p>{{ value.detail }}</p>
          </div>
        </div> 
      </slide>
      <!-- <slide
        v-for="(value, key) in items.design"
        v-bind:key="'design-'+key">
        <div class="item design">
          <div class="box-img" :style="{'background-image': 'url(' + require('@/assets/img/portfolio/'+ value.img +'.jpg') + ')'}">
            <p>design</p>
          </div>
          <div class="box-detail">
            <h2>{{value.name}}</h2>
            <h3>{{ value.type }}</h3>
            <span>{{ value.company}}</span>
            <p>{{ value.detail }}</p>
          </div>
        </div> 
      </slide> -->
    </carousel>
  </section>
</template>
<script>
  import { Carousel, Slide } from 'vue-carousel'
  const API = "static/json/portfolio.json"
  export default {    
    components: {
      Carousel,
      Slide
    },
    data() {
      return {
        items: []
      }
    },
    methods:{      
      fetchData: function () {
        var self = this
        $.ajax({
          method: 'GET',
          url: API,
          crossDomain: true,
          success: function (data) {
            self.items = data            
            console.log("success")
          },
          complete: function(res){
            console.log("complete")
          },
          error: function (xhr, status) {
          }
        }) 
      }
    }, 
    created() {
      this.fetchData()
    },
    mounted() {
    },
  }
</script>
<style lang="stylus">
  $green = #86baa3;
  $darkGreen = #7c9479;
  $lightGreen = #d0e0d9;
  $yellow = #ffcc33;
  .sc-portfolio{
    text-align: center;
    .slide-portfolio{
      width: 100%;
      padding: 0 0 60px;
      .item{
        position: relative;
        color: #666;
        width: 100%;
        display: block;
        &.design .box-img p{
          background-color: $yellow;
        }
      }
      .box-img{
        background: no-repeat;
        background-size: cover;
        width: 100%;
        padding-bottom: 63%;
        position: relative;
        p{
          position: absolute;
          top: 10px;
          left: 10px;
          z-index: 1;
          font-size: 14px;
          font-weight: bold;
          // background: $green;
          background: $yellow;
          color: #fff;
          padding: 5px 15px;
          border-radius: 5px;
          text-transform: uppercase;
        }
      }
      .box-detail{
        padding: 10px 20px 0;
        h2{
          color: #333;
          font-weight: bold;
          font-size: 1.5em;
          margin: 20px 0;
          border-bottom: 1px solid $lightGreen;
          padding-bottom 20px;
          a{
            color: #333;
            &:hover{
              color: $green;
            }
          }
        }
        h3{
          font-size: 1.3em;
          color: #333;
          margin-bottom: 15px;
        }
        p{
          font-size: 15px;
        }
        span{
          display : block;
          color: $green;
          padding-bottom: 5px;
        }
      }
    }
    .VueCarousel-dot:focus{
      outline: none;
    }
  }
  @media screen and (max-width: 580px) {
    .VueCarousel-pagination{
      display: none;
    }
    .sc-portfolio .slide-portfolio {
      padding: 0 0 30px;
    }
  }
</style>