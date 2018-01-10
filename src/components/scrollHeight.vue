<template>
    <vue-markdown>{{content}}</vue-markdown>
</template>

<script>
import VueMarkdown from 'vue-markdown'

const content = `
## scrollHeight ##

\`HTMLElement.scrollHeight\` 返回元素的内容区域高度，包括隐藏的部分，包括padding，不包括border、margin

\`scrollHeight = scrollTop + clientHeight\`
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
