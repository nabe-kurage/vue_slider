<template>
  <div class="pageContainer">
    <div class="sliderWrapper">
      <div class="sliderInner">
        <ul class="slider">
          <transition :name="moveType">
            <li
              v-for="(url, index) in urls"
              v-if="index === sliderIndex"
              class="slider__item"
              :key="index"
            >
              <img :src="url" alt="" width="300" height="150">
            </li>
          </transition>
        </ul>
      </div>
      <div
          class="sliderButton sliderButton__prev"
          @click="changeIndex(sliderIndex-1)"
        ></div>
        <div
          class="sliderButton sliderButton__next"
          @click="changeIndex(sliderIndex+1)"
        ></div>
      <ul class="pagenation">
        <li
          v-for="(url, index) in urls"
          :class="index === sliderIndex ? 'pagenation__item pagenation__item--active': 'pagenation__item'"
          :key="index"
          @click="changeIndex(index)"
        ></li>
      </ul>
      </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      urls: [
        'http://placehold.jp/24/1a508b/fff3e6/300x150.png',
        'http://placehold.jp/24/c1a1d3/fff3e6/300x150.png',
        'http://placehold.jp/24/fff3e6/1a508b/300x150.png',
      ],
      sliderIndex: 0,
      moveType: 'next'
    }
  },
  methods: {
    changeIndex(num){
      if( this.sliderIndex < num) {
        this.moveType = 'next';
      }else {
        this.moveType = 'prev';
      }
      this.sliderIndex = num;
      if(this.sliderIndex < 0) {
        this.sliderIndex = this.urls.length - 1;
      }else if (this.sliderIndex > this.urls.length - 1) {
        this.sliderIndex = 0;
      }
    }
  }
}
</script>

<style lang="scss">
ul {
  list-style: none;
}
.pageContainer {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.slider{
  display: flex;
  padding: 0;
  overflow: hidden;
  width: 300px;
  height: 150px;

  &__item {
    width: 300px;
    height: 150px;
    position: absolute;
  }
}

.sliderWrapper {
  position: relative;
}

.sliderInner {
  position: relative;
  overflow: hidden;
}

.sliderButton{
  width: 0;
  height: 0;
  border-style: solid;
  position: absolute;
  top: 0;
  bottom: 0;
  margin: auto;
  cursor: pointer;

  &__prev {
    border-width: 15px 25px 15px 0;
    border-color: transparent #007bff transparent transparent;
    left: -8px;
    transform: translate(-100%, -18px);
  }

  &__next {
    border-width: 15px 0 15px 25px;
    border-color: transparent transparent transparent #007bff;
    right: -8px;
    transform: translate(100%, -18px);
  }
}

.pagenation{
  display: flex;
  justify-content: center;
  margin-top: 16px;
  padding: 0;

  &__item {
    cursor: pointer;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    border: 2px solid gray;

    & + & {
      margin-left: 16px;
    }

    &--active {
      background: gray;
    }
  }
}

.next-enter-active,
.next-leave-active,
.prev-enter-active,
.prev-leave-active  {
  transition: all .2s ease-in-out;
}

.next-enter,
.prev-leave-to,  {
  transform: translateX(300px);
}

.next-leave-to,
.prev-enter {
  transform: translateX(-300px);
}

.next-enter-to,
.next-leave,
.prev-enter-to,
.prev-leave {
  transform: translateX(0);
}


</style>
