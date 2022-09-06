<template>
  <div>
    <img src="../../public/images/delete.png" alt="delete" @click="deleteMessage">
  </div>
</template>

<script>
export default {
  name: "DeleteMessage",
 props: {
   contact: {
     id: Number,
     name: String,
   }
 },
  methods: {
    deleteMessage(contact) {
      this.$emit('remove', contact.id)
    }
  }
}
</script>

<style scoped>



</style>
