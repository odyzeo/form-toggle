<template>
    <div
        id="app"
        class="app">
        <div class="container">
            <h1 class="text-center">Form toggle</h1>

            <form
                ref="form"
                @submit.prevent="onFormSubmit"
            >
                <form-toggle
                    v-model="isSubscribedChecked"
                    name="isSubscribed"
                ></form-toggle>
                <br>
                <form-toggle
                    v-model="isDevilChecked"
                    name="isDevil"
                    true-value="yes"
                    false-value="no"
                ></form-toggle>
                <button>submit</button>
                <pre v-text="formData"></pre>
            </form>

            <h3>Checked: {{ checked }}</h3>
            <form-toggle v-model="checked">
                <template #checked>
                    on
                </template>
                <template #unchecked>
                    off
                </template>
            </form-toggle>

            <h3>Custom dimensions</h3>
            <form-toggle
                v-model="checked"
                :width="100"
                :height="40"
                :margin="7"
            ></form-toggle>

            <h3>Disabled</h3>
            <form-toggle
                disabled
            ></form-toggle>

            <h3>Custom context</h3>
            <form-toggle
                v-model="checked"
            >
                <template #left>
                    <span v-if="checked">
                        on
                    </span>
                    <span v-else>
                        off
                    </span>
                </template>
            </form-toggle>

            <h3>Custom icons</h3>
            <form-toggle
                v-model="checked"
            >
                <template #left>
                    <span v-if="!checked">
                        off
                    </span>
                </template>
                <template #right>
                    <span v-if="checked">
                        on
                    </span>
                </template>
            </form-toggle>
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
            formData: null,
            isSubscribedChecked: true,
            isDevilChecked: true,
        };
    },
    methods: {
        onFormSubmit() {
            this.formData = '';
            const formData = new FormData(this.$refs.form);
            Array.from(formData).forEach(function (pair) {
                this.formData += `${pair[0]}: ${pair[1]}\n`;
            }, this);
        },
    },
};
</script>

<style lang="less">
@import '../src/less/app.less';
</style>
