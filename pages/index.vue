<template>
  <v-layout>
    <v-flex>
      <h1>LT用ツールを集めたサイト</h1>
      <p>
        LT用のツールを集めたサイトです。どうぞよろしく。
      </p>

      <v-container>
        <v-row dense>
          <v-col cols="12">
            <v-card class="mx-auto">
              <v-card-text>
                <p class="display-1 text--primary">
                  発表順を決める
                </p>
                <div class="text--primary">
                  まずは発表順を決めましょう。
                </div>
              </v-card-text>
              <v-card-actions>
                <v-btn class="ma-4" dark color="indigo" to="/shuffle" nuxt>
                  こちらから
                </v-btn>
              </v-card-actions>
            </v-card>

            <v-card class="mx-auto">
              <v-card-text>
                <p class="display-1 text--primary">
                  時間を測る
                </p>
                <div class="text--primary">
                  時間の計測をしましょう（この機能は実装中です）
                </div>
              </v-card-text>
              <v-card-actions>
                <v-btn class="ma-4" dark color="indigo" to="/timer" nuxt>
                  こちらから
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-flex>
  </v-layout>
</template>

<script>
export default {}
</script>
