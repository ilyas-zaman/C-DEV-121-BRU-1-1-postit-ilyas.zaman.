<template>
<div id="nav">

</div>  <router-view />
<div v-for="notes in sticky" :key="notes">
<ul>
<li>
<a href="#">
<p class="toto">{{ notes._id }}</p>
<h2 contenteditable>{{ notes.title }}</h2>
<p contenteditable>{{ notes.content }}</p>
<button className="btn" @click.prevent="this.deletePost(notes._id)">Delete</button>
<button className="btn2" @click.prevent="this.getPoste(notes._id)">Edit</button>
</a>
</li>
</ul>
</div>
</template>
<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Home',
});
</script>
