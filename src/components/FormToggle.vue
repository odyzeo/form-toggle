<template>
    <label
        :class="{
            'is-disabled': disabled,
            'is-toggled': toggled,
        }"
        class="form-toggle"
    >
        <slot name="left"></slot>
        <input
            :value="trueValue"
            :name="showFalseInput ? null : name"
            :checked="value"
            :disabled="disabled"
            type="checkbox"
            class="form-toggle__input"
            @change="onChange"
        >
        <input
            v-if="showFalseInput"
            :name="name"
            :value="falseValue"
            :disabled="disabled"
            type="hidden"
        >
        <span
            :style="coreStyle"
            class="form-toggle__element"
        >
            <span
                :style="buttonStyle"
                class="form-toggle__button"
            ></span>
        </span>
        <slot name="right"></slot>
        <span
            v-if="toggled"
            :style="labelStyle"
            class="form-toggle__label is-left"
        >
            <slot name="checked"></slot>
        </span>
        <span
            v-else
            :style="labelStyle"
            class="form-toggle__label is-right"
        >
            <slot name="unchecked"></slot>
        </span>
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
        falseValue: {
            type: String,
            default: '0',
        },
        trueValue: {
            type: String,
            default: '1',
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
        showFalseInput() {
            return this.falseValue != null && !this.value;
        },
    },
    watch: {
        value(v) {
            this.toggled = !!v;
        },
    },
    methods: {
        onChange(event) {
            this.toggled = event.target.checked;
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
