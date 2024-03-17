<script setup lang="ts">
const name = ref<string | undefined>("App");
const surname = ref<string | undefined>("Test");
const isComing = ref<string>("No");

const testFetch = async () => {
  //Use parameters cause body object and application/json cause 405 error from CORS policy
  const { data } = await useFetch(
    `https://script.google.com/macros/s/AKfycbxE3igSUUqTwq_nJTBkmnO2o6XkRtvL5MawmMQ-jPwpG1jQ2FIwzEi7NG5w6QZtm14BhQ/exec?name=${name.value}&surname=${surname.value}&isComing=${isComing.value}`,
    { method: "POST" }
  );
};

const areAllInputsCompleted = computed(() => !!name.value && !!surname.value);
</script>

<template>
  <div>
    <div class="flex flex-col gap-2">
      <p>
        <span class="text-orange-300">Nome:</span
        ><input type="text" v-model="name" />
      </p>
      <p>
        <span class="text-orange-300">Cognome:</span
        ><input type="text" v-model="surname" />
      </p>
    </div>
    <div>
      <input
        type="radio"
        id="Si"
        name="isComing"
        value="Si"
        checked
        v-model="isComing"
      />
      <label for="Si">Si</label>
      <input
        type="radio"
        id="No"
        name="isComing"
        value="No"
        v-model="isComing"
      />
      <label for="No">No</label>
    </div>
    <button :disabled="!areAllInputsCompleted" @click="testFetch">
      Submit
    </button>
  </div>
</template>

<style scoped>
button:disabled {
  background-color: #ccc; /* Gray background */
  color: #666; /* Darker text */
  cursor: not-allowed; /* Cursor style for disabled elements */
}
</style>
