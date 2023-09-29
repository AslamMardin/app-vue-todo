<template>
    <div>component 3 {{ author }}</div>
    <button @click="$emit('emitAuthor', 'kirim')">kirim</button>
</template>

<script>
    export default {
        inject:["author", "emitAuthor"]
    }
</script>