<template>
    <vue-markdown>{{content}}</vue-markdown>
</template>

<script>
import VueMarkdown from 'vue-markdown'

const content = `
## cssWidth ##

CSS样式表上的宽度，js获取方式：

\`\`\`javascript
var style = window.getComputedStyle("元素", "伪类")
style.width
\`\`\`
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
