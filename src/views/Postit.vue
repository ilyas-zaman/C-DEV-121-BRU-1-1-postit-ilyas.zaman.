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
        // console.log('data :', response.data);
        // eslint-disable-next-line no-underscore-dangle
        this.sticky.id = response.data.note._id;
        this.sticky.title = response.data.note.title;
        this.sticky.content = response.data.note.content;
      }).catch((error) => {
        console.log(error);
      });
    },
  },

});
</script>
