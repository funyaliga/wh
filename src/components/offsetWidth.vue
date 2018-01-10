<template>
    <vue-markdown>{{content}}</vue-markdown>
</template>

<script>
import VueMarkdown from 'vue-markdown'

const content = `
## offsetWidth ##

\`HTMLElement.offsetWidth\` 返回一个元素的布局宽度。
元素宽度+padding+border+滚动条宽度
`

export default {
    data() {
        return {
            content,
        }
    },
    components: {
        VueMarkdown,
    }
}
</script>
