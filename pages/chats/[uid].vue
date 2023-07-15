<script setup lang="ts">
import { components } from "~/slices";

const prismic = usePrismic();
const route = useRoute();
const { data: page } = useAsyncData("[chat-uid]", () =>
  prismic.client.getByUID("chat", route.params.uid as string)
);

useHead({
  title: page.value?.data.meta_title,
  meta: [
    {
      name: "description",
      content: page.value?.data.meta_description || "",
    },
  ],
});
</script>

<template>
  <h1>{{ page?.data?.nom }}</h1>

  <PrismicImage v-if="page?.data?.image" :field="page?.data?.image" />

  <PrismicRichText
    v-if="page?.data?.caractere"
    :field="page?.data?.caractere"
  />

  <dl>
    <dt>Sexe</dt>
    <dd>{{ page?.data?.sexe }}</dd>

    <dt>Date de Naissance</dt>
    <dd>{{ page?.data?.date_de_naissance }}</dd>

    <dt>identifie_par_puce_electronique</dt>
    <dd>{{ page?.data?.identifie_par_puce_electronique }}</dd>

    <dt>vaccinee</dt>
    <dd>{{ page?.data?.vaccinee }}</dd>

    <dt>deparasitee</dt>
    <dd>{{ page?.data?.deparasitee }}</dd>

    <dt>teste_sida</dt>
    <dd>{{ page?.data?.teste_sida }}</dd>

    <dt>teste_leucose</dt>
    <dd>{{ page?.data?.teste_leucose }}</dd>

    <dt>certificat_de_bonne_sante</dt>
    <dd>{{ page?.data?.certificat_de_bonne_sante }}</dd>

    <dt>prescription_future_sterilisation</dt>
    <dd>{{ page?.data?.prescription_future_sterilisation }}</dd>

    <dt>carnet_de_sante</dt>
    <dd>{{ page?.data?.carnet_de_sante }}</dd>

    <dt>habitue_avec_chien</dt>
    <dd>{{ page?.data?.habitue_avec_chien }}</dd>

    <dt>habitue_avec_chats</dt>
    <dd>{{ page?.data?.habitue_avec_chats }}</dd>

    <dt>ville_famille_daccueil</dt>
    <dd>{{ page?.data?.ville_famille_daccueil }}</dd>

    <dt>reserve</dt>
    <dd>{{ page?.data?.reserve }}</dd>

    <dt>adopte</dt>
    <dd>{{ page?.data?.adopte }}</dd>
  </dl>

  <SliceZone
    wrapper="main"
    :slices="page?.data.slices ?? []"
    :components="components"
  />
</template>
