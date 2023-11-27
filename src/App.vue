<template>
  <div class="wrapper">
    <DisplayChat 
      v-for="user in users" 
      :key="user.id" 
      :user="user"
      @addMessage="addMessage"
      :messages="messages"
      @openModal="openModal"
    />
    <Modal
      v-show="modalOpen"
      @closeModal="closeModal"
      :currentId="currentId"
      @addMessage="addMessage"
      :userForModal="userForModal"
    />
  </div>
</template>

<script>
import "./assets/style.css";
import DisplayChat from "./components/DisplayChat.vue";
import Modal from "./components/Modal.vue";
import photo1 from "@/assets/images/photo1.png"
import photo2 from "@/assets/images/photo2.png"

export default {
  name: 'App',
  components: {
    DisplayChat,
    Modal,
  },

  data() {
    return {
      switchBtn: false,
      users: [
        {
          id: 1,
          name: 'Александр',
          avatar: photo1,
          online: true,
        },
        {
          id: 2,
          name: 'Евгений',
          avatar: photo2,
          online: true,
        },
      ],
      messages: [],
      currentId: 1,
      photos: [],
      modalOpen: false,
      userForModal: 0,

    }
  },
  methods: {
    addMessage(message) {
      this.messages.push(message);
    },
    getMessage() {
      let localMessages = localStorage.messages;
      if (localMessages) {
        this.messages = JSON.parse(localMessages);
        this.currentId = this.messages.length;
        this.currentId++;
      }
    },

    openModal(status) {
      this.modalOpen = status.statusModal;
      this.userForModal = status.statusUser;
    },

    closeModal(status) {
      this.modalOpen = status;
    },
  }
}
</script>

<style scoped>
  .wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 20px;
    padding: 140px;
  }
</style>
