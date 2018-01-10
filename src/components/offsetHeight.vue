<template>
    <vue-markdown>{{content}}</vue-markdown>
</template>

<script>
import VueMarkdown from 'vue-markdown'

const content = `
## offsetHeight ##

\`HTMLElement.offsetHeight\` 返回一个元素的布局高度。
元素高度+padding+border+滚动条高度
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
