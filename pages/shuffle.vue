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
      <v-btn class="ma-2" outlined dark color="indigo" @click="shuffleUser"
        >シャッフル!!</v-btn
      >
      <v-data-table
        :headers="headers"
        :items="results"
        :options.sync="options"
        loading-text="ぐるぐる"
        no-data-text="まだ順番が決まっていません"
      ></v-data-table>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data() {
    return {
      users: '',
      results: [],
      headers: [
        { text: '順番', align: 'center', sortable: true, value: 'order_id' },
        { text: 'お名前', align: 'center', sortable: false, value: 'username' }
      ],
      options: {
        page: 1,
        itemsPerPage: 15,
        sortBy: ['order_id'],
        sortDesc: [false],
        multiSort: false
      }
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
    shuffleUser() {
      const shuffledUser = this.shuffleArray(this.sliceUserData())
      if (shuffledUser.length === 0) {
        return {}
      }
      const ret = []
      for (let i = 0; i < shuffledUser.length; i++) {
        ret.push({ order_id: i + 1, username: shuffledUser[i] })
      }
      this.results = ret
    }
  }
}
</script>
