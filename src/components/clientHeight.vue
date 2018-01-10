<template>
    <vue-markdown>{{content}}</vue-markdown>
</template>

<script>
import VueMarkdown from 'vue-markdown'

const content = `
## clientHeight ##

\`Element.clientHeight\` 属性表示元素的内部高度，以像素计。该属性包括内边距，但不包括垂直滚动条（如果有）、边框和外边距。 
可以通过 CSS \`height\` + CSS \`padding\` - 水平滚动条高度 (如果存在)来计算.
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
