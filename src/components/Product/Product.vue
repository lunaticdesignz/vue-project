<script lang="ts">
import Bookmark from '../icons/Bookmark.vue'
import { defineComponent } from 'vue'
import type { PropType } from 'vue'
import { Product } from '../../interface'

export default defineComponent({
  components: {
    Bookmark,
  },
  data() {
    return {
      // bookmarkAdded: false,
    }
  },
  computed: {
    // added() {
    //   return this.$store.getters['bookmarks/bookmarks'].filter(
    //     (e) => e.code === this.product.code,
    //   ).length
    // },
  },
  props: {
    product: {
      type: Object as PropType<Product>,
      default: {},
    },
  },
  methods: {
    // toggleBookmark(product) {
    //   this.$store.dispatch('bookmarks/toggleBookmark', {
    //     product: this.product,
    //   })
    //   console.log(this.$store.getters['bookmarks/bookmarks'])
    // },
  },
})
</script>

<template>
  <div class="container-wrapper">
    <div class="container">
      <div class="image-wrapper">
        <img
          class="first-image"
          src="https://res.cloudinary.com/baywa-ag-p/image/upload/A2542940.jpg"
          alt=""
        />
      </div>
      <span v-if="product.priceOffer" class="ribbon">Angebot</span>
      <div class="title-wrapper">
        <h4 class="title">{{ product.title }}</h4>
        <div v-if="product.variant" class="variant">
          {{ product.variant }} Varianten verfügbar
        </div>
      </div>

      <div class="price">
        <div class="old-price-wrapper">
          <span class="old-price">{{ product.oldPrice }} €</span>
        </div>
        {{ product.price }} € / Stück
      </div>

      <div class="availability">
        <div class="info">{{ product.info }} verfügbar</div>
        <!-- add a class to bars (low, medium or high) -->
        <div :class="product.availability" class="bars">
          <div class="bar"></div>
        </div>
      </div>
      <div class="buttons">
        <button class="bookmark">
          <Bookmark
            @click="toggleBookmark(product)"
            :class="{ 'primary-color': added }"
          />
        </button>
        <button class="buy">kaufen</button>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.container-wrapper {
  padding: 1rem;
  height: calc(100% - 2rem);

  .container {
    background-color: #fff;
    box-shadow: 0px 1rem 0.5rem -1rem gray;
    display: flex;
    flex-direction: column;
    position: relative;
    height: 100%;

    .image-wrapper {
      position: relative;
      height: 15rem;
      padding: 1rem;
      border-bottom: 1px solid #bbb;

      .first-image {
        position: absolute;
        width: 100%;
        height: 100%;
        max-width: calc(100% - 2rem);
        max-height: calc(100% - 2rem);
        object-fit: contain;
      }
    }

    .ribbon {
      top: 11.5rem;
      right: -0.3rem;
      position: absolute;
      padding: 0.25rem 0.5rem 0.5rem 0.5rem;
      color: #fff;
      background-color: #009650;
      font-weight: bold;
      border-top-right-radius: 0.2rem;
      box-shadow: 0 -5px 0 inset gray;

      clip-path: polygon(
        0 0,
        100% 0,
        100% calc(100% - 5px),
        calc(100% - 5px) 100%,
        calc(100% - 5px) calc(100% - 5px),
        0 calc(100% - 5px)
      );
    }

    .title-wrapper {
      flex: 1;
      .title {
        color: #4d4d4d;
        margin: 1rem 2rem 1rem 2rem;
        font-size: 1.1rem;
        word-wrap: break-word;
      }

      .variant {
        margin: 1rem 2rem 1rem 2rem;
        background-color: lightgray;
        color: gray;
        padding: 0.25rem 2rem 0.25rem 0.25rem;
        font-size: 0.75rem;
      }
    }

    .price {
      padding: 0 2rem;
      font-weight: bold;
      color: #4d4d4d;
      font-size: 1.25rem;
      margin-bottom: 1rem;
      display: flex;

      .old-price-wrapper {
        margin-right: 0.5rem;
        position: relative;
        white-space: nowrap;

        .old-price {
          color: gray;
        }

        .old-price::before {
          content: '';
          position: absolute;
          left: 0;
          width: 100%;
          height: 0;
          display: block;
          border-bottom: 2px solid red;
          top: 50%;
          transform: rotate(348deg);
        }
      }
    }

    .availability {
      margin-bottom: 0.5rem;

      .info {
        margin-bottom: 0.5rem;
        margin-left: 2rem;
        color: gray;
        font-size: 0.75rem;
      }

      .bars {
        display: flex;
        position: relative;

        .bar {
          width: 33%;
          height: 0.75rem;
          background-color: #cddc00;
        }

        .bar::before {
          content: '';
          width: 33%;
          height: 0.75rem;
          position: absolute;
          left: 33.5%;
          background-color: #cddc00;
        }

        .bar::after {
          content: '';
          width: 33%;
          height: 0.75rem;
          position: absolute;
          right: 0;
          background-color: #cddc00;
        }

        // low in store
        &.low .bar {
          background-color: #009650;
        }

        // medium in store
        &.medium .bar,
        &.medium .bar::before {
          background-color: #009650;
        }

        // high in store
        &.high .bar,
        &.high .bar::before,
        &.high .bar::after {
          background-color: #009650;
        }
      }
    }

    .buttons {
      display: flex;
      height: 3rem;

      .bookmark {
        width: 33%;
        border: none;
        cursor: pointer;
      }

      .buy {
        width: 67%;
        border: none;
        background-color: #009650;
        color: #fff;
        cursor: pointer;
      }
    }
  }
}

.primary-color {
  color: green;
}
</style>
