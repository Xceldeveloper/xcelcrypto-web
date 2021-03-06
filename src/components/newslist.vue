<template>
    <div id="news-wrapper" v-if="news.length > 0">
     
    <span id="newsheader">News</span>
      <ul id="news-container">
        <li v-for="(newx,index) in news" :key="index">
        <a :href="newx.url">
              <img :src="newx.imageurl" alt="">
          <span class="news-title">{{newx.title}}</span>
        
         <span class="news-time"> {{ timeConverter(newx.published_on) }}</span>
         
        </a>
        </li>
       
      </ul>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name:'newslist',
  data(){
      return{
          news:[]
      }
  },
  mounted(){
    setTimeout(()=>{
      this.getNews();
    },1000)
  },
  methods:{
    getNews(){
      this.news = axios.get('https://min-api.cryptocompare.com/data/v2/news/?lang=EN&api_key=af83ea3217205e8c8fab1e5a0e40027ab34fa4735635f9d9bfa10cf08c2f2db4').then(res=>{
        this.news = res.data.Data
      })
    },
     timeConverter(UNIX_timestamp){
  var a = new Date(UNIX_timestamp * 1000);
  var months = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
  var year = a.getFullYear();
  var month = months[a.getMonth()];
  var date = a.getDate();
  var hour = a.getHours();
  var min = a.getMinutes();
  var sec = a.getSeconds();
  var time = date + ' ' + month + ' ' + year ;
  return time;
}
  }
}
</script>

<style scoped>
#news-wrapper{
  display: block;
  margin: 20px auto;
  width: 100%;
  max-width: 900px;
  border-radius: 5px;
 
   box-shadow: 0px 1px 2px lightgrey;
}

#news-container{
  padding: 0px;
  margin: 0px;
  width: 100%;
  overflow: auto;
   white-space: nowrap;
  text-align: left;
}

#newsheader{
    display:block;
    text-align: left;
    padding: 3px;
    font-weight: bold;
}

#news-container li{
  width: 180px;
  display: inline-block;
  background-color: #fff;
  margin: 4px 10px;
  overflow: auto;
  border-radius: 10px;
  cursor: pointer;

}

#news-container li img{
  height: 180px;
  width: 180px;
  object-fit: cover;
  border-radius: 10px 10px 0px 0px;
}

.news-title{
  font-size: 14px;
  font-weight: bold;
  height: 43px;
  overflow: hidden;
  word-wrap: break-word; 
  white-space: pre-line;
  width:100%;
  display: block;
  padding: 4px;
}

.news-time{
  font-size: 15px;
  padding: 4px;
  display: block;
}
</style>