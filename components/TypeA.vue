<template>
<div>this is test A</div>
</template>

<script setup>
await setTimeout(() => {
console.log("Delayed for 3 second.");
}, 3000);
</script>