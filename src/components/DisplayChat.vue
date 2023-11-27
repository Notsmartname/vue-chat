<template>
  <div class="diplay__chat" @click="photoOnBtn">
    <div class="display__chat-header">
        <div class="chat__header-avatar" >
            <img :src="user.avatar" alt="">
        </div>
        <div class="chat__header-info">
            <h4 class="chat__header-info-name">{{ user.name }}</h4>
            <span v-if="user.online">Онлайн</span>
            <span v-else>Оффлайн</span>
        </div>
    </div>
    <div class="display__chat-main">
        <MyMessage 
            v-for="(message, index) in messages"
            :key="index"
            :message="message"
            :user="user"
        />
    </div>
    <div class="display__chat-footer" @click.stop>
        <input type="text" placeholder="Написать сообщение..." v-model="TextController" v-on:focus="messageOnBtn">
        <button v-if="messageBtn" class="chat__footer-btn" @click="addMessage">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="18" viewBox="0 0 20 18" fill="none">
                <path d="M1.4 17.4L18.85 9.91999C19.66 9.56999 19.66 8.42999 18.85 8.07999L1.4 0.599986C0.74 0.309986 0.00999999 0.799987 0.00999999 1.50999L0 6.11999C0 6.61999 0.37 7.04999 0.87 7.10999L15 8.99999L0.87 10.88C0.37 10.95 0 11.38 0 11.88L0.00999999 16.49C0.00999999 17.2 0.74 17.69 1.4 17.4Z" fill="white"/>
            </svg>
        </button>
        <button v-else class="chat__footer-btn" @click="openModal">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none">
                <path d="M12 15C13.6569 15 15 13.6569 15 12C15 10.3431 13.6569 9 12 9C10.3431 9 9 10.3431 9 12C9 13.6569 10.3431 15 12 15Z" fill="white"/>
                <path d="M20 4H16.83L15.59 2.65C15.22 2.24 14.68 2 14.12 2H9.88C9.32 2 8.78 2.24 8.4 2.65L7.17 4H4C2.9 4 2 4.9 2 6V18C2 19.1 2.9 20 4 20H20C21.1 20 22 19.1 22 18V6C22 4.9 21.1 4 20 4ZM12 17C9.24 17 7 14.76 7 12C7 9.24 9.24 7 12 7C14.76 7 17 9.24 17 12C17 14.76 14.76 17 12 17Z" fill="white"/>
            </svg>
        </button>
    </div>
  </div>
</template>

<script>
import MyMessage from "./MyMessage.vue";


export default {
    components: {
        MyMessage,
    },
    name: "display-chat",
    props: {
        user: Object,
        currentId: Number,
        messages: Array,
    },

    data() {
        return {
            TextController: "",
            id: this.currentId,
            messageBtn: false,
        }
    },

    methods: {
        addMessage() {
            const now = new Date();
            const message = {
                id: this.id++,
                text: this.TextController,
                time: now.getHours() + ':' + now.getMinutes(),
                user: this.user.id
            };
            this.$emit('addMessage', message);
            this.TextController = '';
        },

        messageOnBtn() {
            this.messageBtn = true;
        },

        photoOnBtn() {
            this.messageBtn = false;
        },

        openModal() {
            const status = {
                statusModal: true,
                statusUser: this.user.id,
            }
            this.$emit('openModal', status);
        }
    },
}
</script>

<style scoped>
    .diplay__chat {
        width: 400px;
        height: 800px;
        background-image: url(../assets/images/main_bg.png);
        user-select: none;

    }
    
    .display__chat-main {
        padding: 10px;
        overflow-y: scroll;
    }

    ::-webkit-scrollbar {
        width: 2px;
        border-radius: 3px;
    }


    ::-webkit-scrollbar-thumb {
        width: 3px;
        border-radius: 3px;
        background: #00AAA1;
    }

    ::-webkit-scrollbar-thumb:hover {
        background: #3b5352; 
    }
    .display__chat-header {
        padding: 31px 20px;
        background: #323232;
        border-radius: 30px 30px 0 0;
        display: flex;
        align-items: center;
        gap: 10px;
    }

    .chat__header-info span {
        color: #FFF;
        font-family: "Roboto";
        font-size: 14px;
        font-style: normal;
        font-weight: 300;
        line-height: 18px; /* 128.571% */
        filter: brightness(85%);
    }

    .chat__header-info-name {
        color: #FFF;
        font-family: "Roboto";
        font-size: 18px;
        font-style: normal;
        font-weight: 500;
        line-height: 14px; /* 77.778% */
    }

    .display__chat-main {
        height: 632px;
    }

    .display__chat-footer {
        height: 56px;
        width: 100%;
        background: #323232;
        border-radius: 0 0 30px 30px;
        padding: 16px 20px 16px 20px;
        display: flex;
        align-items: center;
        justify-content: space-between;

    }

    .display__chat-footer input {
        background: none;
        border: none;
        color: #FFF;
        font-family: "Roboto";
        font-size: 14px;
        font-style: normal;
        font-weight: 400;
        line-height: normal;
        height: 16px;
        width: 250px;
        outline:none;
    }
    
    .chat__footer-btn {
        border: none;
        background: none;
    }
</style>