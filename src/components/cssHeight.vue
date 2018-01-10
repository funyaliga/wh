<template>
    <vue-markdown>{{content}}</vue-markdown>
</template>

<script>
import VueMarkdown from 'vue-markdown'

const content = `
## cssHeight ##

CSS样式表上的高度，js获取方式：

\`\`\`javascript
var style = window.getComputedStyle("元素", "伪类")
style.height
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
