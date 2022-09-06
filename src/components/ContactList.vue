<template>
  <div >
    <div class="message-list">
    <div class="list-top">
     <input type="text" placeholder="search" v-model="search" class="input">
      <button class="new-friend-btn" @click.stop="showModal">+</button>
    </div>
    <p
        v-for="contact in renderingContactList"
        :key="contact.id"
        @click="selectChat(contact)"
        class="name"
    >{{ contact.name }}
      <img class="profile" src="https://i.ytimg.com/vi/1Ne1hqOXKKI/maxresdefault.jpg" alt="avatar" style="width: 50px; height: 50px;  border-radius: 50%;
">
    </p>
     <NewContact
         v-bind="$attrs"
         v-model:show="modalVisible"
     />

    </div>
  </div>
</template>

<script>
import NewContact from "@/components/NewContact";

export default {
  name: "ContactList",
  components: {NewContact},
  data(){
    return {
      search: '',
      modalVisible: false,
      contact:  {
        id: 0,
        name: "",
      },
    }
  },
  props: {
    user:
        {
          id: 0,
          name: "",
          contactList: []
        },
  },
  methods: {
    selectChat(contact) {
      this.emitter.emit('creatingSingleRoom', { "contact": contact})
    },
    showModal() {
      this.modalVisible = true;
    }
  },
  computed: {
    renderingContactList() {
      if (this.search == null || this.search === "") {
        return this.user.contactList
      }

      let keyword  = this.search.toLowerCase()

      return this.user.contactList.filter((contact) => {
        return contact.name.toLowerCase().includes(keyword)
      })
    }
  }
}
</script>

<style scoped>
.side-nav {
  font-size: 25px;
  text-align: center;
  height: 100%;
  z-index: 2;
}
.message-list {
  height: 100%;
}

@media screen and (max-width: 640px) {
  .message-list {
    position: absolute;
    display: none;
    z-index: 1;
  }
}

.message-list .list-top {
  display: grid;
  grid-template-columns: 60% 22% 18%;
  padding: 5px;
}

/*.message-list .list-top .close-list {*/
/*  !*display: none;*!*/
/*}*/

@media screen and (max-width: 640px) {
  .message-list .list-top {
    grid-template-columns: 60% 20% 10% 10%;
  }
  /*.message-list .list-top .close-list {*/
  /*  display: block;*/
  /*  position: absolute;*/
  /*  background: transparent;*/
  /*  border: none;*/
  /*  content: "\2039";*/
  /*  font-size: 20px;*/
  /*  color: black;*/
  /*  top: 15px;*/
  /*  right: 15px;*/
  /*}*/
}

.message-list .input {
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
.new-friend-btn {
  font-size: 16px;
  border-radius: 50px 50px 50px 50px;
  outline: none;
  border: none;
  background: whitesmoke;
  box-shadow: 1px 1px 3px 1px;
  color: black;
  margin: 7px;
  width: 59px;
  padding: 7px;
}
.message-list .name {
  display: grid;
  grid-template-columns: 25% auto;
  height: 50px;
  padding: 10px;
  box-shadow: 1px 1px 1px 1px;
  border-radius: 0 30px 30px 0;
  color: black;
  position: relative;
}

@media screen and (max-width: 640px) {
  .message-list .name {
    display: grid;
    grid-template-columns: 60px auto;
  }
}

.name{}
.message-list .name {
  margin: 5px 10px;
  font-size: 16px;
  font-weight: 100;
}

.message-list img {
  height: 100%;
  width: auto;
  max-height: 50px;
  border-radius: 50%;
  filter: grayscale(1);
  z-index: 2;
}

</style>
