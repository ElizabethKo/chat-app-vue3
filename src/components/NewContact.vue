<template>
  <div v-if="show" class="modal" @click.stop="closeModal">
    <div class="modal-content" @click.stop>
    <input type="text" placeholder="name" v-model="contact.name" @keyup.enter="addNewContact">
    <button @click.stop="addNewContact">add new friend</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "NewContact",
  props: {
    show: {
      type: Boolean,
      required: false
    }
  },
  data() {
    return {
      openModal: true,
      contact: {
        id: Math.floor(Math.random()*20),
        name: ""
      },

    }
  },
  methods: {
    addNewContact() {
      if (this.contact.name === "") {
        return
      }
      this.$emit('newContact', this.contact);
      this.contact= {
        name: '',
        id: ''
      }
    },
    closeModal() {
      this.$emit('update:show', false);
    }
  }
}
</script>

<style scoped>
.modal {
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  display: flex;
}
.modal-content {
  margin: auto;
  background: white;
  border-radius: 12px;
  min-height: 50px;
  min-width: 300px;
  padding: 20px;
}
button {
  font-size: 12px;
  border-radius: 50px 50px 50px 50px;
  outline: none;
  border: none;
  background: whitesmoke;
  box-shadow: 1px 1px 3px 1px;
  color: black;
  margin: 7px;
  width: 75px;
  padding: 14px;
}
input {
  display: inline;
  font-size: 16px;
  border-radius: 50px 50px 50px 50px;
  outline: none;
  border: none;
  background: whitesmoke;
  box-shadow: 1px 1px 3px 1px;
  color: black;
  margin: auto;
  width: 170px;
  padding: 7px;
}

</style>
