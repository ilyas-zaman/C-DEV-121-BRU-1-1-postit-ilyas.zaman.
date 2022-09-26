<template>
<div id="nav">
<router-link to="/">BACK</router-link>

</div>
<ul>
  <li>
    <a href="#" contenteditable>
  <form>
    <input class="form" v-model="title" placeholder="title" required />
    <textarea v-model="content" placeholder="content" required />
    <div class="wrap">
    <button class="button3" type="button" @click.prevent="sendPost()">Create</button>
    </div>
    </form>
    </a>
  </li>
  </ul>
</template>

<script>
import axios from 'axios';
import '@/assets/global.css';

export default {
  data() {
    return {

      title: '',
      content: '',
    };
  },
  methods: {
    sendPost() {
      const postData = { title: this.title, content: this.content };
      axios
        .post('http://5.135.119.239:3090/notes', postData)
        .then((res) => {
          console.log(res.content);
          // this.$router.push('/');
          this.$router.push('/');
        }).catch((error) => {
          console.log(error);
        });
    },
  },
};

</script>
