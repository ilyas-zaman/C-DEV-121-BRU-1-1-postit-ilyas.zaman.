<template>
 <div class="home">
    <img alt="Vue logo" src="../assets/130616.png">
    <HelloWorld msg="POST - IT WORLD"/>
  </div>
  <h1>POST IT</h1>
<div id="nav">
<router-link to="/">HOME</router-link> |
<router-link to="/create">CREATE A POST-IT</router-link>
<div class="container">
</div>
<div class="post" v-for="notes in sticky" :key="notes">
  <ul>
  <li>
  <a href="#" v-bind:style='bgc'>

  <h2>{{ notes.title }}</h2>
  <p>{{ notes.content }}</p>

  <button className="button2"
  @click="this.$router.push({name: 'Edit', params: {id:notes._id}})">Edit</button>
  <button className="button" @click.prevent="this.deletePost(notes._id)">Delete</button>

  </a>
  </li>
  </ul>
</div>
</div>
</template>
<script>
import { defineComponent } from 'vue';
import axios from 'axios';
import '@/assets/global.css';

export default defineComponent({
  data() {
    return {
      sticky: [],
      bgc: {
        backgroundColor: '',
      },
    };
  },
  mounted() {
    this.getPost();
  },
  methods: {
    getPost() {
      axios.get('http://5.135.119.239:3090/notes').then((response) => {
        this.sticky = response.data.notes;
        console.log(response.data.notes);

        // eslint-disable-next-line no-bitwise
        // for (i = 0; i < response.data.notes.length; i++) {
        // eslint-disable-next-line no-bitwise
        const randomColor = `#${((1 << 24) * Math.random() | 0).toString(16)}`;
        this.bgc.backgroundColor = randomColor;
      }).catch((error) => {
        console.log(error);
      });
    },
    /* randomColors() {
      this.currentColor = this.colors[Math.floor(Math.random() * this.colors.length)];
    }, */

    deletePost(id) {
      axios.delete(`http://5.135.119.239:3090/notes/${id}`).then(() => {
        this.getPost();
      }).catch((error) => {
        console.log(error);
      });
    },
  },
});
</script>
<style>

</style>
