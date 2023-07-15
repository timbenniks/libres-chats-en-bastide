<script setup lang="ts">
const prismic = usePrismic();

const { data: chats } = useAsyncData("[chats]", () =>
  prismic.client.getAllByType("chat")
);

useHead({
  title: "Chats",
});
</script>

<template>
  <h1>Chats</h1>

  <ul>
    <li v-for="chat in chats" :key="chat.uid">
      <nuxt-link :to="`/chats/${chat.uid}`">{{ chat.data.nom }}</nuxt-link>
    </li>
  </ul>
</template>
