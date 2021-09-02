<template>
  <div class="">
    <client-only>
      <div class="example-3d">
        <swiper ref="mySwiper" class="swiper" :options="swiperOptions">
          <swiper-slide>Slide 1</swiper-slide>
          <swiper-slide>Slide 2</swiper-slide>
          <swiper-slide>Slide 3</swiper-slide>
          <swiper-slide>Slide 4</swiper-slide>
          <swiper-slide>Slide 5</swiper-slide>
          <div slot="pagination" class="swiper-pagination"></div>
        </swiper>
      </div>

      <carousel-3d>
        <slide :index="0"> Slide 1 Content </slide>
        <slide :index="1"> Slide 2 Content </slide>
        <slide :index="2"> Slide 3 Content </slide>
        <slide :index="3"> Slide 4 Content </slide>
        <slide :index="4"> Slide 5 Content </slide>
        <slide :index="5"> Slide 6 Content </slide>
        <slide :index="6"> Slide 7 Content </slide>
        <slide :index="7"> Slide 8 Content </slide>
      </carousel-3d>
    </client-only>

    <News :articles="news" />
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const news = await $content('news')
      .only(['title', 'description', 'img', 'slug', 'author', 'updatedAt'])
      .sortBy('createdAt', 'asc')
      .fetch()

    return {
      news
    }
  },
  data() {
    return {
      swiperOptions: {
        pagination: {
          el: '.swiper-pagination'
        },
        effect: 'coverflow',
        grabCursor: true,
        centeredSlides: true,
        slidesPerView: 'auto',
        coverflowEffect: {
          rotate: 50,
          stretch: 0,
          depth: 100,
          modifier: 1,
          slideShadows: true
        }
      }
    }
  },
  computed: {
    swiper() {
      return this.$refs.mySwiper.$swiper
    }
  },
  mounted() {
    setTimeout(() => {
      this.swiper.slideTo(3, 1000, false)
    })
  },
  methods: {}
}
</script>

<style lang="scss" scoped>
.nuxt-content h2 {
  font-weight: bold;
  font-size: 28px;
}
.nuxt-content p {
  margin-bottom: 20px;
}

.example-3d {
  width: 100%;
  height: 300px;
  padding-top: 50px;
  padding-bottom: 50px;
}

.swiper {
  height: 100%;
  width: 100%;

  .swiper-slide {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 300px;
    height: 300px;
    text-align: center;
    font-weight: bold;
    font-size: 24px;
    background-color: #2c8dfb;
    background-position: center;
    background-size: cover;
    color: #fff;
  }

  .swiper-pagination {
    ::v-deep .swiper-pagination-bullet.swiper-pagination-bullet-active {
      background-color: #fff;
    }
  }
}
</style>
