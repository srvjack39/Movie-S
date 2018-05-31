<template>
  <div class="contrainer">
    <div class="columns">
      <div class="column is-6 offset-1">
        <label class="title is-2">ชื่อหนัง : {{movieSelected}} ราคา : {{cost}}</label>
      </div>
    </div>

    <div class="columns is-centered box">
      <div class="column is-2">
        <a @click="select('hug-paeng')">
      <img src="../assets/hug-paeng.jpg" alt="">
      </a>
      <br>
      <label class="title is-2">ฮักแพง</label>
      </div>

      <div class="column is-2">
        <a @click="select('deadpool-2')">
      <img src="../assets/deadpool-2.jpg" alt="">
      </a>
      <br>
      <label class="title is-2">เดดพูล 2</label>
      </div>

      <div class="column is-2">
        <a @click="select('toot-too-ku-chart')">
      <img src="../assets/toot-too-ku-chart.jpg" alt="">
      </a>
      <br>
      <label class="title is-2">ตุ๊ดตู่กู้ชาติ</label>
      </div>

      <div class="column is-2">
        <a @click="select('nongpeeteerak')">
      <img src="../assets/nongpeeteerak.jpg" alt="">
      </a>
      <br>
      <label class="title is-2">น้อง พี่ ที่รัก</label>
      </div>

      <div class="column is-2">
        <a @click="select('infinity-war')">
      <img src="../assets/avengers-infinity-war.jpg" alt="">
      </a>
      <br>
      <label class="title is-2">infinity war</label>
      </div>

      <div class="column is-2">
        <a @click="select('peter-rabbit')">
      <img src="../assets/peter-rabbit.jpg" alt="">
      </a>
      <br>
      <label class="title is-2">ปีเตอร์แรบบิท</label>
      </div>
    </div>
    <br><br>
    <div class="columns is-centered">

         <label class="title is-2">จองที่นั่ง</label>
         <br><br><br>
      </div>
        <div class="columns is-centered">
          <div v-for="(d,index) in seat" :key="index">
            <div v-if="!d.seated">
                <div v-if="d.status !== 'disable'">
                  <button class="button is-medium is-success is-outlined" @click="selectSeat(d.id,d.price,index)"> {{d.id}}({{d.price}}) </button>
                </div>
                <div v-else>
                  <button class="button is-medium is-primary" disabled> {{d.id}}({{d.price}}) </button>
                </div>
            </div>
            <div v-else>
                <button class="button is-medium is-danger" disabled> {{d.id}}({{d.price}}) </button>
            </div>
          </div>
    </div>
    </div>
</template>

<script>
import data from '../Others/movie.json'
export default {
  name: 'HelloWorld',
  data () {
    return {
      data,
      movieSelected: '',
      selectedSeat: []
    }
  },
  methods: {
    select (title) {
      this.movieSelected = title
    },
    selectSeat (id, price, index) {
      this.selectedSeat.push({
        id,
        price
      })
      this.seat[index].status = 'disable'
    }
  },
  computed: {
    seat () {
      if (this.movieSelected === 'hug-paeng') {
        return this.data.hug
      } else if (this.movieSelected === 'deadpool-2') {
        return this.data.deadpool
      } else if (this.movieSelected === 'toot-too-ku-chart') {
        return this.data.toot
      } else if (this.movieSelected === 'nongpeeteerak') {
        return this.data.nongpeeteerak
      } else if (this.movieSelected === 'infinity-war') {
        return this.data.infinity
      } else if (this.movieSelected === 'peter-rabbit') {
        return this.data.peter
      }
    },
    cost () {
      return this.selectedSeat.reduce((cost, s) => cost + s.price, 0)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
