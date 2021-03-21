<template>
  <v-app>
    <v-main>
      <v-card width="400px" class="mx-auto mt-5">
        <v-card-title>
        <h2 class="display-1">アカウント登録</h2>
        </v-card-title>
        <v-form>
          <div
            class="flex items-center justify-center flex-col w-full h-full mt-8"
          >
            <div
              class="flex items-center justify-center w-32 h-32 bg-gray-200 rounded-full border border-gray-400 "
            >
              <template v-if="form.imageUrl.val">
                <v-img
                  :src="form.imageUrl.val"
                  class=""
                  @click="selectImage"
                />
              </template>
              <template v-else>
                <v-icon
                  class="text-center text-7xl"
                  @click="selectImage"
                >
                  mdi-account
                </v-icon>
              </template>
              <input
                ref="image"
                type="file"
                style="display: none"
                accept="image/*"
                @change="onSelectFile"
              />
            </div>
          </div>
          <label
            class="block mt-8 mb-2 ml-2 uppercase tracking-wide text-darkGray text-s"
          >
            名前
          </label>
          <div class="h-20 mb-6">
            <input
              type="text"
              class="block w-full py-3 px-4 appearance-none bg-gray-200 text-darkGray border rounded leading-tight focus:outline-none focus:bg-white"
            />
          </div>

          <div class="flex">
            <v-card-actions>

            <v-btn
              class="w-full p-3 gradation rounded-full text-white
        "
            >
              登録
            </v-btn>
            </v-card-actions>
          </div>
        </v-form>
      </v-card>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      form: {
        imageUrl: {
          val: null
        }
      }
    };
  },
  methods: {
    selectImage() {
      this.$refs.image.click();
    },
    onSelectFile(e) {
      const files = e.target.files;
      if (files.length === 0) return;

      const reader = new FileReader();
      reader.readAsDataURL(files[0]);

      reader.addEventListener("load", () => {
        this.upload({
          localImageFile: files[0]
        });
      });
    },
    async upload({ localImageFile }) {
      const user = await this.$auth();

      // 未ログインの場合
      if (!user) this.$router.push("/login");

      // // ストレージオブジェクト作成
      const storageRef = this.$fireStorage.ref();

      // ファイルのパスを設定
      const imageRef = storageRef.child(
        `images/${user.uid}/${localImageFile.name}`
      );

      // ファイルを適用してファイルアップロード開始
      const snapShot = await imageRef.put(localImageFile);
      this.form.imageUrl.val = await snapShot.ref.getDownloadURL();
    }
  }
};
</script>
