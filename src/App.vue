<template>
  <div class="container">
    <div class="side-nav">
    <div class="profile">
      <img class="profile" src="https://i.ytimg.com/vi/1Ne1hqOXKKI/maxresdefault.jpg" alt="avatar" style="width: 50px; height: 50px;  border-radius: 50%;
">
    </div>
    </div>
    <div class="main-view">
      <div class="content">
        <ContactList
            :user="user"
            @newContact="addNewContact"
        />
        <div>
          <p class="selectChat" :class="{hide:isHidden}" >Select a chat to start messaging</p>
          <ChatRoom
              :user="user"

          >
          </ChatRoom>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
import ContactList from "@/components/ContactList";
import ChatRoom from "@/components/ChatRoom";


export default {
  name: 'App',
  components: {ContactList,ChatRoom},
  data() {
    return {
    user: {
      id: 1 , name: 'li', contactList: [{id: 2, name: 'Ed'},{id: 3, name: 'Boris'},{id: 4, name: 'Emma'}]
    },
      isHidden: false
    }
  },
  methods: {
    addNewContact(contact) {
      this.user.contactList.push(contact)
    },
  },
  mounted() {
    this.emitter.on("hideSelect", (event) => {
      this.isHidden = event.isHidden
    })
  }
}
</script>

<style >
body {

  height: 100%;
  background: lightgray;
}

.container {
  display: grid;
  grid-template-columns: 80px auto;

}
.side-nav {
  background: rgba(239, 245, 39, 0.3);
  font-size: 25px;
  text-align: center;
  height: auto;
  z-index: 2;

}
.side-nav .profile img {
  margin-top: 15px;
  width: auto;
  height: 60px;
  filter: grayscale(1);
  border-radius: 50%;
}

.content {
  display: grid;
  grid-template-columns: 40% auto;
  grid-template-rows: 100%;
}

@media screen and (min-width: 800px) {
  .content {
    grid-template-columns: 30% auto;
  }
}

@media screen and (max-width: 640px) {
  .content {
    grid-template-columns: auto;
  }
}
.hide {
  visibility: hidden;
}
.selectChat {
  text-align: center;
  font-weight: bold;
  font-size: 18px;
  color: gray;
  font-family: fantasy;
  text-shadow: 1px 5px 3px rgba(239, 245, 39, 0.5);
}
</style>
