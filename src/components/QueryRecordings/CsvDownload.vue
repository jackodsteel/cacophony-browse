<template>
  <b-button type="submit" variant="secondary" class="btn-sm" @click="click">
    <font-awesome-icon icon="download" class="fa-1x" />
    Export
  </b-button>
</template>

<script>
import config from "../../config";
import userapi from "../../api/User.api.js";
import querystring from "querystring";

export default {
  name: "CsvDownload",
  props: {
    params: {
      type: Object,
      required: true
    }
  },
  methods: {
    async click() {
      const token = await userapi.token();
      const params = Object.assign(this.params, {
        jwt: token
      });
      params.offset = 0;
      params.limit = 100000;
      const url =
        `${config.api}/api/v1/recordings/report?` +
        querystring.stringify(params);
      window.open(url, "_self");
    }
  }
};
</script>
