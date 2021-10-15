<template>
    <div id="app">
        {{ current }}
        <w-select :array="languages" v-model="current">
            Language

            <template #selected>
                {{ languages[current] }}
            </template>

            <template class="option" v-for="(name, code) in languages" :slot="code"
            :value="code">
                {{ name }}
                <img src='/favicon.ico' alt="#" :key="code">
            </template>
        </w-select>
    </div>
</template>

<script>
import WSelect from './components/WSelect.vue'
export default {
    name: 'App',
    components: {
        WSelect
    },
    data() {
        return {
            current: 'en',
            languages: {
                en: 'English',
                ru: 'Russian',
                jp: 'Japanese'
            },
        }
    }
}
</script>

<style lang="less">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
