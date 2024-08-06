<template>
  <main class="gallery" @click="init">
    <div class="item" v-for="(item, index) in items" :key="index" :data-pos="item.pos">
      <img :src="item.src" />
    </div>
  </main>
</template>

<script>
export default {

  data() {
    return {
      message: 'Welcome to Vue!',
      items: [
        { pos: 0, src: 'https://picsum.photos/300/300?random=1' },
        { pos: 1, src: 'https://picsum.photos/300/300?random=2' },
        { pos: 2, src: 'https://picsum.photos/300/300?random=3' },
        { pos: 3, src: 'https://picsum.photos/300/300?random=4' },
        { pos: 4, src: 'https://picsum.photos/300/300?random=5' },
      ]
    };
  },

  methods: {
    init(e) {
      const target = e.target.closest('.item');
      if (!target) return;
      const hero = this.$el.querySelector('div[data-pos="0"]');
      [target.dataset.pos, hero.dataset.pos] = [hero.dataset.pos, target.dataset.pos];
      this.updateItems();
    },

    updateItems() {
      this.items = Array.from(this.$el.querySelectorAll('.item')).map(item => ({
        pos: parseInt(item.dataset.pos, 10),
        src: item.querySelector('img').src
      })).sort((a, b) => a.pos - b.pos);
    }
  }


};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin-top: 1rem;
}

.gallery {
  position: relative;
  width: 760px;
  height: 305px;
  margin: 0 auto;
}

.gallery:hover :not(div[data-pos='0'], img) {
  cursor: pointer;
}

.gallery .item {
  position: absolute;
  width: 175px;
  height: 150px;
  overflow: hidden;
  transition: transform 0.9s, width 0.9s, height 0.9s;
}

.gallery .item img {
  width: 100%;
  height: 100%;
}

.gallery div[data-pos='0'] {
  width: 400px;
  height: inherit;
  z-index: 10;
}

div[data-pos='0'] {
  transform: translate(0, 0);
}

div[data-pos='1'] {
  transform: translate(405px, 0);
}

div[data-pos='2'] {
  transform: translate(585px, 0);
}

div[data-pos='3'] {
  transform: translate(405px, 155px);
}

div[data-pos='4'] {
  transform: translate(585px, 155px);
}

@media (max-width: 800px) {
  .gallery {
    width: 405px;
    height: 660px;
  }

  .gallery .item {
    width: 200px;
    height: 150px;
  }

  .gallery div[data-pos='0'] {
    width: inherit;
    height: 350px;
    z-index: 10;
  }

  div[data-pos='0'] {
    transform: translate(0, 0);
  }

  div[data-pos='1'] {
    transform: translate(0, 355px);
  }

  div[data-pos='2'] {
    transform: translate(0, 510px);
  }

  div[data-pos='3'] {
    transform: translate(205px, 355px);
  }

  div[data-pos='4'] {
    transform: translate(205px, 510px);
  }
}
</style>