<template>
  <div>
    <!-- bootstrap 排版 -->
    <div class="container-fluid">
      <div class="row">
        <div class="col-md-3 text-center" id="share">
          <a href="#">
            <search/>
          </a>
        </div>
        <div class="col-md-9" id="sale">
          <sale/>
        </div>
      </div>
      <div class="row">
        <userfilter id="user"/>
        <div class="col-md-9 col-12" id="navbar">
          <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal">
            <el-menu-item index="1">排序</el-menu-item>
            <el-submenu index="2">
              <template slot="title">精選評分</template>
              <el-menu-item v-for="item of rateList" :key="item.index" :index="item.index" @click="changeRate(item.rate)">{{item.name}}</el-menu-item>
            </el-submenu>
            <el-submenu index="3">
              <template slot="title">價格</template>
              <el-menu-item v-for="item of priceList" :key="item.index" :index="item.index" @click="changePrice(item.result)">{{item.name}}</el-menu-item>
            </el-submenu>
            <el-submenu index="4">
              <template slot="title">天數</template>
              <el-menu-item index="4-1">1</el-menu-item>
              <el-menu-item index="4-2">2</el-menu-item>
              <el-menu-item index="4-3">3</el-menu-item>
              <el-menu-item index="4-4">4</el-menu-item>
              <el-menu-item index="4-5">不回家了</el-menu-item>
            </el-submenu>
            <el-menu-item index="5">出發日期</el-menu-item>
          </el-menu>
          <shop-lists :results="resultEnd" />
          <div class="page">
            <nav aria-label="Page navigation example">
              <ul class="pagination">
                <li class="page-item" @click="decreasePage()">
                  <a class="page-link" aria-label="Previous" href="#">
                    <span aria-hidden="true">&laquo;</span>
                  </a>
                </li>
                <li class="page-item" v-for="item of pages" :key="item" @click="getPageData(item)"><a class="page-link" href="#">{{ item }}</a></li>
                <li class="page-item" @click="increasePage()" v-if="other">
                  <a class="page-link" href="#" aria-label="Next">
                    <span aria-hidden="true">&raquo;</span>
                  </a>
                </li>
              </ul>
            </nav>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import userfilter from "./userfilter";
  import sale from "./sale";
  import search from "./search";
  import shopLists from "./shopLists";
  import axios from 'axios';
  import * as $ from 'jquery';

    export default {
        name: "navbar",
        components: {
          userfilter,
          sale,
          shopLists,
          search
        },
        data(){
          return{
            activeIndex: '1',
            priceList: [{index:'3-1',name: '高到低' , result: 'price_desc'},{index:'3-2',name: '低到高', result: 'price_asc'}],
            rateList: [{index:'2-1',name: '高到低' , rate: 'rating_desc'},{index:'2-2',name: '低到高', rate: 'rating_asc'}],
            page: 1,
            row_per_page: 10,
            sort: 'rating_desc',
            pages: [1],
            resultEnd: [],    //測試資料  this.$store.getters.listsData.data.tour_list && 將 getData() 裏面 coding 注解掉
            other: true
          }
        },

        created() {
          this.getData();
        },

        methods: {

          changeRate(item) {
            if (item === 'rating_asc') {
              this.sort = item;
              this.getData()
            } else {
              this.sort = item;
              this.getData()
            }
          },

          changePrice(item) {
            if (item === 'price_desc') {
              this.sort = item;
              this.getData()
            } else {
              this.sort = item;
              this.getData()
            }
          },

          // ajax 獲取資料
          getData() {

            let todo = [];
            axios.get('http://interview.tripresso.com/tour/search',{
              params:{
                page: this.page,
                row_per_page: this.row_per_page,
                sort: this.sort
              }
            }).then(res => {
              let items = res.data.data.tour_list;
              for (let item of items) {
                todo.push(item);
              }
              this.resultEnd = todo
            })
          },

          // 根據點選分頁數篩選資料
          getPageData(item) {
            this.page = item;
            this.getData();
          },

          increasePage() {

              this.page++;
              let dis = this.pages.find(todo => todo === this.page);
              this.getData();
              if (!dis && this.resultEnd.length > 0 ) {
                this.pages.push(this.page);
              } else if (!dis && this.resultEnd.length === 0 ){
                this.page--;
                this.getData();
                this.other = false;
              }

            },
            decreasePage() {
              if (this.page > 0 && this.page !== 0 && this.page !== 1 ) {
                this.page--;
                this.getData();
              }
          }
      }
    }
</script>

<style scoped>
  @media screen and (min-width: 1280px){

      a:hover{
        text-decoration: none;
      }

      #navbar{
        position: relative;
        margin-top: 70px;
      }

      #user{
        position: relative;
        top:  70px;
      }

      #sale {
        position: relative;
        top: 70px;
      }

      #share {
        position: relative;
        top: 70px;
      }

      .page {
        position: relative;
        left: 40%;
        margin: 45px 0 20px 0;
      }


  }
  @media screen and (min-width: 768px) and (max-width: 1279px){

  }
  @media screen and (max-width: 767px){

    #share{
      margin-top: 30px;
    }

    #sale{
      margin: 15px 0;
    }

    #navbar {
      margin-top: 15px;
    }

    .page {
      position: relative;
      left: 30%;
      margin: 30px 0 0 0;
    }


  }
</style>
