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
    <ChatRoom
    :user="user"
    >
    </ChatRoom>
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
    }
  },
  methods: {
    addNewContact(contact) {
      this.user.contactList.push(contact)

    }
  }
}
</script>

<style >
body {
  height: 100%;
}

.container {
  display: grid;
  grid-template-columns: 80px auto;
  /*grid-template-rows: 100vh;*/
  background: antiquewhite;
}
.side-nav {
  background: darkseagreen;
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

</style>
