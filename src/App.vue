<template>
    <div
        id="app"
        class="app">
        <div class="container">
            <h1 class="text-center">Form toggle</h1>

            <h3>Checked: {{ checked }}</h3>
            <form-toggle
                v-model="checked"
                :labels="true"
            >
                <template #checked>
                    on
                </template>
                <template #unchecked>
                    off
                </template>
            </form-toggle>

            <h3>Disabled</h3>
            <form-toggle
                disabled
            ></form-toggle>
        </div>
    </div>
</template>

<script>
import FormToggle from './components/FormToggle';

export default {
    name: 'App',
    components: {
        FormToggle,
    },
    data() {
        return {
            checked: true,
        };
    },
};
</script>

<style lang="less">
@import '../src/less/app.less';
</style>
