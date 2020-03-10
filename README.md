# image-uploader

### Install
`npm install -s vue-profile-uploader`

### Usage
```
<template>
  <div class="">
    <vue-profile-uploader v-model="logo" endpoint="{your-endpoint}"/>
  </div>
</template>

<script>
import VueProfileUpload from "vue-profile-uploader";

export default {
  props: {
    msg: String
  },
  components: {
    VueProfileUploader
  },
  data() {
    return {
      logo: ""
    };
  }
};
</script>
```

## Props

| name        |  type    | Description         | Required  |                                 Default |
|-------------|----------|---------------------|-----------|-----------------------------------------|
| value       | string   | image path          |true       |""                                       |    
| endpoint    | string   | url to the upload   |true       | ""                                      |  
| placeholder | string   | text to show in the box when there's no image |false |  "Click to upload" |
| fieldName   | string   | field name of the file expected in the backend | false| "logo"            |

## Events

| name   | payload       |
|--------|---------------|
| input  |  value        |
| upload |  response     |
| error  |  error object |
