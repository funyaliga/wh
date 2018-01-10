<template>
    <vue-markdown>{{content}}</vue-markdown>
</template>

<script>
import VueMarkdown from 'vue-markdown'

const content = `
## scrollWidth ##

\`HTMLElement.scrollWidth\` 返回元素的内容区域宽度，包括隐藏的部分，包括padding，不包括border、margin

\`scrollWidth = scrollLeft + clientWidth\`
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
