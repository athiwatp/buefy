<template>
    <label class="checkbox" :class="{ 'is-disabled': disabled }">
        <input
            type="checkbox"
            :disabled="disabled"
            :name="name"
            v-model="newValue"
            @change="$emit('change', newValue, $event)">
        <span><slot></slot></span>
    </label>
</template>

<script>
    export default {
        name: 'bCheckbox',
        props: {
            value: Boolean,
            disabled: Boolean,
            name: String,
            checked: Boolean,
            customValue: [String, Number, Boolean]
        },
        data() {
            return {
                newValue: this.value
            }
        },
        watch: {
            value(value) {
                this.newValue = value
            },
            newValue(value) {
                this.$emit('input', value)
                this.$parent.isCheckboxGroup && this.$parent.updateValue()
            }
        },
        mounted() {
            if (this.checked) {
                this.newValue = this.checked
            }
        }
    }
</script>
