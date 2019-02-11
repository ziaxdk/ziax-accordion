<template>
    <div>
        <div @click="toggle()">
            <slot name="header">[header]</slot>
        </div>
        <transition @before-enter="be" @enter="e" @before-leave="bl" @leave="l">
            <div ref="el" v-show="selected === thisValue" class="body" :style="transition">
                <slot name="body">[body]</slot>
            </div>
        </transition>
    </div>
</template>

<script>

const calc = (el) => el.style.height = `${el.scrollHeight}px`
const zero = (el) => el.style.height = '0px'

export default {
    props: {
        duration: {
            type: Number,
            default: 300
        },
        value: {}
    },
    computed: {
        thisValue () {
            return this.value || this.$vnode.key
        },
        selected () {
            return this.$parent.value
        },
        transition () {
            return `transition: height ${this.duration}ms;`
        }
    },
    methods: {
        toggle () {
            const same = this.thisValue === this.selected ? null : this.thisValue
            this.$parent.$emit('input', same)
        },
        be (el) {
            zero(el)
        },
        e (el, done) {
            calc(el)
            setTimeout(done, this.duration)
        },
        bl (el) {
            calc(el)
        },
        l (el, done) {
            zero(el)
            setTimeout(done, this.duration)
        }
    },
    mounted () {
        if (this.selected === this.thisValue) {
            this.$refs.el.style.height = `${this.$refs.el.scrollHeight}px`
        }
    }
}
</script>

<style scoped>
.v-enter-active.body, .v-leave-active.body {
    overflow: hidden;
}

</style>
