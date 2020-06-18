<template>
    <div id="app">
        <!-- v-model 仅仅是一个语法糖（简写形式） -->
        <input v-model="message">
        <!-- 去除 v-model 语法糖 -->
        <input :value="message" @input="handelChange">
        {{ message }}
        <todo-list>
            <!-- 使用默认插槽，可以省略外层 `template` 标签 -->
            <!--<template v-slot>-->
            <todo-item
                    v-for="item in list"
                    :key="item.id"
                    :title="item.title"
                    :del="item.del"
                    @delete="handleDelete"
            >
                <!-- 具名插槽 -->
                <!-- Vue 2.5.x 插槽语法 -->
                <img slot="pre-icon"
                     src="https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1564264355,3357835124&fm=26&gp=0.jpg"
                     alt="前置图标" style="width: 20px; height: 20px;">
                <img slot="suf-icon"
                     src="https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3745390473,3851381912&fm=26&gp=0.jpg"
                     alt="后置图标" style="width: 20px; height: 20px;">
                <!-- Vue 2.6.x 插槽语法 -->
                <template v-slot:last-icon="{ value }">
                    <img src="https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=2586427976,2127777837&fm=26&gp=0.jpg"
                         alt="前置图标" style="width: 20px; height: 20px;">
                    <span>{{ value }}</span>
                </template>
            </todo-item>
            <!--</template>-->
        </todo-list>
    </div>
</template>

<script>
    import TodoList from "./components/TodoList"
    import TodoItem from "./components/TodoItem"

    export default {
        name: 'app',
        components: {
            TodoList,
            TodoItem
        },
        data() {
            return {
                message: 'Hello World !',
                list: [
                    {
                        id: 1,
                        title: '光绪',
                        del: false
                    },
                    {
                        id: 2,
                        title: '慈禧',
                        del: true
                    },
                    {
                        id: 3,
                        title: '荣中堂',
                        del: false
                    }
                ]
            }
        },
        methods: {
            handleDelete(val) {
                console.log('handleDelete', val)
            },
            handelChange(e) {
                this.message = e.target.value
            }
        }
    }
</script>
