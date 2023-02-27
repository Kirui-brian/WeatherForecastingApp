<template>
<<<<<<< HEAD
  <div>
    <Suspense>
      <template #default>
        <AsyncCityView />
      </template>
    </Suspense>
  </div>
=======
    <div>
        <Suspense>
            <AsyncCityView />
            <template #fallback>
                <p>Loading...</p>
            </template>
        </Suspense>
    </div>
>>>>>>> origin/master
</template>

<script setup>
import AsyncCityView from '../components/AsyncCityView.vue';

</script>
