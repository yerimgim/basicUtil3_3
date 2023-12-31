<template>
  <section id="slider">
    <button class="button prev" @click="handlePrev">&lt;</button>
    <main id="wrapper" ref="wrapperRef">
      <ul id="items" ref="itemsRef">
        <li class="item" v-for="n in itemCount" :key="n">
          <div class="content" :class="getColorClass(n - 1)">
            {{ n }}
          </div>
        </li>
      </ul>
    </main>
    <button class="button next" @click="handleNext">&gt;</button>
  </section>
</template>

<script>
import { ref } from "vue";

export default {
  name: "CarouselSlider",
  setup() {
    const currentIdx = ref(0);
    const positions = ref([]);
    const wrapperRef = ref(null);
    const itemsRef = ref(null);
    const itemCount = 4;

    console.log("itemsRef", itemsRef.value);

    const colorClasses = ["pink", "yellow", "skyblue", "orange"];

    const getColorClass = (index) => {
      return colorClasses[index % colorClasses.length];
    };

    return { wrapperRef, itemsRef, getColorClass };
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
}
ul,
li {
  list-style: none;
}

#sldier {
  width: 100%;
  position: relative;
  margin: 0 auto;
  visibility: hidden;
}

#wrapper {
  width: 100%;
  height: 15rem;
  position: relative;
  overflow: hidden;
  cursor: grab;
  margin: 0 auto;
}

#items {
  width: 500%;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
}
#items.active {
  transition: 0.3s;
}

.item {
  width: 100%;
  pointer-events: none;
  position: relative;
  padding: 0 1rem;
  .content {
    width: 100%;
    height: 15rem;
    border: 1px solid #c8c8c8;
    box-shadow: 0 1rem 2.8rem rgba(0, 0, 0, 0.05);
    border-radius: 1rem;
    background-color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 700;
    font-size: 5rem;
    color: #fff;
  }
}

.content.pink {
  background: #dd80ab;
}
.content.yellow {
  background: #fce043;
}
.content.skyblue {
  background: #5bbbe7;
}
.content.orange {
  background: #fc9842;
}

.button {
  position: absolute;
  width: 3rem;
  height: 15rem;
  top: 0;
  z-index: 1;
  border: 0;
  background: rgba(250, 250, 250, 0.3);
  transition: 0.2s;
  cursor: pointer;
  font-size: 2rem;
  background: #c3c3c3;
  opacity: 0.3;
}

.button:hover {
  background: rgba(250, 250, 250, 0.5);
}

.button.prev {
  left: 0;
}
.button.next {
  right: 0;
}
</style>
