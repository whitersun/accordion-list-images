<template>
  <ion-slides mode="md" ref="slides" :options="slidesOptions">
    <ion-slide v-for="(item, i) in data" :key="i">
      <!-- <img :src="item.image" :alt="item.title" class="img-fluid" /> -->
      <img
        v-lazy="{ src: item.image, lifecycle: lazyOptions.lifecycle }"
        class="img-fluid skeleton-img custom-rounded"
      />
    </ion-slide>
  </ion-slides>
</template>

<script lang="ts">
import { defineComponent, reactive, ref, onMounted } from "vue";
import { IonSlides, IonSlide } from "@ionic/vue";

export default defineComponent({
  name: "slider",
  components: { IonSlides, IonSlide },

  setup() {
    const data = reactive([
      { title: "image1", image: "https://source.unsplash.com/random/1230x728?sig=1" },
      { title: "image2", image: "https://source.unsplash.com/random/1230x728?sig=2" },
      { title: "image3", image: "https://source.unsplash.com/random/1230x728?sig=3" },
      { title: "image4", image: "https://source.unsplash.com/random/1230x728?sig=4" },
      { title: "image5", image: "https://source.unsplash.com/random/1230x728?sig=5" },
    ]);

    const slides: any = ref(null);

    const lazyOptions: any = reactive({
      src: "your image url",
      lifecycle: {
        loading: () => {
          console.log("image loading");
        },
        error: () => {
          console.log("image error");
        },
        loaded: () => {
          console.log("image loaded");
        },
      },
    });

    const slidesOptions = {
      on: {
        beforeInit: async function () {
          const swiper: any = this;

          const overwriteParams = {
            slidesPerView: 1.5,
            spaceBetween: 10,
            freeMode: true,

            // this maybe help swiper not fired or
            // not working after platform app to mobile (android: apk, ios: pad)
            observer: true,
            observeParents: true,
            observeSlideChildren: true,
          };

          swiper.params = await Object.assign(swiper.params, overwriteParams);
          swiper.originalParams = await Object.assign(
            swiper.originalParams,
            overwriteParams
          );
        },
      },
    };

    onMounted(() => {
      // this statement not sure maybe does it work on phone after platform to app
      // and use on mobile (android, ios)
      document.onreadystatechange = async () => {
        if (document.readyState == "complete") {
          //   const UpdateSwiper = await slides?.value?.$el.getSwiper();
          await slides?.value?.$el.update();
        }
      };
    });

    return { data, slidesOptions, lazyOptions };
  },
});
</script>

<style lang="scss" scoped>
$skeleton-color: #e0e0e0;
$skeleton-width: 100vw;
$skeleton-offset: 50px;

$image-height: 25rem;

@mixin background {
  background-image: linear-gradient(
    90deg,
    $skeleton-color 0px,
    lighten($skeleton-color, 5%) 30px,
    $skeleton-color 60px
  );
  background-size: calc(#{$skeleton-width} + #{$skeleton-offset});
}

ion-slides {
  ion-slide {
    padding: 4rem 1.5rem 3rem 3rem;

    img {
      border-radius: 5px;
      box-shadow: 5px 5px 45px rgba(#161616, 35%);
      object-fit: cover;

      &.img-fluid {
        max-width: 100%;
        width: 100%;
      }

      &.custom-rounded {
        border-radius: 5px;
      }

      &.skeleton-img {
        @include background;

        height: $image-height;
        animation: refresh 2s infinite ease-out;
      }

      @keyframes refresh {
        0% {
          background-position: calc(-#{$skeleton-offset});
        }

        40%,
        100% {
          background-position: $skeleton-width;
        }
      }
    }
  }
}
</style>
