<template>
  <div id="avatar">
    <file-input
      name="profile-picture"
      label="Upload Picture"
      class-name="image-uploader"
      @input="change"
    >
      <div class="avatar">
        <img fit="cover" :src="value" v-if="value" class="avatar">
        <div v-else class="avatar">
          <p>
            {{ placeholder }}
          </p>
          <slot>
              <div class="instructions">
                    <small>Maximum 5MB in size.</small>
                    <small>JPG, PNG, or GIF formats.</small>
                    <small>Recommended size: 300 x 200 pixel</small>
              </div>
          </slot>
        </div>
      </div>
    </file-input>

    <div v-show="isUploaded"></div>
  </div>
</template>

<script>
import FileInput from "./file-input.vue";

export default {
  components: {
    FileInput
  },
  props: {
    value: {
        type: String,
        required: true
    },
    endpoint: {
        type: String,
        required: true
    },
    fieldName: {
        type: String,
        default: 'logo'
    },
    placeholder: {
        type: String,
        default: "Click to Upload"
    }
  },

  data() {
    return {
      file: null,
      isUploaded: false,
      error: ""
    };
  },

  mounted() {
    this.localAvatarUrl = this.avatarUrl;
  },
  methods: {
    change(file) {
      const reader = new FileReader();
      this.file = file;
      reader.readAsDataURL(file);
      reader.onload = event => {
        this.$emit("input", event.target.result);
      };
      window.files = file;
      this.update();
    },

    update() {
      let fileData = new FormData();
      fileData.append("logo", this.file);

      fetch(this.endpoint, {
        method: "post",
        body: fileData
      })
        .then(response => response.json())
        .then(response => {
            this.$emit("uploaded", response);
        })
        .catch(response => {
            this.$emit("input", "");
            this.$emit("error", response)
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.image-uploader {
  border: 1px dashed #aaa;
  background: white;
  cursor: pointer;
  border-radius: 10px;
  width: 100%;
  display: inline-block;
}
.avatar {
  width: 210px;
  height: 150px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  object-fit: cover;
}
</style>
