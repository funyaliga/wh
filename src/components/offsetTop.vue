<template>
    <vue-markdown>{{content}}</vue-markdown>
</template>

<script>
import VueMarkdown from 'vue-markdown'

const content = `
## offsetTop ##

\`HTMLElement.offsetTop\` 返回当前元素顶部相对于 \`HTMLElement.offsetParent\` 节点（相当于 最近的、CSS position 属性被设置为 \`relative\`、\`absolute\` 或 \`fixed\` 的祖先元素 或者 \`body\`）的上边界偏移的像素值。
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
