<template>
<div id="app">
    <div id="view">
        <div id="content" ref="content" @scroll="handleScroll">
            <p>喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵</p>
            <img src="./assets/img.jpg">
        </div>
        <div id="clone" ref="clone">
            <p>喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵喵</p>
            <img src="./assets/img.jpg">
        </div>
        <div id="overlay">
            <div
                v-for="api in apis"
                :key="api.id"
                :id="api.id"
                :ref="api.id"
                :t="api.t"
                :v="api.v"
                :txt="api.txt || api.id"
                :class="{
                    active: !filter || ~filter.indexOf(api.id)
                }"
            >
            </div>
        </div>
    </div>

    <Side @change="change"></Side>
</div>
</template>

<script>
import Side from './Side.vue'

export default {
    name: "app",
    components: {
        Side,
    },
    data(){
        return {
            apis: [
                {
                    id: 'cssWidth',
                    t: 'width',
                },
                {
                    id: 'cssHeight',
                    t: 'height',
                },
                {
                    id: 'clientWidth',
                    t: 'width',
                },
                {
                    id: 'clientHeight',
                    t: 'height',
                },
                {
                    id: 'clientLeft',
                    t: 'width',
                    v: 'bottom',
                },
                {
                    id: 'clientTop',
                    t: 'height',
                    v: 'bottom',
                },
                
                {
                    id: 'scrollWidth',
                    t: 'width',
                },
                {
                    id: 'scrollHeight',
                    t: 'height',
                },
                {
                    id: 'scrollLeft',
                    t: 'width',
                    v: 'bottom',
                },
                {
                    id: 'scrollTop',
                    t: 'height',
                    v: 'bottom',
                },
                {
                    id: 'offsetWidth',
                    t: 'width',
                },
                {
                    id: 'offsetHeight',
                    t: 'height',
                },
                {
                    id: 'offsetLeft',
                    t: 'width',
                    v: 'bottom',
                },
                {
                    id: 'offsetTop',
                    t: 'height',
                },
                {
                    id: 'getBoundingClientRectLeft',
                    txt: 'getBoundingClientRect().left',
                    t: 'width',
                    v: 'bottom',
                },
                {
                    id: 'getBoundingClientRectTop',
                    txt: 'getBoundingClientRect().top',
                    t: 'height',
                    v: 'bottom',
                },
            ],
            filter: '',
            contentStyle: {}
        }
    },
    mounted() {
        this.$nextTick(function () {
            this.contentStyle = window.getComputedStyle(this.$refs.clone, null)
            const img = new Image()
            img.onload = () => {
                this.cssWidthInit()
                this.cssHeightInit()
                this.clientWidthInit()
                this.clientHeightInit()
                this.clientLeftInit()
                this.clientTopInit()
                this.offsetWidthInit()
                this.offsetHeightInit()
                this.scrollWidthInit()
                this.scrollHeightInit()
                this.scrollLeftInit()
                this.scrollTopInit()
                this.offsetLeftInit()
                this.offsetTopInit()
                this.getBoundingClientRectLeftInit()
                this.getBoundingClientRectTopInit()
            }
            img.src = this.$refs.content.querySelector('img').src
        })
    },
    updated() {

    },
    watch: {
        contentStyle(contentStyle) {
            
        }
    },
    methods: {
        cssWidthInit() {
            this.$refs.cssWidth[0].style.width = this.contentStyle.getPropertyValue('width')
            this.$refs.cssWidth[0].style.top = `${this.$refs.content.offsetTop - 30}px`
            this.$refs.cssWidth[0].style.left = `${this.$refs.content.offsetLeft + parseInt(this.contentStyle.borderLeftWidth) + parseInt(this.contentStyle.paddingLeft)}px`
        },
        cssHeightInit() {
            this.$refs.cssHeight[0].style.height = this.contentStyle.getPropertyValue('height')
            this.$refs.cssHeight[0].style.top = `${this.$refs.content.offsetTop + parseInt(this.contentStyle.borderLeftWidth) + parseInt(this.contentStyle.paddingTop)}px`
            this.$refs.cssHeight[0].style.left = `${this.$refs.content.offsetLeft - 30}px`
        },
        clientWidthInit() {
            this.$refs.clientWidth[0].style.width = `${this.$refs.content.clientWidth}px`
            this.$refs.clientWidth[0].style.top = `${this.$refs.content.offsetTop - 60}px`
            this.$refs.clientWidth[0].style.left = `${this.$refs.content.offsetLeft + parseInt(this.contentStyle.borderLeftWidth)}px`
        },
        clientHeightInit() {
            this.$refs.clientHeight[0].style.height = `${this.$refs.content.clientHeight}px`
            this.$refs.clientHeight[0].style.top = `${this.$refs.content.offsetTop + parseInt(this.contentStyle.borderLeftWidth)}px`
            this.$refs.clientHeight[0].style.left = `${this.$refs.content.offsetLeft - 60}px`
        },
        clientLeftInit() {
            this.$refs.clientLeft[0].style.width = `${this.$refs.content.clientLeft}px`
            this.$refs.clientLeft[0].style.top = `${this.$refs.content.offsetTop + this.$refs.content.offsetHeight + 60}px`
            this.$refs.clientLeft[0].style.left = `${this.$refs.content.offsetLeft}px`
        },
        clientTopInit() {
            this.$refs.clientTop[0].style.height = `${this.$refs.content.clientTop}px`
            this.$refs.clientTop[0].style.top = `${this.$refs.content.offsetTop}px`
            this.$refs.clientTop[0].style.left = `${this.$refs.content.offsetLeft + this.$refs.content.offsetWidth + 60}px`
        },
        offsetWidthInit() {
            this.$refs.offsetWidth[0].style.width = `${this.$refs.content.offsetWidth}px`
            this.$refs.offsetWidth[0].style.top = `${this.$refs.content.offsetTop - 90}px`
            this.$refs.offsetWidth[0].style.left = `${this.$refs.content.offsetLeft}px`
        },
        offsetHeightInit() {
            this.$refs.offsetHeight[0].style.height = `${this.$refs.content.offsetHeight}px`
            this.$refs.offsetHeight[0].style.top = `${this.$refs.content.offsetTop}px`
            this.$refs.offsetHeight[0].style.left = `${this.$refs.content.offsetLeft - 90}px`
        },
        scrollWidthInit() {
            this.$refs.scrollWidth[0].style.width = `${this.$refs.content.scrollWidth}px`
            this.$refs.scrollWidth[0].style.top = `${this.$refs.content.offsetTop - 120}px`
            this.$refs.scrollWidth[0].style.left = `${this.$refs.content.offsetLeft + parseInt(this.contentStyle.borderLeftWidth)}px`
        },
        scrollHeightInit() {
            this.$refs.scrollHeight[0].style.height = `${this.$refs.content.scrollHeight}px`
            this.$refs.scrollHeight[0].style.top = `${this.$refs.content.offsetTop + parseInt(this.contentStyle.borderLeftWidth)}px`
            this.$refs.scrollHeight[0].style.left = `${this.$refs.content.offsetLeft - 120}px`
        },
        scrollLeftInit() {
            this.$refs.scrollLeft[0].style.width = `${this.$refs.content.scrollLeft}px`
            this.$refs.scrollLeft[0].style.top = `${this.$refs.content.offsetTop + this.$refs.content.offsetHeight + 30}px`
            this.$refs.scrollLeft[0].style.left = `${this.$refs.content.offsetLeft + parseInt(this.contentStyle.borderLeftWidth) - this.$refs.content.scrollLeft}px`
            // this.$refs.scrollLeft[0].style.width = `${this.$refs.content.scrollLeft * this.$refs.content.clientWidth / this.$refs.content.scrollWidth}px`
            // this.$refs.scrollLeft[0].style.top = `${this.$refs.content.offsetTop + this.$refs.content.offsetHeight + 90}px`
            // this.$refs.scrollLeft[0].style.left = `${this.$refs.content.offsetLeft + parseInt(this.contentStyle.borderLeftWidth)}px`
        },
        scrollTopInit() {
            this.$refs.scrollTop[0].style.height = `${this.$refs.content.scrollTop}px`
            this.$refs.scrollTop[0].style.top = `${this.$refs.content.offsetTop + parseInt(this.contentStyle.borderLeftWidth) - this.$refs.content.scrollTop}px`
            this.$refs.scrollTop[0].style.left = `${this.$refs.content.offsetLeft + this.$refs.content.offsetWidth + 30}px`
            // this.$refs.scrollTop[0].style.height = `${this.$refs.content.scrollTop * this.$refs.content.clientHeight / this.$refs.content.scrollHeight}px`
            // this.$refs.scrollTop[0].style.top = `${this.$refs.content.offsetTop + parseInt(this.contentStyle.borderLeftWidth)}px`
            // this.$refs.scrollTop[0].style.left = `${this.$refs.content.offsetLeft + this.$refs.content.offsetWidth + 90}px`
        },
        offsetLeftInit() {
            this.$refs.offsetLeft[0].style.width = `${this.$refs.content.offsetLeft}px`
            this.$refs.offsetLeft[0].style.top = `${this.$refs.content.offsetTop + this.$refs.content.offsetHeight + 60}px`
            this.$refs.offsetLeft[0].style.left = `0px`
        },
        offsetTopInit() {
            this.$refs.offsetTop[0].style.height = `${this.$refs.content.offsetTop}px`
            this.$refs.offsetTop[0].style.top = `0px`
            this.$refs.offsetTop[0].style.left = `${this.$refs.content.offsetLeft - 60}px`
        },
        getBoundingClientRectLeftInit() {
            this.$refs.getBoundingClientRectLeft[0].style.width = `${this.$refs.content.getBoundingClientRect().left}px`
            this.$refs.getBoundingClientRectLeft[0].style.top = `${this.$refs.content.offsetTop + this.$refs.content.offsetHeight + 90}px`
            this.$refs.getBoundingClientRectLeft[0].style.left = `${this.$refs.content.offsetLeft - this.$refs.content.getBoundingClientRect().left}px`
        },
        getBoundingClientRectTopInit() {
            this.$refs.getBoundingClientRectTop[0].style.height = `${this.$refs.content.getBoundingClientRect().top}px`
            this.$refs.getBoundingClientRectTop[0].style.top = `${this.$refs.content.offsetTop - this.$refs.content.getBoundingClientRect().top}px`
            this.$refs.getBoundingClientRectTop[0].style.left = `${this.$refs.content.offsetLeft + this.$refs.content.offsetWidth + 90}px`
        },
        handleScroll(e){
            ['clone', 'cssHeight', 'scrollHeight'].forEach(id => {
                if (this.$refs[id][0]) {
                    this.$refs[id][0].style.marginTop = `${-e.target.scrollTop}px`
                } else {
                    this.$refs[id].style.marginTop = `${-e.target.scrollTop}px`
                }
            });
            ['clone', 'cssWidth', 'scrollWidth'].forEach(id => {
                if (this.$refs[id][0]) {
                    this.$refs[id][0].style.marginLeft = `${-e.target.scrollLeft}px`
                } else {
                    this.$refs[id].style.marginLeft = `${-e.target.scrollLeft}px`
                }
            });
            ['scrollLeft', 'scrollTop'].forEach(id => {
                this[`${id}Init`]()
            });
        },
        change(val){
            this.filter = val
        }
    }
};
</script>

<style lang="postcss">
@import './assets/style.css';

:root {
    --content-width: 200px;
    --content-height: 200px;
    --content-pt: 80px;
    --content-bd: 10px;
}

#app{
    position: relative;
    margin: 20px;
    border: 1px dashed #ddd;
}

#clone,
#content{
    width: var(--content-width);
    height: var(--content-height);
    min-width: var(--content-width);
    min-height: var(--content-height);
    margin: 150px;
    padding: var(--content-pt);
    border: var(--content-bd) solid #78BBE6;
    background: #fff;
    background: #fdfdf2;
    overflow: auto;
    & img{
        display: block;
        width: 420px;
    }
}

#content{
    position: relative;
    &:before{
        content: '';
        position: absolute;
        top: 80px;
        left: 80px;
        width: 200px;
        height: 200px;
        min-height: 200px;
        outline: 1px dashed #eee;
    }
    &:after{
        content: '';
        display: block;
        clear: both;
    }
}

#clone{
    position: absolute;
    top: 150px;
    left: 150px;
    margin: 0;
    opacity: 0.2;
    pointer-events: none;
    border-color: transparent;
    background: transparent;
    overflow: visible;
}
#overlay {
    text-align: center;
    &,
    & *{
        pointer-events: none;
    }
    & div {
        position: absolute;
        width: 20px;
        height: 20px;
        overflow: visible;
        visibility: hidden;
        opacity: 0;
        transition: opacity .3s;
        &.active{
            visibility: visible;
            opacity: 1;
        }

        &:before, 
        &:after {
            position: absolute;
            display: block;
            z-index: 1;
        }
        &:before {
            content: attr(txt);
        }
        &:after {
            content: '';
        }

        &[t="width"]:before{
            width: 100%;
        }
        &[t="width"]:after{
            border-left: 1px dashed;
            border-right: 1px dashed;
            right: 0;
            width: 100%;
            box-sizing: border-box;
        }
        &[t="height"]:before{
            writing-mode: vertical-rl;
            transform: rotate(180deg);
            height: 100%;
        }
        &[t="height"]:after{
            border-top: 1px dashed;
            border-bottom: 1px dashed;
            bottom: 0;
            height: 100%;
            box-sizing: border-box;
        }
        &[t="width"][v="bottom"]{
            &:before,
            &:after{
                bottom: 0;
            }
        }
        &[t="height"][v="bottom"]{
            &:before,
            &:after{
                right: 0;
            }
        }
    }
    & #cssWidth{
        color: #1160AA;
        background: #D5EEFF;
        &:after {
            height: calc(var(--content-height) + var(--content-pt) * 2 + var(--content-bd) * 2 + 30px);
        }
    }
    & #cssHeight{
        color: #1160AA;
        background: #D5EEFF;
        &:after {
            width: calc(var(--content-width) + var(--content-pt) * 2 + var(--content-bd) * 2 + 30px);
        }
    }
    & #clientWidth{
        color: #F70776;
        background: #FFD6D6;
        &:after {
            height: calc(var(--content-height) + var(--content-pt) * 2 + var(--content-bd) * 2 + 60px);
        }
    }
    & #clientHeight{
        color: #F70776;
        background: #FFD6D6;
        &:after {
            width: calc(var(--content-width) + var(--content-pt) * 2 + var(--content-bd) * 2 + 60px);
        }
    }
    & #clientLeft{
        color: #57ACC5;
        background: #E8ECF1;
        &:after {
            height: calc(var(--content-height) + var(--content-pt) * 2 + var(--content-bd) * 2 + 60px + 20px);
        }
    }
    & #clientTop{
        color: #57ACC5;
        background: #E8ECF1;
        // color: #45ADA8;
        // background: #E5FCC2;
        &:after {
            width: calc(var(--content-width) + var(--content-pt) * 2 + var(--content-bd) * 2 + 60px + 10px);
        }
    }
    & #offsetWidth{
        color: #11BFAE;
        background: #BFF4ED;
        &:after {
            height: calc(var(--content-height) + var(--content-pt) * 2 + var(--content-bd) * 2 + 90px);
        }
    }
    & #offsetHeight{
        color: #11BFAE;
        background: #BFF4ED;
        &:after {
            width: calc(var(--content-width) + var(--content-pt) * 2 + var(--content-bd) * 2 + 90px);
        }
    }
    & #scrollWidth{
        color: #F09872;
        // color: #355C7D;
        background: #FAF8D7;
        &:after {
            height: calc(var(--content-height) + var(--content-pt) * 2 + var(--content-bd) * 2 + 120px);
        }
    }
    & #scrollHeight{
        color: #F09872;
        // color: #355C7D;
        background: #FAF8D7;
        &:after {
            width: calc(var(--content-width) + var(--content-pt) * 2 + var(--content-bd) * 2 + 120px);
        }
    }
    & #scrollLeft{
        color: #EB55BF;
        background: #f5d9f7;
        &:after {
            height: calc(var(--content-height) + var(--content-pt) * 2 + var(--content-bd) * 2 + 30px + 20px);
        }
    }
    & #scrollTop{
        color: #EB55BF;
        background: #f5d9f7;
        &:after {
            width: calc(var(--content-width) + var(--content-pt) * 2 + var(--content-bd) * 2 + 30px + 20px);
        }
    }
    & #offsetLeft{
        color: #43405D;
        background: #EEEEEE;
        &:after {
            height: calc(var(--content-height) + var(--content-pt) * 2 + var(--content-bd) * 2 + 60px + 20px);
        }
    }
    & #offsetTop{
        color: #43405D;
        background: #EEEEEE;
        &:after {
            width: calc(var(--content-width) + var(--content-pt) * 2 + var(--content-bd) * 2 + 60px);
        }
    }
    & #getBoundingClientRectLeft{
        color: #45ADA8;
        background: honeydew;
        font-size: 12px;
        &:after {
            height: calc(var(--content-height) + var(--content-pt) * 2 + var(--content-bd) * 2 + 90px + 20px);
        }
    }
    & #getBoundingClientRectTop{
        color: #45ADA8;
        background: honeydew;
        font-size: 12px;
        &:after {
            width: calc(var(--content-width) + var(--content-pt) * 2 + var(--content-bd) * 2 + 90px + 20px);
        }
    }
}

</style>
