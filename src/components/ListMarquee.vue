<template>
  <div ref="marquee" class="rowup">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name:'list-marquee',
  props: {
    //每条滚动耗时，单位s
    interval: {
      type: Number,
      default: 1
    },
    //每屏显示多少条
    rowCount: {
      type: Number,
      default: 5
    },
    //每条数据高度
    rowHeight: {
      type: Number,
      default: 30
    }
  },
  data() {
    return {
      itemCount: 0
    };
  },
  methods: {
    /**
     * 将前`rowCount`个元素复制一份添加到末尾，使每一屏滚动完之后无缝衔接
     */
    fixMarquee() {
      Array.from(this.$refs.marquee.children)
        .slice(0, this.rowCount)
        .forEach(d => {
          this.$refs.marquee.appendChild(d.cloneNode(true));
        });
    },
    startMarquee() {
      const height = this.itemCount * this.rowHeight;
      const duration = this.itemCount * this.interval;
      this.$refs.marquee.style.setProperty("--height", `-${height}px`);
      this.$refs.marquee.style.setProperty("--duration", `${duration}s`);
    }
  },
  mounted() {
    //超过`rowCount`条才滚动
    this.itemCount = this.$refs.marquee.children.length;
    if (this.itemCount < this.rowCount) return;

    setTimeout(() => {
      this.fixMarquee();
      this.startMarquee();
    }, this.interval * 1000);
  }
};
</script>

<style scoped>
@keyframes rowup {
  0% {
    transform: translate3d(0, 0, 0);
  }
  100% {
    transform: translate3d(0, var(--height), 0);
  }
}

.rowup {
  animation: var(--duration) rowup linear infinite normal;
  position: relative;
}
</style>
