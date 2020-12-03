
# 前言
Vue.js 3.0 "One Piece" 已正式发布啦，在 2020 年 9 月 19 日 Vue3 更新了 正式版本，正式版本一出，代表着不会再有太大的改动了，也意味着又要开始学习啦
官方网站地址: v3.vuejs.org

 ## 新特性
 ### 1 向下兼容
Vue3和Vue2是一样的，也是一套用于构建用户界面的渐进式框架，并且向下兼容，也就是说用Vue2的语法基于Vue3进行开发是没有问题的
### 2  性能的提升
官方网站给出的数据是：打包大小减少 41%，初次渲染快 55%，更新快 133%，内存使用减少 54% (不禁感叹大佬还是大佬，请收下我的膝盖)
### 3 更好TypeScript支持
Vue3 的源代码就是使用TypeScript进行开发的
### 4 Composition API
Vue 官方发布了 Composition API 的官方插件，使广大用户可以在 Vue2.x 中享受 Function Base 带来的新体验。
而在 vue 3 中无需单独安装插件，开箱即用
### 5 Multiple root elements
在 Vue 2 中，tempalte 只能取一个根元素。即使我们只有两个p标签 标记，我们也必须将它们包含在一个根元素中，在 Vue 3 中取消了这一限制：可以直接在template标签中使用任意数量的标签:

## 通过vue-cli搭建Vue3
### 1 安装vue-cli
```
npm install -g @vue/cli   // 安装

通过命令vue --version获取版本信息，如果你的版本低于V4.5.4，可以再使用npm install -g @vue/cli来进行安装，因为只有最新版本(V4.5.4 以上版本)才有创建 Vue3 的选项。

通过命令vue create vue3即可创建vue3项目
Please pick a preset: (Use arrow keys)                      // 请选择预选项
> Default ([Vue 2] babel, eslint)                               // 使用Vue2默认模板进行创建
   Default (Vue 3 Preview) ([Vue 3] babel, eslint)     // 使用Vue3默认模板进行创建
   Manually select features                                       // 手动选择(自定义)
   
我们选择第二个使用Vue3默认模板进行创建
```
这样我们就创建出一个vue3的项目啦


## 通过案例加深对Vue3的理解
### 案例1 setup 与 ref
```javascript
import { ref } from "vue";
setup() {
        // Composition API
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
}
```
setup 函数的用法，可以代替 Vue2 中的 data 和 methods 属性，直接把逻辑挂载 setup 里，return出去就可以了。
注意：setup 函数创建组件之前，在beforeCreate和created之前执行

通过ref函数可以创建响应式数据，在setup中需要通过xxx.value的形式才能获取到值，在template中无需通过xxx.value的形式，只需要xxx即可获取到值

### 案例2 reactive与toRefs
在案例1中我们不难发现，ref可以实现响应式数据，方法可以通过return的形式暴露到template中使用，所有的变量和方法都混淆在一起，可以说没什么章法可言，最难受的是在setup中要改变和读取一个ref返回的值，还要加上value。很容易开发时候就遗忘，这种代码一定是可以优化的。这个时候就需要用到reactive，他是一个方法，接收一个对象参数。

```javascript
import { ref, reactive, toRefs } from "vue";
setup() {
        console.log('setup------>');
        const data = reactive({
            count: 0,
            list: [1, 2],
            inc: () => {
                data.count++;
            },
            myFun: () => {
                data.list[2] = 3;
            }
        })

        const refData = toRefs(data);
        return {
            ...refData
        };
    },
```
通过reactive方法无论是变量和方法，都可以作为 参数Object 中的一个属性，而且在改变某个属性值的时候也不用再加讨厌的value属性了。再return返回的时候也不用一个个返回了，只需要返回一个data,就可以了。

toRefs函数则是可以将一个reactive生成的对象，转化为ref，在template模板中就不需要用data.xxx的形式了


### 案例3 生命周期
通过Vue3与Vue2生命周期的对比，进行了解
值得注意的是vue3中的setup要比beforeCreate和created 更早的执行，vue2的destroyed 对应的是onUnmounted
|  vue2 |  vue3  |
| ------------ | ------------ |
| beforeCreate  |   setup|
|  created    |  setup |
|  beforeMount    |  onBeforeMount |
|  mounted    |  onMounted |
|  beforeUpdate    |  onBeforeUpdate |
|  updated    |  onUpdated |
|  destroyed    |  onUnmounted |
|  activated    |  onActivated |
|  deactivated    |  onDeactivated |

