<template>
  <div
    class="card"
    @mouseover="showDelete = true"
    @mouseleave="showDelete = false"
  >
    <div class="card-image">
      <img :src="product.image" :alt="product.title" />
    </div>
    <div class="card-content">
      <div class="card-content-title">{{ product.title }}</div>
      <span class="card-content-description">{{ product.description }}</span>
      <div class="card-content-price">{{ formattedPrice }}</div>
    </div>

    <transition name="slide-fade">
      <button
        class="delete-btn"
        :class="{ show: showDelete }"
        @click="deleteProduct"
      >
        <img src="../assets/img/delete-icon.svg" />
      </button>
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      default: () => {
        return {}
      }
    }
  },
  data() {
    return {
      showDelete: false
    }
  },
  computed: {
    formattedPrice() {
      return `${this.product.price.toLocaleString()} руб.`
    }
  },
  methods: {
    deleteProduct() {
      this.$emit('delete-product', this.product.id)
    }
  }
}
</script>

<style lang="scss" scoped>
.card {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: calc(100% / 3 - 16px);
  height: auto;
  background: $bg-element;
  box-shadow: $shadow-block;
  border-radius: $radius-default;
  margin: 0 8px 16px;
  position: relative;
  transition: all 0.3s;
  cursor: pointer;

  &:hover {
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.4);
    transform: translateY(-5px);
  }

  &-image {
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    max-height: 200px;
    border-top-left-radius: $radius-default;
    border-top-right-radius: $radius-default;
    img {
      width: 100%;
      height: auto;
      display: block;
      object-fit: cover;
    }
  }

  &-content {
    display: flex;
    flex-direction: column;
    padding: 16px 16px 24px;
    color: $color-primary;
    font-weight: 600;

    &-title {
      font-size: 20px;
      line-height: 25px;
      margin-bottom: 16px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    &-description {
      font-weight: 400;
      font-size: 16px;
      line-height: 20px;
      margin-bottom: 32px;
      height: 80px;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    &-price {
      font-size: 24px;
      line-height: 30px;
    }
  }

  &:nth-child(3n) {
    margin-right: 0;
  }
}

.delete-btn {
  width: 32px;
  height: 32px;
  background: $color-danger;
  box-shadow: $shadow-input;
  border-radius: $radius-higher;
  outline: none;
  border: none;
  position: absolute;
  right: -8px;
  top: -8px;
  transition: all 0.1s;
  display: none;
  &.show {
    display: block;
  }
  &:hover {
    background: #ff5757;
  }
}

.slide-fade-enter-active {
  transition: all 0.2s ease;
}
.slide-fade-leave-active {
  transition: all 0.2s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter,
.slide-fade-leave-to {
  opacity: 0;
}

@media (max-width: 1200px) {
  .card {
    width: calc(100% / 2 - 16px);
  }
}

@media (max-width: 992px) {
  .card {
    width: 100%;
  }
  .delete-btn {
    display: block;
  }
}

@media (max-width: 768px) {
  .card {
    width: calc(100% / 2 - 16px);
  }
}
@media (max-width: 600px) {
  .card {
    width: calc(100% - 16px);
  }
}
</style>
