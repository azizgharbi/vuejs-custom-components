<template>
  <div>
    <div>
      <button class="btn demo" v-on:click="open">open</button>
      <Modal
        :active="active"
        :closeable="closeable"
        :closeOnOutsideClick="closeOnOutsideClick"
        :state="state"
        :title="'Excepteur in aliquip et mollit officia'"
      >
        <div slot="header"></div>
        <p>
          Excepteur in aliquip et mollit officia aliquip eiusmod
          labore veniam magna. Et deserunt qui ad mollit esse cillum
          veniam non nostrud reprehenderit ipsum ad. Nulla sunt anim
          do ut sunt ullamco sunt mollit quis minim aliquip velit in proident,
          Excepteur in aliquip et mollit officia aliquip eiusmod
          labore veniam magna. Et deserunt qui ad mollit esse cillum
          veniam non nostrud reprehenderit ipsum ad. Nulla sunt anim
          do ut sunt ullamco sunt mollit quis minim aliquip velit in proident.
        </p>
        <div slot="footer"></div>
      </Modal>
    </div>

    <div class="options">
      <h1>Options:</h1>
      <input type="checkbox" id="closeable" v-model="closeable" />
      <label for="closeable">Closeable : {{ closeable }}</label>
      <input type="checkbox" id="closeOnOutsideClick" v-model="closeOnOutsideClick" />
      <label for="closeOnOutsideClick">Close On Outside Click : {{ closeOnOutsideClick }}</label>
      <label for="state">State</label>
      <select v-model="state" id="state">
        <option value="normal">normal</option>
        <option value="success">success</option>
        <option value="info">info</option>
        <option value="alert">alert</option>
        <option value="danger">danger</option>
      </select>
    </div>
  </div>
</template>

<script>
import "./../public/css/app.scss";
//UI components
import Modal from "./Modal";
//Bus event
import { EventBus } from "./eventBus";

export default {
  name: "App",
  components: {
    Modal
  },
  data() {
    return {
      active: false,
      closeable: true,
      closeOnOutsideClick: false,
      state: "normal"
    };
  },
  methods: {
    open: function() {
      this.active = !this.active;
    }
  },
  created() {
    EventBus.$on("close", c => {
      this.active = c;
    });
  }
};
</script>