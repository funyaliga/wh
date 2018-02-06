<template>
    <div id="api">
        <div id="filter">
            <c-radio
                :options="apis.map(v => ({
                    label: v.name,
                    value: v.hasOwnProperty('value') ? v.value : v.name,
                }))"
                @input="radioChange"
                :defaultValue="selected"
            ></c-radio>
        </div>
        <div id="introduce" class="markdown-body">
            <component :is="compIntroduce"></component>
        </div>
    </div>
</template>

<script>
import cRadio from './components/radio'
import 'github-markdown-css'
const allTemp = { template: '<div></div>' }

export default {
    name: 'Side',
    components: {
        [cRadio.name]: cRadio,
        all: allTemp,
    },
    data() {
        return {
            selected: '',
            apis: [
                {
                    name: 'all',
                    value: '',
                    introduce: '',
                },
                {
                    name: 'cssWidth',
                    introduce: () => import('./components/cssWidth'),
                },
                {
                    name: 'cssHeight',
                    introduce: () => import('./components/cssHeight'),
                },
                {
                    name: 'clientWidth',
                    introduce: () => import('./components/clientWidth'),
                },
                {
                    name: 'clientHeight',
                    introduce: () => import('./components/clientHeight'),
                },
                {
                    name: 'clientLeft',
                    introduce: () => import('./components/clientLeft'),
                },
                {
                    name: 'clientTop',
                    introduce: () => import('./components/clientTop'),
                },
                {
                    name: 'offsetWidth',
                    introduce: () => import('./components/offsetWidth'),
                },
                {
                    name: 'offsetHeight',
                    introduce: () => import('./components/offsetHeight'),
                },
                {
                    name: 'offsetLeft',
                    introduce: () => import('./components/offsetLeft'),
                },
                {
                    name: 'offsetTop',
                    introduce: () => import('./components/offsetTop'),
                },
                {
                    name: 'scrollWidth',
                    introduce: () => import('./components/scrollWidth'),
                },
                {
                    name: 'scrollHeight',
                    introduce: () => import('./components/scrollHeight'),
                },
                {
                    name: 'scrollLeft',
                    introduce: () => import('./components/scrollLeft'),
                },
                {
                    name: 'scrollTop',
                    introduce: () => import('./components/scrollTop'),
                },
                {
                    name: 'getBoundingClientRect',
                    value: 'getBoundingClientRectLeft, getBoundingClientRectTop',
                    introduce: () => import('./components/getBoundingClientRect'),
                },
            ]
        }
    },
    computed: {
        compIntroduce(){
            return this.apis.find(v => v.name === this.selected || v.value === this.selected).introduce || allTemp
        }
    },
    methods: {
        radioChange(val) {
            this.selected = val
            this.$emit('change', val)
        }
    }
}
</script>

<style lang="postcss">
@import './assets/style.css';

#api{
    position: absolute;
    top: -20px;
    left: 700px;
    right: -20px;
    height: 100vh;    
    background: #6C567B;
    color: #fff;
    &,
    & *{
        box-sizing: border-box;
    }
    & .markdown-body{
        color: #fff;
        & code {
            background: rgba(27, 31, 35, .5);
        }
        & pre code{
            color: #607D8B;
            background: transparent;
        }
    }
}


#filter{
    height: 250px;
    padding: 10px;
    border-bottom: 2px dashed #fff;
    overflow: auto;
    & .m-radio{
        display: flex;
        flex-wrap: wrap;
    }
    & .radio-label{
        position: relative;
        flex: 1;
        display: inline-block;
        padding: 4px 10px;
        margin: 4px;
        border: 2px dashed #C06C84;
        text-align: center;
        cursor: pointer;
        z-index: 1;
        & input{
            position: absolute;
            left: 0;
            width: 0;
            height: 0;
            overflow: hidden;
            opacity: 0;
            &:checked {
                &+.radio-label-check{
                    position: absolute;
                    left: 0;
                    top: 0;
                    width: 100%;
                    height: 100%;
                    background: #C06C84;
                    z-index: -1;
                }
            }
        }
    }
}
#introduce{
    height: calc(100vh - 250px);
    padding: 10px;
    overflow: auto;
}
</style>