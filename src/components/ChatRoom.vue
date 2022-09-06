<template>
  <div v-if="chats[contact.id]">
  <div class="message-container">
    <div
        v-for="member in members"
        :key="member.id"
    >
      <div class="friend-chat sticky" id="header">{{ member.name }}</div>
    </div>
  <div v-for="(messages, index) in chats[contact.id]"
       :key="index"
  >
    <div v-for="(message, index) in messages"
       :key="index"
         :class="message.style"
    >
      {{ message.text}}
      <DeleteMessage
      @remove="deleteMessage(index,contact)"
      />
      <p class="date-time" v-if="message.user"
      > {{ message.createdAt.toLocaleDateString() }}
        {{ message.createdAt.toLocaleTimeString()  }}

      </p>
      <span v-else
            :style="dateTime">
        {{ message.createdAt.toLocaleDateString() }}
        {{ message.createdAt.toLocaleTimeString()  }}
        </span>
    </div>

  </div>
  </div>
    <SendMessage
        :contact="contact"
        @send="sendMessage"
    />
  </div>
</template>

<script>
import DeleteMessage from "@/components/DeleteMessage";
import SendMessage from "@/components/SendMessage";
import axios from"axios";
import {Message} from "@/model/message";



export default {
  name: "ChatRoom",
  components: {SendMessage, DeleteMessage},
  props: {
    user:
        {
          id: Number,
          name: String,
        }
  },
  data() {
    return {
      chats: {
        0: {
          "messages": []
        }
      },
      members: [],
      contact:  {
        id: Number,
        name: String,
      },
      dateTime: {
        color: 'black',
        fontSize: '10px'
      }
    }
  },
  methods: {
    sendMessage(event) {
      this.chats[event.contact.id].messages.push(new Message(event.message, event.createdAt, "admin"))

    axios.get("https://api.chucknorris.io/jokes/random").then(
        response => this.chats[event.contact.id].messages.push(new Message(response.data.value, event.createdAt, "friend"))
    )},

    deleteMessage(index,contact) {
      this.chats[contact.id].messages.splice(index, 1)
    }


  },
  mounted() {
    this.emitter.on('creatingSingleRoom', (event) => {
        this.members.push(event.contact)
        this.contact = event.contact
        if (!(event.contact.id in this.chats)) {
          this.chats[event.contact.id] = {"messages": []}
        }
    })
  },
}
</script>

<style scoped>
.admin {
  float: right;
  text-align: right;
  min-height: 25px;
  width: 50%;
  margin: 50px 10px;
  background: lightgray;
  border: 1px solid white;
  border-radius: 25px;
  padding: 10px;
  box-shadow: 0 1px 1px 1px;
}

.friend {
  min-height: 25px;
  width: 50%;
  float: left;
  margin: 21px 10px;
  text-align: left;
  border: 1px solid white;
  border-radius: 25px;
  padding: 10px;
  box-shadow: 0 1px 1px 1px;
}

.message-container {
  padding: 0 18px 500px 0;
  overflow-y: scroll;
  width: 100%;
  box-sizing: content-box;
  background: gray;
}
/*sticky header*/
.friend-chat {
  height: 20px;
  width: 50%;
  border: 1px solid white;
  background: #cccccc;
}
.sticky {
  position: fixed;
  top: 7px;
  width: 100%;
}
</style>
