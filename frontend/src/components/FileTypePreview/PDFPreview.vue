<template>
  <LoadingIndicator
    v-if="loading"
    class="w-10 h-full z-10 text-neutral-100 mx-auto" />
  <div
    v-else
    class="max-h-[95vh] max-w-[75vw] z-10 bg-[#252728] rounded-lg shadow-xl">
    <iframe class="w-full min-w-[75vw] h-[90vh]" :src="previewURL" />
  </div>
</template>

<script setup>
import { LoadingIndicator } from "frappe-ui";
import { onMounted, ref } from "vue";
import { useObjectUrl } from "@vueuse/core";

const props = defineProps(["previewEntity"]);
const loading = ref(true);
const blob = ref(null);
const previewURL = useObjectUrl(blob);

async function fetchContent() {
  loading.value = true;
  const headers = {
    Accept: "application/json",
    "Content-Type": "application/json; charset=utf-8",
    "X-Frappe-Site-Name": window.location.hostname,
    Range: "bytes=0-10000000",
  };
  const res = await fetch(
    `/api/method/drive.api.files.get_file_content?entity_name=${props.previewEntity.name}`,
    {
      method: "GET",
      headers,
    }
  );
  if (res.ok) {
    loading.value = false;
    blob.value = await res.blob();
  }
}
onMounted(() => {
  fetchContent();
});
</script>
<style scoped></style>