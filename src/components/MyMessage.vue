<template>
  <div class="my__message"  v-if="message.user == user.id">
    <p class="my__message-text">
        <img v-show="message.url" :src="message.url" alt="">
        {{ message.text }}
    </p>
    <span class="time">
        {{ message.time }}
    </span>
  </div>
  <div class="else__message"  v-else>
    <p class="else__message-text">
        <img v-show="message.url" :src="message.url" alt="">
        {{ message.text }}
        
    </p>
    <span class="time">
        {{ message.time }}
    </span>
  </div>
</template>

<script>
export default {
    props: {
        message: Object,
        user: Object,
    }
}
</script>

<style>
    .my__message {
        display: flex;
        align-items: center;
    }

    .time {
        padding: 5px 5px 5px 10px;
        margin-bottom: 10px;
        color: #323232;
        font-family: "Roboto";
        font-size: 14px;
        font-style: normal;
        font-weight: 400;
        line-height: normal;
    }
    
    .my__message-text {
        padding: 5px 5px 5px 10px;
        max-width: 302px;
        border-radius: 15px 15px 15px 0px;
        background: #C4BFFF;
        margin-bottom: 10px;
        color: #000;
        font-family: "Roboto";
        font-size: 16px;
        font-style: normal;
        font-weight: 400;
        line-height: normal;
        
    }

    img {
        border-radius: 13px;
        max-width: 280px;
        
    }

    .else__message {
        display: flex;
        flex-direction: row-reverse;
        align-items: center;
    }

    .else__message-text {
        padding: 5px 5px 5px 10px;
        max-width: 302px;
        border-radius: 15px 15px 0px 15px;
        margin-bottom: 10px;
        background: #D0DCFF;
    }
</style>