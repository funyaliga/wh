<template>
    <transition :name="animation">
        <div class="loading-overlay is-active" v-if="isActive">
            <svg id="load" x="0px" y="0px" viewBox="0 0 150 150" >
                <circle id="loading-inner" cx="75" cy="75" r="60" />
            </svg>
        </div>
    </transition>
</template>

<script>
function removeElement(el) {
    if (typeof el.remove !== 'undefined') {
        el.remove()
    } else {
        el.parentNode.removeChild(el)
    }
}

export default {
    name: 'BLoading',
    props: {
        active: Boolean,
        programmatic: Boolean,
        animation: {
            type: String,
            default: 'fade'
        },
        canCancel: {
            type: Boolean,
            default: false
        },
        onCancel: {
            type: Function,
            default: () => {}
        }
    },
    data() {
        return {
            isActive: this.active || false
        }
    },
    watch: {
        active(value) {
            this.isActive = value
        }
    },
    methods: {
        /**
         * Close the Modal if canCancel.
         */
        cancel() {
            if (!this.canCancel) return
            this.close()
        },
        /**
         * Emit events, and destroy modal if it's programmatic.
         */
        close() {
            this.onCancel.apply(null, arguments)
            this.$emit('close')
            this.$emit('update:active', false)
            // Timeout for the animation complete before destroying
            if (this.programmatic) {
                this.isActive = false
                setTimeout(() => {
                    this.$destroy()
                    removeElement(this.$el)
                }, 150)
            }
        },
    },
  
    beforeMount() {
        // Insert the Loading component in body tag
        // only if it's programmatic
        this.programmatic && document.body.appendChild(this.$el)
    },
    mounted() {
        if (this.programmatic) this.isActive = true
    },
    beforeDestroy() {
        if (typeof window !== 'undefined') {
            document.removeEventListener('keyup', this.keyPress)
        }
    }
}
</script>

<style lang="postcss">
.loading-overlay {
   position: fixed;
   top: 0;
   left: 0;
   width: 100%;
   height: 100%;
   background: rgba(255, 255, 255, .8);
   text-align: center;
   z-index: 100;
   & #load,
   &:after{
       display: inline-block;
       vertical-align: middle;
   }
   &:after{
       content: '';
       height: 100%;
   }
}

#load {
	width: 150px;
    animation: loading 3s linear infinite;
    & > #loading-inner {
        stroke-dashoffset: 0;
        stroke-dasharray: 300;
        stroke-width: 10;
        stroke-miterlimit: 10;
        stroke-linecap: round;
        animation: loading-circle 2s linear infinite;
        stroke: #51BBA7;
        fill: transparent;
    }
}

@keyframes loading {
	0% { 
      transform: rotate(0); 
    }
		100% { 
      transform: rotate(360deg);
    }
}
@keyframes loading-circle {
	0% { 
      stroke-dashoffset: 0
    }
	100% { 
      stroke-dashoffset: -600;
    }
}
</style>
