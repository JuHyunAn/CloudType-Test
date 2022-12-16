<template>

  <!-- nav -->
  <div class="menu">
    <!-- <a>의 사용이 반복되기 때문에, 반복문으로 변경
    <a>Home</a>
    <a>Products</a>
    <a>About</a> -->

    <!-- vue 반복문 -->
    <!-- v-for="(명칭) in (횟수/data명)" :key="(명칭)" -->
    <a v-for="menu in taps" :key="menu">{{menu}}</a>
  </div>

  <img alt="Vue logo" src="./assets/logo.png">

  <h1>Vue공인중개사무소</h1>

  <!------------ vue data binding ------------>

  <!-- Json data를 가져오도록 코드 변경 2022.04.27 -->
  <!-- i를 key 값으로 사용하여, 정수 출력 -->
  <div v-for="(p_info, i) in productsDataSet" :key="(p_info, i)">
    <img class="room-img" :src="p_info.image" alt="해당 이미지를 불러올 수 없습니다.">
    <!-- Array에서 특정 column만 추출: (배열명칭).(컬럼명) -->
    <!-- 단순 data를 순서대로 뿌려주는 거라면, p_info 사용가능 -->
    <h4 class="room-nm" v-on:click="modalOpen = true;
      modalTitle = p_info.title; modalContent = p_info.content">🏡 {{p_info.title}}
    </h4>
    <p>💸 보증금: {{p_info.deposit}}만원 | 월세: {{p_info.rent}}만원</p>

    <!-- vue event handler -->
    <div id="report">
      <!-- 'v-on:' → '@' 대체 가능 (ex. @click="") -->
      <button id="increase" v-on:click="reports[i]++">신고하기🔺</button>
      &nbsp;
      <button id="decrease" v-on:click="reports[i]--">신고취소🔻</button>
      &nbsp;
      <span>신고수: {{reports[i]}}</span>
    </div>

    <!-- modal window -->
    <!-- vue 조건식 -->
    <!-- v-if="(조건식)" : 해당 조건식이 true일 경우에만 작동 -->
    <div id="modal" v-if="modalOpen == true">
      <div class="modal-window">
        <div class="title">
          <h2 class="modal-title">{{modalTitle}}</h2>
        </div>
        <div class="close-area" v-on:click="modalOpen = false">❌</div>
        <div class="content">
          <p>{{modalContent}}</p>
        </div>
      </div>
    </div>
  </div>


<!-- 2022.04.28 vue 무료 강의 완강~ -->
</template>


<script>
import productsData from "@/productsData";

export default {
  // Vue의 실시간 렌더링 사용을 위해, data binding('{{ }}')을 사용
  name: 'App',
  data() {  // data list
    return {
      // Json data
      productsDataSet : productsData, // import data
      // dummy data
      deposit : ['500', '400', '250'],
      rent : [55, 45, 50],
      products : ['청수동원룸', '삼룡동원룸', '가전리원룸'],
      styleGreen : 'color: #42b983',
      taps : ['Home', 'Shop', 'About'],
      reports : [0, 0, 0, 0, 0, 0],
      imgs: ['./static/room0.jpg', './static/room1.jpg', './static/room2.jpg'],
      modalOpen: false, // 기본을 false로 해서 modal window가 평소에는 off 되도록
      modalTitle: '',
      modalContent: ''
    }
  },
  methods: {  // 함수 작성
    increase() {
      this.reports++; // 'this'를 통해 data의 출처(data())를 명시
    },
    changeText() {
      let roomTitle = document.getElementsByClassName("room-nm");
      let modalDetail = document.getElementsByClassName("modal-detail");

      modalDetail.innerHTML = roomTitle.innerHTML;
    }
  },
  components: { // 컴포넌트 작성
    }
  }

// modal window api
const loremIpsum = document.getElementById("lorem-ipsum")
fetch("https://baconipsum.com/api/?type=all-meat&paras=200&format=html")
    .then(response => response.text())
    .then(result => loremIpsum.innerHTML = result)

</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h4:hover {
  color: #42b983;
  background-color: #2c3e50;
  -webkit-transition: 0.5s;
  -moz-transition: 0.5s;
  -o-transition: 0.5s;
  -ms-transition: 0.5s;
  transition: 0.5s;
}

.menu {
  background: #2c3e50;
  padding: 15px;
  border-radius: 10px;
}

/* 해당 class에 속한 모든 <a> tag에 적용 */
.menu a {
  color: white;
  padding: 10%;
}

.room-img {
  width: 50%;
  margin-top: 40px;
}

body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

/* modal window */
#modal {
  width: 100%;
  height: 100%;
  position: fixed;
  left: 0;
  top: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.25);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(1.5px);
  -webkit-backdrop-filter: blur(1.5px);
  border-radius: 10px;
  border: 1px solid rgba(255, 255, 255, 0.18);
}
#modal .modal-window {
  background: rgba( 69, 139, 197, 0.70 );
  box-shadow: 0 8px 32px 0 rgba( 31, 38, 135, 0.37 );
  backdrop-filter: blur( 13.5px );
  -webkit-backdrop-filter: blur( 13.5px );
  border-radius: 10px;
  border: 1px solid rgba( 255, 255, 255, 0.18 );
  width: 400px;
  height: 200px;
  position: relative;
  top: -50px;
  padding: 10px;
}

#modal .title {
  padding-left: 10px;
  display: inline;
  text-shadow: 1px 1px 2px #2c3e50;
  color: white;
}

#modal .title h2 {
  display: inline;
}

#modal .close-area {
  display: inline;
  float: right;
  padding-right: 10px;
  cursor: pointer;
  text-shadow: 1px 1px 2px gray;
  color: white;
}

#modal .content {
  margin-top: 20px;
  padding: 0px 10px;
  text-shadow: 1px 1px 2px #2c3e50;
  color: white;
}

/* 동적 UI 만드는 방법
  1. UI의 현재 상태를 데이터로 저장
  2. 데이터에 따라 UI가 어떻게 달라질지 작성
*/
</style>
