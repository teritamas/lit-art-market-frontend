<template>
  <nav class="bg-opacity-0 border-gray-200 dark:bg-gray-900">
    <div
      class="flex flex-wrap justify-between items-center mx-auto max-w-screen-xl px-4 md:px-6 py-2.5"
    >
      <img src="@/assets/logo.png" width="60" height="60" alt="" />
      <span>Lit Art Market</span>
      <div v-if="token" class="items-center" @click="getDetail()">
        <router-link
          to="/mypage"
          class="flex text-sm text-white font-medium hover:underline"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            fill="currentColor"
            class="w-6 h-6 mr-2 text-white"
          >
            <path
              fill-rule="evenodd"
              d="M4.5 3.75a3 3 0 00-3 3v10.5a3 3 0 003 3h15a3 3 0 003-3V6.75a3 3 0 00-3-3h-15zm4.125 3a2.25 2.25 0 100 4.5 2.25 2.25 0 000-4.5zm-3.873 8.703a4.126 4.126 0 017.746 0 .75.75 0 01-.351.92 7.47 7.47 0 01-3.522.877 7.47 7.47 0 01-3.522-.877.75.75 0 01-.351-.92zM15 8.25a.75.75 0 000 1.5h3.75a.75.75 0 000-1.5H15zM14.25 12a.75.75 0 01.75-.75h3.75a.75.75 0 010 1.5H15a.75.75 0 01-.75-.75zm.75 2.25a.75.75 0 000 1.5h3.75a.75.75 0 000-1.5H15z"
              clip-rule="evenodd"
            />
          </svg>
          <span class="text-small">{{ detail.userName }} さん</span>
        </router-link>
      </div>
      <div v-if="!token" class="items-center">
        <router-link
          to="/mypage"
          class="flex text-sm text-white font-medium hover:underline"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            fill="currentColor"
            class="mr-1 w-6 h-6 text-white-600"
          >
            <path
              fill-rule="evenodd"
              d="M7.5 3.75A1.5 1.5 0 006 5.25v13.5a1.5 1.5 0 001.5 1.5h6a1.5 1.5 0 001.5-1.5V15a.75.75 0 011.5 0v3.75a3 3 0 01-3 3h-6a3 3 0 01-3-3V5.25a3 3 0 013-3h6a3 3 0 013 3V9A.75.75 0 0115 9V5.25a1.5 1.5 0 00-1.5-1.5h-6zm5.03 4.72a.75.75 0 010 1.06l-1.72 1.72h10.94a.75.75 0 010 1.5H10.81l1.72 1.72a.75.75 0 11-1.06 1.06l-3-3a.75.75 0 010-1.06l3-3a.75.75 0 011.06 0z"
              clip-rule="evenodd"
            />
          </svg>
          <span class="text-small text-white">ログイン</span>
        </router-link>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "app-headrer",
  components: {},
  data() {
    return {};
  },
  computed: {
    isAuthorized() {
      const token = this.token;
      if (token === "") {
        return false;
      } else {
        return true;
      }
    },
    userId() {
      return this.$store.getters["userStore/userId"];
    },
    detail() {
      return this.$store.getters["userStore/detail"];
    },
    token() {
      return this.$store.getters["userStore/token"];
    },
  },
  created() {
    if (this.isAuthorized) {
      // this.getDetail().then(() => {});
    }
  },
  methods: {
    getDetail() {
      const token = this.token;
      return this.$store.dispatch("userStore/getDetail", token);
    },
  },
};
</script>

<style scoped>
nav {
  color: white;
  z-index: 10000;
  position: sticky;
}

span {
  letter-spacing: 0.05em;
  font-weight: bold;
  font-size: 1rem;
}

span.text-small {
  letter-spacing: 0.01em;
  font-size: 0.7rem;
}
</style>
