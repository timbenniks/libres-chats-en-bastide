<script setup lang="ts">
import { Content } from "@prismicio/client";

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.MediaItemSlice>([
    "slice",
    "index",
    "slices",
    "context",
  ])
);
</script>

<template>
  <section
    :data-slice-type="slice.slice_type"
    :data-slice-variation="slice.variation"
  >
    <ul>
      <li v-for="item in slice.items" :key="item?.media?.url">
        <template v-if="item?.media?.kind === 'document'">
          <video :src="item?.media?.url" controls />
        </template>
        <template v-else>
          <PrismicImage :field="item?.media" />
        </template>
      </li>
    </ul>
  </section>
</template>
