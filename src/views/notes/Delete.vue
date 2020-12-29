<template>
  <button ref="deleteNote" @click.prevent="destroyNote">Delete</button>
</template>

<script>
import axios from "axios";
export default {
  props: ["endpoint"],

  methods: {
    async destroyNote() {
      let q = window.confirm("Are you sure?");
      if (q == true) {
        let response = await axios.delete(`/api/notes/${this.endpoint}/delete`);
        if (response.status == 200) {
          this.$toasted.show(response.data.message, {
            type: "success",
            duration: 3000,
          });

          this.$refs.deleteNote.parentNode.parentNode.remove();
        }
      }
    },
  },
};
</script>
