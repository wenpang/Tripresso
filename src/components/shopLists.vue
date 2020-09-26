<template>
  <div>
    <div class="media" id="shop" v-for="item in results" v-bind:key="item.id">
      <a v-bind:href="item.tour_detail_url">
        <div class="media-body">
          <img :src="item.image_url" class="mr-0 photo" alt="載入錯誤">
          <div class="contents">
            <div class="company">
              {{item.agency}}
              <el-rate
                style="display: inline-block"
                v-model="item.rating"
                disabled
              >
              </el-rate>
            </div>
            <div class="title">
              <b>{{item.title}}</b>
            </div>
            <span class="locale">
                &nbsp;
                <i class="fas fa-map-marker-alt"></i>
                未提供
              </span>
            <div class="phonePirce">
              <b style="color: orange">{{item.tour_days}}</b>
              天<b style="color: orange">{{item.min_price}}</b>元起
              <p style="color: gray;font-size: 10px">下單現賺珈幣<i style="color: orange">$ 666</i></p>
            </div>
            <div class="tages">
              <el-row>
                <el-button type="primary" round size="mini" v-for="tag of item.tags" class="tag">{{tag}}</el-button>
              </el-row>
            </div>
            <hr style="margin-left: 25px;"/>
            <span class="scheduled" v-for="popo of item.group">
                &nbsp;
                {{popo.date}}
                <el-button type="primary" plain size="mini" style="display: block;margin-bottom: 5px">可售{{popo.quantity}}位</el-button>
              </span>
            <span>
                <a href="#" style="color: cornflowerblue;font-size: 14px;text-align: center">
                  <b>更多日期</b>
                </a>
              </span>
            <div class="price">
              <b style="color: orange">{{item.tour_days}}</b>
              天<b style="color: orange">{{item.min_price}}</b>元起
              <p style="color: gray;font-size: 10px">下單現賺珈幣<i style="color: orange">$ 666</i></p>
            </div>
          </div>
        </div>
      </a>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

    export default {
        name: "shopLists",
        props: ['results'],
        data() {
          return {
            page: null
          }
      }
    }
</script>

<style scoped>




  @media screen and (min-width: 1280px){

    .contents {
      float: right;
    }

    .phonePirce {
      display: none;
    }

    .photo {
      height:240px;
      width:200px;
    }

    #shop {
      margin-top: 30px;
      background-color: white;
      color: black;
    }

    #shop:hover {
      box-shadow: 1px 6px lightgray , 1px 10px silver;
    }

    a:hover{
      text-decoration: none;
    }

    .company{
      margin: 10px;
      color: gray;
      font-weight: bold;
    }

    .title{
      font-size: 16px;
      margin: 15px 20px;
      color: black;

    }

    .title:hover {
      color: black;
    }

    .locale {
      background: lightgrey;
      width: 100px;
      padding: 2px;
      border-radius: 3px;
      margin: 20px 25px;
      color: gray;
      font-family: Ebrima,cursive;
    }

    .tages {
      margin: 20px;
    }

    .scheduled{
      color: cornflowerblue;
      font-size: 13px;
      display: inline-block;
      margin:0 0 6px 25px;
    }

    .price {
      font-weight: bold;
      display: inline-block;
      color: black;
      position: absolute;
      left: 86%;
    }

    .price:hover{
      color:black;
    }

    .love {
      display: inline-block;
    }

  }
  @media screen and (min-width: 768px) and (max-width: 1279px){

  }
  @media screen and (max-width: 767px){

    .photo{
      width: 100%;
    }

    #shop {
      width: 100%;
      margin-top: 30px;
      background-color: white;
      color: black;
    }

    #shop:hover {
      box-shadow: 1px 6px lightgray , 1px 10px silver;
    }

    a:hover{
      text-decoration: none;
    }

    .company{
      margin: 17px 10px;
      color: gray;
      font-weight: bold;

    }

    .title{
      font-size: 14px;
      margin-left: 3px;
      text-indent: 10px;
      color: black;
      text-align: left;
    }

    .title:hover {
      color: black;
    }

    .locale {
      background: lightgrey;
      width: 80px;
      border-radius: 3px;
      margin: 10px;
      color: gray;
      font-family: Ebrima,cursive;
    }

    .tages {
      margin: 10px 10px 10px 10px;
    }

    .scheduled{
      color: cornflowerblue;
      font-size: 13px;
      display: inline-block;
      margin:0 0 6px 8px;
    }

    .price {
      display: none;
    }

    .price:hover{
      color:black;
    }


    .tag {
      margin: 5px;
    }

    .phonePirce {
      font-weight: bold;
      color: black;
      display: inline-block;
      margin-top: 10px;
      margin-left: 50px;
    }

  }



</style>
