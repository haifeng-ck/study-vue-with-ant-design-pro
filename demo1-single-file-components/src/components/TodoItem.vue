<template>
    <li>
        <slot name="pre-icon">前置图标</slot>
        <span v-if="!del" class="red">{{ title }}</span>
        <span v-else style="text-decoration: line-through">{{ title }}</span>
        <slot name="suf-icon">后置图标</slot>
        <button v-if="!del" @click="handelClick">删除</button>
        <slot name="last-icon" :value="value"></slot>
    </li>
</template>

<script>
    export default {
        name: "TodoItem",
        props: {
            title: String,
            del: {
                type: Boolean,
                default: false
            }
        },
        data() {
            return {
                value: Math.random()
            }
        },
        methods: {
            handelClick() {
                console.log('点击了删除')
                this.$emit('delete', this.title)
            }
        }
    }
</script>

<style scoped>
.red {
    color: red;
}
</style>
