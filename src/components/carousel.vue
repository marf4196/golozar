<template>
  <Carousel :items-to-show="items.length "  :breakpoints="breakpoints" class="py-4">
    <Slide v-for="slide in items" :key="slide">
      <div class="carousel__item">
        <h5 class="mb-2">{{ slide.substring(0,10) }}</h5>
        <h5 class="mb-0">{{ slide.substring(11,16) }}</h5>
        <!-- <h4>Oct</h4> -->
      </div>
    </Slide>

    <template #addons>
      <Navigation />
    </template>
  </Carousel>
</template>

<script>
import { defineComponent } from 'vue'
import { Carousel, Navigation, Slide } from 'vue3-carousel'

export default defineComponent({
  name: 'WrapAround',
  props: {
    items : Array
  },
  components: {
    Carousel,
    Slide,
    Navigation,
  },
  data: () => ({
    // carousel settings
    settings: {
      itemsToShow: 1,
      snapAlign: 'center',
    },
    // breakpoints are mobile first
    // any settings not specified will fallback to the carousel settings
    breakpoints: {
      // 300px and up
      300: {
        itemsToShow: 1,
        snapAlign: 'center',
      },
      // 700 and up
      700: {
        itemsToShow: 2,
        snapAlign: 'center',
      },
    },
  })
})
</script>

<style>
.carousel__track {
    padding-top: 10px !important;
    padding-bottom: 10px !important;
}

.carousel__item {
    background-color: #ffffff;
    padding: 12px 30px;
    border-radius: 12px;
    cursor: pointer;
    box-shadow: 0px 0px 10px rgb(56 79 108 / 8%);
}

.carousel__icon {
  width: var(--vc-icn-width);
  height: var(--vc-icn-width);
  fill: currentColor;
}
:root {
  /* Color */
  --vc-clr-primary: #000;
  --vc-clr-secondary: #090f207f;
  --vc-clr-white: #ffffff;

  /* Icon */
  --vc-icn-width: 1.2em;

  /* Navigation */
  --vc-nav-width: 30px;
  --vc-nav-height: 30px;
  --vc-nav-border-radius: 0;
  --vc-nav-color: var(--vc-clr-primary);
  --vc-nav-color-hover: var(--vc-clr-secondary);
  --vc-nav-background: transparent;

  /* Pagination */
  --vc-pgn-width: 12px;
  --vc-pgn-height: 4px;
  --vc-pgn-margin: 4px;
  --vc-pgn-border-radius: 0;
  --vc-pgn-background-color: var(--vc-clr-secondary);
  --vc-pgn-active-color: var(--vc-clr-primary);
}
.carousel {
  position: relative;
  text-align: center;
  box-sizing: border-box;
}

.carousel * {
  box-sizing: border-box;
}

.carousel__track {
  display: flex;
  margin: 0;
  padding: 0;
  position: relative;
}

.carousel__viewport {
  overflow: hidden;
}

.carousel__sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
.carousel__slide {
  scroll-snap-stop: auto;
  flex-shrink: 0;
  margin: 0;
  position: relative;

  display: flex;
  justify-content: center;
  align-items: center;

  /* Fix iOS scrolling #22 */
  transform: translateZ(0);

}
.carousel__pagination {
  display: flex;
  justify-content: center;
  list-style: none;
  line-height: 0;
  margin: 10px 0 0;
}

.carousel__pagination-button {
  display: block;
  border: 0;
  margin: 0;
  cursor: pointer;
  padding: var(--vc-pgn-margin);
  background: transparent;
}

.carousel__pagination-button::after {
  display: block;
  content: '';
  width: var(--vc-pgn-width);
  height: var(--vc-pgn-height);
  border-radius: var(--vc-pgn-border-radius);
  background-color: var(--vc-pgn-background-color);
}

.carousel__pagination-button:hover::after,
.carousel__pagination-button--active::after {
  background-color: var(--vc-pgn-active-color);
}
.carousel__prev,
.carousel__next {
  box-sizing: content-box;
  background: var(--vc-nav-background);
  border-radius: var(--vc-nav-border-radius);
  width: var(--vc-nav-width);
  height: var(--vc-nav-height);
  text-align: center;
  font-size: var(--vc-nav-height);
  padding: 0;
  color: var(--vc-nav-color);
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  border: 0;
  cursor: pointer;
  margin: 0 10px;
  top: 50%;
  transform: translateY(-50%);
}

.carousel__prev:hover,
.carousel__next:hover {
  color: var(--vc-nav-color-hover);
}

.carousel__next--disabled,
.carousel__prev--disabled {
  cursor: not-allowed;
  opacity: 0.5;
}

.carousel__prev {
  left: 0;
}

.carousel__next {
  right: 0;
}

.carousel--rtl .carousel__prev {
  left: auto;
  right: 0;
}

.carousel--rtl .carousel__next {
  right: auto;
  left: 0;
}

@media (max-width: 768px) {
  .carousel__item {
    padding: 8px 20px;
  }

  .carousel__slide {
    width: 100% !important;
  }
}
</style>