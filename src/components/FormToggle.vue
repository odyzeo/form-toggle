<template>
    <label
        :class="{
            'is-disabled': disabled,
            'is-toggled': toggled,
        }"
        class="form-toggle"
    >
        <input
            :name="name"
            :checked="value"
            :disabled="disabled"
            type="checkbox"
            class="form-toggle__input"
            @change.stop="toggle"
        >
        <div
            :style="coreStyle"
            class="form-toggle__element"
        >
            <div
                :style="buttonStyle"
                class="form-toggle__button"
            ></div>
        </div>
        <div
            v-if="toggled"
            :style="labelStyle"
            class="form-toggle__label is-left"
        >
            <slot name="checked"></slot>
        </div>
        <div
            v-else
            :style="labelStyle"
            class="form-toggle__label is-right"
        >
            <slot name="unchecked"></slot>
        </div>
    </label>
</template>

<script>
const px = v => `${v}px`;

const translate3d = (x, y, z = '0px') => `translate3d(${x}, ${y}, ${z})`;

export default {
    name: 'FormToggle',
    props: {
        value: {
            type: Boolean,
            default: false,
        },
        name: {
            type: String,
            default: null,
        },
        disabled: {
            type: Boolean,
            default: false,
        },
        speed: {
            type: Number,
            default: 300,
        },
        width: {
            type: Number,
            default: 50,
        },
        height: {
            type: Number,
            default: 22,
        },
        margin: {
            type: Number,
            default: 3,
        },
    },
    data() {
        return {
            toggled: !!this.value,
        };
    },
    computed: {
        coreStyle() {
            return {
                width: px(this.width),
                height: px(this.height),
                borderRadius: px(Math.round(this.height / 2)),
            };
        },
        buttonRadius() {
            return this.height - this.margin * 2;
        },
        distance() {
            return px(this.width - this.height + this.margin);
        },
        buttonStyle() {
            const transition = `transform ${this.speed}ms`;
            const margin = px(this.margin);

            const transform = this.toggled
                ? translate3d(this.distance, margin)
                : translate3d(margin, margin);

            return {
                width: px(this.buttonRadius),
                height: px(this.buttonRadius),
                transition,
                transform,
            };
        },
        labelStyle() {
            return {
                lineHeight: px(this.height),
            };
        },
    },
    methods: {
        toggle(event) {
            this.toggled = !this.toggled;
            this.$emit('input', this.toggled);
            this.$emit('change', {
                value: this.toggled,
                srcEvent: event,
            });
        },
    },
};
</script>

<style lang="less">
@import '../less/form-toggle.less';
</style>
