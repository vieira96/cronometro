<template>
    <div v-show="this.history.length > 0" class="history-area">
        <h4>Historico de pausas</h4>
        <div class="history-single" v-for="(historySingle, index) in history" :key="index">
            Você pausou em: {{historySingle}}
        </div>
    </div>
</template>

<script>
export default {
    name: 'History',
    data() {
        return {
        
        }
    },
    props: {
        history: {
            type: Array
        }
    } 
}
</script>

<style scoped>

</style>