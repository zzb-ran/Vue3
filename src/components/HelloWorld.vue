<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <ul>
      <li v-for="item in data" @click="handleLink(item.link)">
        <a
          :class="{ active: item.link === activeLink }"
          :href="`#${item.link}`"
          >{{ item.text }}</a
        >
      </li>
    </ul>
    <h2
      :ref="setH2List"
      :id="item.link"
      v-for="item in data"
      :style="{ color: item.color }"
    >
      {{ item.text }}
    </h2>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import data from '../data.js';

export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  setup() {
    const activeLink = ref(null);
    const h2List = ref([]);

    const handleLink = (link) => {
      activeLink.value = link;
    };

    const setH2List = (el) => {
      h2List.value.push(el);
    };

    const onScroll = () => {
      const offsetTopList = [];
      const scrollTop =
        document.documentElement.scrollTop || document.body.scrollTop;
      let activeIndex = 0;

      h2List.value.forEach((el) => {
        offsetTopList.push(el.offsetTop);
      });

      for (let i = 0; i < offsetTopList.length; i++) {
        if (scrollTop > offsetTopList[i]) {
          activeIndex = i;
        }
      }

      // activeLink.value = data[activeIndex].link;
      console.log(data[activeIndex].link);
    };

    onMounted(() => {
      window.addEventListener('scroll', onScroll, false);
    });

    return {
      data,
      activeLink,
      handleLink,
      setH2List,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  padding-bottom: 30px;
}
h2 {
  height: 80vh;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  position: fixed;
  right: 10px;
  top: 10px;
  text-align: left;
}
li {
  display: inline-block;
  margin: 10px 0 0 0;
}
a {
  color: #42b983;
}
a.active {
  color: red;
}
</style>
