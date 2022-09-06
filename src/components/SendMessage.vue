<template>
  <div @click.prevent>
    <textarea
    class="textarea-container"
    placeholder="Type your message"
    v-model="messageText"
    @keyup.enter="sendMessage"
    ></textarea>
    <button class="send"  @click.stop="sendMessage">Send</button>
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
      messageText: ''
    }
  },
  methods: {
    sendMessage() {
      this.$emit('send', {"contact":this.contact, "message": this.messageText, "createdAt": new Date()})
      this.messageText = '';
    }
  }
}
</script>

<style scoped>
textarea {
  outline: none;
  font-size: 16px;
  font-family: "Roboto", sans-serif;
  resize: none;
  overflow-y: scroll;
  width: 100%;
  height: 8vh;
  padding-right: 18px;
  box-sizing: content-box;

}
.send {
  border: none;
  background: darkseagreen;
  color: white;
  font-size: 17px;
  border-radius: 50%;
  position: absolute;
  right: 22px;
  padding: 10px 10px 21px 10px;
}

</style>
