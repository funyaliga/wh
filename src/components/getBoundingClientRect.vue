<template>
    <vue-markdown>{{content}}</vue-markdown>
</template>

<script>
import VueMarkdown from 'vue-markdown'

const content = `
## getBoundingClientRect ##

\`Element.getBoundingClientRect()\` 返回元素的大小及其相对于视口的位置
属性有left、top、right、bottom、width、height、x、y
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
