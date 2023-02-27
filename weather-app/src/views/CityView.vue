<template>
  <div>
    <Suspense>
      <template #default>
        <AsyncCityView />
      </template>
    </Suspense>
  </div>
</template>

<script setup>
import AsyncCityView from '../components/AsyncCityView.vue';

</script>
