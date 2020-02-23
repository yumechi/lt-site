<template>
  <v-layout>
    <v-flex class="text-center">
      <blockquote class="blockquote">
        順番決めちゃうよ！
      </blockquote>
      <v-textarea
        v-model="users"
        placeholder="名前を改行区切りで入れてね"
      ></v-textarea>
      <v-btn
        class="ma-2"
        dark
        color="indigo"
        :loading="loading"
        :disabled="loading"
        loading-text="loading..."
        @click="loader = 'loading'"
        >シャッフル!!</v-btn
      >
      <blockquote class="blockquote">
        <v-data-table
          :headers="headers"
          :items="results"
          :options.sync="options"
          :server-items-length="total"
          :footer-props="{
            'items-per-page-options': [10, 20, 50, 100, 200, 300, 400, 500],
            showFirstLastPage: true
          }"
          :loading="loading"
          loading-text="loading..."
          no-data-text="まだ順番が決まっていません"
        >
        </v-data-table>
      </blockquote>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data() {
    return {
      users: '',
      headers: [
        { text: '順番', align: 'center', sortable: true, value: 'order_id' },
        { text: 'お名前', align: 'center', sortable: false, value: 'username' }
      ],
      options: {
        page: 1,
        itemsPerPage: 20,
        sortBy: ['order_id'],
        sortDesc: [false],
        multiSort: false,
        mustSort: true
      },
      results: [],
      total: 0,
      loader: null,
      loading: false
    }
  },
  watch: {
    loader() {
      const l = this.loader
      this[l] = !this[l]

      setTimeout(() => (this[l] = false), 500)
      this.shuffleUser()

      this.loader = null
    }
  },
  methods: {
    sliceUserData() {
      return this.users.split('\n').filter((c) => c.trim().length > 0)
    },
    shuffleArray(arr) {
      if (arr.length === 0) {
        return []
      }
      // refer: https://qiita.com/komaji504/items/62a0f8ea43053e90555a
      for (let i = arr.length - 1; i > 0; i--) {
        const r = Math.floor(Math.random() * (i + 1))
        const tmp = arr[i]
        arr[i] = arr[r]
        arr[r] = tmp
      }
      return arr
    },
    setResult(data) {
      this.results = data
      this.total = (data ?? []).length
    },
    shuffleUser() {
      const data = this.shuffleArray(this.shuffleArray(this.sliceUserData()))
      if (data.length === 0) {
        this.setResult([])
        return
      }
      const ret = data.map((value, index) => {
        return {
          order_id: index + 1,
          username: value
        }
      })

      this.setResult(ret)
    }
  }
}
</script>
