<template>
  <div @click.prevent>

    <textarea
        ref="focusRef"
        class="textarea-container"
        placeholder="Type your message"
        v-model="messageText"
        @keyup.enter="sendMessage"
    ></textarea>
    <button class="send" @click.stop="sendMessage">Send</button>
  </div>
</template>

<script>


export default {
  name: "SendMessage",
  props: {
    contact:
        {
          id: Number,
          name: String,
        },
  },
  data() {
    return {
      messageText: '',
      item: {
        image: null,
        imageUrl: null
      }
    }
  },
  mounted() {
    this.$refs.focusRef.focus()
  },
  methods: {
    sendMessage() {
      this.$emit('send', {"contact":this.contact, "message": this.messageText, "createdAt": new Date()})
      this.messageText = '';
    },

  }
}
</script>

<style scoped>
textarea {
  outline: none;
  font-size: 16px;
  font-family: "Roboto", sans-serif;
  resize: none;
  width: 100%;
  height: 8vh;
  padding-right: 18px;
  box-sizing: content-box;

}
.send {
  border: none;
  background: lightgray;
  color: rgba(239, 245, 39);
  font-size: 17px;
  border-radius: 50%;
  position: absolute;
  right: 22px;
  padding: 10px 10px 21px 10px;
}

</style>
