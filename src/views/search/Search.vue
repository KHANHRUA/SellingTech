<template>
  <div class="Container">
    <div class="nav">
      <RouterLink to="/" class="path"> Trang chủ </RouterLink>
      <h2 v-for="(part, index) in this.nav" :key="index" class="path">/ {{ part.name }}</h2>
    </div>
    <div class="temp1">
      <div class="left">
        <div class="CoreIndex">
          <div class="Text"><Rank></Rank>Danh mục</div>
          <ul>
            <li
              class="list"
              v-for="(part, index) in Index.type"
              :key="index"
              @click="Search(0, part.name)"
            >
              {{ part.name }}
              <Down v-if="part.children.length !== 0" class="Triangle"></Down>
              <ul class="HoverList">
                <li
                  v-for="(part1, index1) in part.children"
                  :key="index1"
                  @click="Search(part.name, part1.name)"
                >
                  {{ part1.name }}
                </li>
              </ul>
            </li>
          </ul>
        </div>
        <div class="CoreIndex">
          <div class="Text"><Rank></Rank>Lọc theo giá</div>
          <div class="box">
            <div>từ {{ this.min }}đ : {{ this.max }}đ</div>
            <div
              id="volume-control"
              ref="volumeControl"
            >
              <div id="handle" @mousedown="startDrag"
              @mouseup="endDrag" ref="handle"></div>
              <div id="line"></div>
              <div id="handle1" @mousedown="startDrag1"
              @mouseup="endDrag1" ref="handle1"></div>
            </div>
          </div>
        </div>
      </div>
      <div class="right">
        <div class="Sort">
          Display:
          <Stack class="Stack"></Stack>
          <Rubik class="Rubik"></Rubik>
          Tìm kiếm theo
          <select class="Option" onchange="selectOption()">
            <option value= 1>mới nhất</option>
            <option value= 2>Tăng dần</option>
            <option value= 3>Giảm dần</option>
            <option value= 4>Sale</option>
          </select>
          Hiển thị:
          <h2 class="type">15</h2>
          |
          <h2 class="type">30</h2>
          |
          <h2 class="type">45</h2>
        </div>
        <div class="CoreData">
          <div v-for="(part1, index1) in Data.data.product" :key="index1" class="Product">
          <div class="ButtonHover">
            <button @click="On(part1)" class="Eyes">
              <Eyes></Eyes>
            </button>
            <button class="Heart">
              <Heart></Heart>
            </button>
          </div>
          <img :src="`${part1.url}`" alt="error" class="Img" />
          <div class="Name">
            {{ part1.name }}
          </div>
          <div class="Price">{{ part1.price }} VNĐ</div>
          <div class="Rate">
            <div
              v-for="n of Array.from({ length: part1.rate / 2 }, (_, index) => index + 1)"
              :key="n"
            >
              <Star></Star>
            </div>
            <div v-if="part1.rate % 2 === 1">
              <StarHalf></StarHalf>
            </div>
            <div v-if="part1.rate % 2 === 0 && part1.rate / 2 != 5">
              <StarEmpty></StarEmpty>
            </div>
            <div
              v-for="n of Array.from({ length: 4.5 - part1.rate / 2 }, (_, index) => index + 1)"
              :key="n"
            >
              <StarEmpty></StarEmpty>
            </div>
          </div>
          <button @click="AddToCart(part1)">MUA NGAY</button>
        </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import Index from './Index.json'
import Rank from '../../components/icons/Rank.vue'
import Down from '../../components/icons/Down.vue'
import Data from './Data.json'
import Stack from '../../components/icons/Stack.vue'
import Rubik from '../../components/icons/Rubik.vue'
import Heart from '../../components/icons/Heart.vue'
import Eyes from '../../components/icons/Eyes.vue'
import Star from '../../components/icons/Star.vue'
import StarHalf from '../../components/icons/StarHalf.vue'
import StarEmpty from '../../components/icons/StarEmpty.vue'
</script>

<script>
export default {
  name: 'search',
  data() {
    return {
      nav: sessionStorage.search,
      min: '0',
      maxConst: '10,000,000',
      max: '10,000,000',
      percentMax: 1,
      percentMin: 0,
      Data: undefined,
      default: 15,
      page: 1,
      Object:[[]]
    }
  },
  methods: {
    startDrag() {
      const handle = this.$refs.handle
      handle.style.cursor = 'grabbing'
      window.addEventListener('mousemove', this.handleMouseMove);
    },
    startDrag1() {
      const handle = this.$refs.handle1
      handle.style.cursor = 'grabbing'
      window.addEventListener('mousemove', this.handleMouseMove1);
    }
    ,
    handleMouseMove(event) {
      // Access the mouse coordinates
      const mouseX = event.clientX;

      // Perform actions based on the mouse position
        const volumeControl = this.$refs.volumeControl
        const handle = this.$refs.handle
        let line = document.getElementById("line")
        let volumePercentage =
          (event.clientX - volumeControl.getBoundingClientRect().left) / volumeControl.offsetWidth
      let price = parseFloat(String(this.maxConst).replace(/,/g, ''))
        // Update the handle position
        if (volumePercentage >= 0 && volumePercentage <= this.percentMax ) {
          console.log(volumePercentage)
          if (volumePercentage < 0.005) {
            volumePercentage = 0;
          }
          if (volumePercentage > this.percentMax - 0.005) {
            volumePercentage = this.percentMax;
          }
          price = parseInt(price * volumePercentage);
          price = price.toLocaleString('en-US')
          this.min = price;
          handle.style.left = `${event.clientX - volumeControl.getBoundingClientRect().left - 15}px`
          this.percentMin = volumePercentage;
          line.style.marginLeft = `${event.clientX - volumeControl.getBoundingClientRect().left}px`
        }
    },handleMouseMove1(event) {
      // Access the mouse coordinates
      const mouseX = event.clientX;
      let line = document.getElementById("line")
      // Perform actions based on the mouse position
        console.log("Mouse move", mouseX);
        const volumeControl = this.$refs.volumeControl
        const handle = this.$refs.handle1
        let volumePercentage =
          (event.clientX - volumeControl.getBoundingClientRect().left) / volumeControl.offsetWidth
        let price = parseFloat(String(this.maxConst).replace(/,/g, ''))
        // Update the handle position
        if (volumePercentage >= this.percentMin && volumePercentage <= 1) {
          console.log(volumePercentage)
          if (volumePercentage < this.percentMin + 0.005) {
            volumePercentage = this.percentMin;
          }
          if (volumePercentage > 0.995) {
            volumePercentage = 1;
          }
          price = parseInt(price * volumePercentage);
          price = price.toLocaleString('en-US')
          this.max = price;
          handle.style.left = `${event.clientX - volumeControl.getBoundingClientRect().left - 15}px`
          this.percentMax = volumePercentage;
          line.style.marginRight = `${volumeControl.offsetWidth-(event.clientX - volumeControl.getBoundingClientRect().left)}px`
        }
    },
    endDrag() {
      const handle = this.$refs.handle
      handle.style.cursor = 'grab'
      window.removeEventListener("mousemove",this.handleMouseMove)
    },
    endDrag1() {
      const handle = this.$refs.handle1
      handle.style.cursor = 'grab'
      window.removeEventListener("mousemove",this.handleMouseMove1)
    }
  },
  mounted() {
    this.nav = JSON.parse(this.nav)
    const changecolor = document.getElementsByClassName('path')
    changecolor[this.nav.length].style.color = '#31beff';

    this.Data = Data.data.product;
    // for (let i = 0; i < this.Object.length; i++){
    //   for (let j = 0; j < 15; j++){
    //     this.Object[this.page].push(this.Data[i])
    //   }
    //   if (i != this.Object.length - 1) {
    //     this.page = this.page + 1;
    //   }
    // }
  }
}
</script>

<style scoped src="./Search.css"></style>
