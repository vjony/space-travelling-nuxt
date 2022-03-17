/* eslint-disable vue/multi-word-component-names */
<template>
  <div class="container flow flex technology">
    <div id="content" v-if="technology">
      <h1 class="numbered-title"><span>03</span> SPACE LAUNCH 101</h1>
      <img :src="technology['image-landscape'].guid" alt="technology picture" />
      <ul class="dot-indicators flex">
        <li
          v-for="(item, index) in technologies"
          :key="item['technology-name']"
          @click="setTechnology(index)"
          class="tech-number"
        >
          {{ index + 1 }}
        </li>
      </ul>
      <h3 class="uppercase ff-sans-cond text-accent terminology">
        The Terminology...
      </h3>
      <h2 class="uppercase ff-serif technology-name">
        {{ technology['technology-name'] }}
      </h2>
      <p class="text-accent technology-description">
        {{ technology.description }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      technologies: [],
      activeTechnologyValue: 0,
    }
  },
  computed: {
    technology() {
      return this.technologies[
        this.technologies.length - 1 - this.activeTechnologyValue
      ]
    },
  },
  methods: {
    async loadData() {
      const response = await fetch(
        'https://space.wp.seiwald.hak-stjo.schulwebspace.at/wp-json/wp/v2/technology'
      )
      this.technologies = await response.json()
    },
    setTechnology(value) {
      this.activeTechnologyValue = value
    },
  },
  mounted() {
    this.loadData()
    document.body.style.backgroundImage =
      "url('background-technology-mobile.jpg')"
  },
}
</script>
<style scoped>
.numbered-title {
  font-size: 16px;
}
.dot-indicators {
  list-style-type: none;
  text-align: center;
  justify-content: center;
  margin-left: -50px;
}
.dot-indicators > *:hover {
  background-color: white;
  color: black;
}
.terminology {
  font-size: 14px;
  text-align: center;
  padding-bottom: 10px;
}
.technology-name {
  font-size: 24px;
  text-align: center;
  padding-bottom: 20px;
}
.technology-description {
  font-size: 15px;
  text-align: center;
  padding-bottom: 20px;
}
img {
  max-width: 100%;
  height: auto;
}
</style>