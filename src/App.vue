<script setup lang="ts">
const { activeError } = storeToRefs(useErrorStore());

onErrorCaptured((error) => {
  useErrorStore().setError({ error });
});
</script>

<template>
  <AuthLayout>
    <AppErrorPage v-if="activeError" />

    <RouterView v-slot="{ Component, route }">
      <Suspense v-if="Component" timeout="0">
        <Component :is="Component" :key="route.name" />
        <template #fallback>
          <span>Loading ...</span>
        </template>
      </Suspense>
    </RouterView>
  </AuthLayout>
</template>
