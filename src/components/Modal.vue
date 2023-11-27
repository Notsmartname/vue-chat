<template>
    <div class="modal" @click="closeModal">
      <div class="modal__block" @click.stop="">
        <h2 class="modal__title">
            Отправить картинку
        </h2>
        <div class="modal__inputs">
          <label>
            <span> URL </span>
            <input
              type="text"
              placeholder="URL"
              v-model="urlController"
            />
          </label>
          <label>
            <span> Комментарий </span>
            <textarea placeholder="Заметка" v-model="textController"></textarea>
          </label>
        </div>
  
        <div class="modal__btns">
          <button class="modal__btn cancel" @click="closeModal">Отмена</button>
          <!--  -->
          <button class="modal__btn add" @click="addMessage">
            Добавить
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {

    data() {
      return {
        urlController: "",
        textController: "",
        id: this.currentId,
      };
    },
    methods: {
      closeModal() {
        this.$emit("closeModal", false);
        this.urlController = "";
        this.textController = "";
      },

      addMessage() {
            const now = new Date();
            const message = {
                id: this.id++,
                text: this.textController,
                url: this.urlController,
                time: now.getHours() + ':' + now.getMinutes(),
                user: this.userForModal
            };
            this.$emit('addMessage', message);
            this.textController = '';
            this.urlController = "";
            this.$emit("closeModal", false);
        },
      
    },
    props: {
      currentId: Number,
      userForModal: Number,
    },
  };
  </script>
  
  <style>
  .modal {
    position: fixed;
    background: rgba(0, 0, 0, 0.35);
    width: 100%;
    height: 100vh;
    top: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .modal__block {
    padding: 24px;
    border-radius: 28px;
    background: var(
      --m-3-read-only-light-surface-3,
      linear-gradient(
        0deg,
        rgba(103, 80, 164, 0.11) 0%,
        rgba(103, 80, 164, 0.11) 100%
      ),
      #fffbfe
    );
    width: 100%;
    max-width: 312px;
  }
  
  .modal__title {
    color: #1C1B1F;
    font-family: "Roboto";
    font-size: 24px;
    font-style: normal;
    font-weight: 400;
    line-height: 32px; /* 133.333% */
  }
  
  .modal__inputs {
    display: flex;
    flex-direction: column;
    gap: 16px;
    margin-top: 16px;
  }
  
  .modal__inputs label {
    position: relative;
  }
  
  .modal__inputs span {
    color: #000;
    font-family: "Roboto";
    font-size: 12px;
    font-style: normal;
    font-weight: 400;
    line-height: 16px; /* 133.333% */
    letter-spacing: 0.4px;
  }
  
  .modal__inputs input,
  .modal__inputs textarea {
    border-radius: 4px 4px 0px 0px;
    background: #e7e0ec;
    width: 100%;
    border: none;
    outline: none;
    resize: none;
    padding: 23px 16px 9px 16px;
    border-bottom: 1px solid #1c1b1f;
    font-size: 16px;
    font-style: normal;
    font-weight: 400;
    line-height: 24px;
    letter-spacing: 0.5px;
    color: #49454F;
    font-family: "Roboto";
  }
  
  .modal__inputs input::placeholder,
  .modal__inputs textarea::placeholder {
    color: var(--m-3-sys-light-on-surface-variant, #49454f);
  }
  
  .modal__btns {
    display: flex;
    justify-content: flex-end;
    margin-top: 24px;
    gap: 8px;
  }
  
  .modal__btn {
    border: none;
    outline: none;
    background: transparent;
    padding: 0 10px;
    text-align: center;
    font-size: 14px;
    font-style: normal;
    font-weight: 500;
    line-height: 20px;
    letter-spacing: 0.1px;
    text-transform: uppercase;
    transition: 0.3s;
  }
  
  .modal__btn:active {
    transform: scale(0.95);
  }
  
  .add {
    color: var(--m-3-sys-light-primary, #6750a4);
  }
  
  .cancel {
    color: #cf1b1b;
  }
  </style>