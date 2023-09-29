<template>
<h1>ini halaman Home</h1>
<p>{{ $data }}</p>
<button @click="onClickBtn">klik</button>

<hr>
<Teleport to="#target-teleport">
    <TeleportPage />
</Teleport>
</template>

<script>

import BasicMixin from '../mixins/basic'
import TombolMixin from '../mixins/button'
import TeleportPage from './TeleportPage.vue'
export default {
    components:{
        TeleportPage
    },
    mixins:[BasicMixin, TombolMixin],
    data(){
        return {
            name:'aslammardin'
        }
    }
}
</script>