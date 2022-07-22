<script setup lang="ts">
import axios from "axios";
import FormData from "form-data";

let file: File;

const onUpdate = async (event: any) => {
  file = await event?.target?.files[0];
};

const onSubmit = () => {
  if (!file) return;

  const formData = new FormData();
  formData.append("file", file);

  const config = { headers: { "Content-Type": "multipart/form-data" } };

  axios
    .post("http://localhost:3001/diaguard", formData, config)
    .then((res) => console.log(res))
    .catch((err) => console.error(err));
};
</script>

<template>
  <h1>Home</h1>
  <form v-on:submit.prevent="onSubmit" enctype="multipart/form-data">
    <input
      type="file"
      name="file"
      accept=".csv"
      @input="(event) => onUpdate(event)"
    />
    <input type="submit" value="submit" />
  </form>
</template>
