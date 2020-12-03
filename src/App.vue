<template>
    <!--
        在 Vue 2 中，tempalte 只能取一个根元素。即使我们只有两个 <p> 标记，
        我们也必须将它们包含在一个 <div> 标记中
        Vue 3 中取消了这一限制
    -->
    <img src="./assets/logo.png" />
    <h1>Hello Vue 3!</h1>
    <button @click="inc">Clicked {{ count }} times.</button>
    <button @click="myFun">数组list的值: {{list}}</button>
</template>

<script>
import { ref, reactive, toRefs } from "vue";
export default {
    setup() {
        console.log('setup------>');
        let count = ref(0);
        let inc = () => {
            count.value++;
        };
        let list = ref([1, 2]);
        function myFun() {
            list.value[2] = 3;
        }
        return {
            count,
            inc,
            list,
            myFun
        };
    },
    // setup() {
    //     console.log('setup------>');
    //     const data = reactive({
    //         count: 0,
    //         list: [1, 2],
    //         inc: () => {
    //             data.count++;
    //         },
    //         myFun: () => {
    //             data.list[2] = 3;
    //         }
    //     })

    //     onBeforeMount(() => {
    //         console.log("2-组件挂载到页面之前执行-----onBeforeMount()");
    //     });

    //     onMounted(() => {
    //         console.log("3-组件挂载到页面之后执行-----onMounted()");
    //     });

    //     onBeforeUpdate(() => {
    //         console.log("4-组件更新之前-----onBeforeUpdate()");
    //     });

    //     onUpdated(() => {
    //         console.log("5-组件更新之后-----onUpdated()");
    //     });

    //     const refData = toRefs(data);
    //     return {
    //         ...refData
    //     };
    // },
    beforeCreate () {
        console.log('beforeCreate----->');
    },
    created () {
        console.log('created----->');
    }
};
</script>

<style scoped>
    img {
        width: 100px;
    }
    h1 {
        font-family: Arial, Helvetica, sans-serif;
    }
</style>
