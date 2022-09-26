<template>
<div id="nav">
<router-link to="/">BACK</router-link>
</div>

<ul>
<li>
<a href="#">

<input class="form" v-model="sticky.title" placeholder="title" required />
<textarea v-model="sticky.content" placeholder="content" required />
<div class="wrap_div">
<button @click.prevent="submitPost()">Submit Post</button>
</div>
</a>
</li>
</ul>
</template>

<script>
import { defineComponent } from 'vue';
import axios from 'axios';
import '@/assets/global.css';

export default defineComponent({
  data() {
    return {
      sticky: [],
    };
  },
  mounted() {
    this.getPost();
  },
  methods: {
    getPost() {
      axios.get(`http://5.135.119.239:3090/notes/${this.$route.params.id}`).then((response) => {
        // eslint-disable-next-line no-underscore-dangle
        console.log('data :', response.data);
        // eslint-disable-next-line no-underscore-dangle
        this.sticky.id = response.data.note._id;
        this.sticky.title = response.data.note.title;
        this.sticky.content = response.data.note.content;
      }).catch((error) => {
        console.log(error);
      });
    },
    submitPost() {
      console.log(this.sticky.title);
      const post = {
        title: this.sticky.title,
        content: this.sticky.content,
      };
      axios.put(`http://5.135.119.239:3090/notes/${this.$route.params.id}`, post).then((result) => {
        this.$router.push('/');
      }).catch((error) => {
        console.log(error);
      });
    },

  },

});

</script>
