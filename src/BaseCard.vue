<template>
    <transition
            :name="transition"
            mode="in-out"
            appear
            :appear-active-class="enterClass"
            :enter-active-class="enterClass"
            :leave-active-class="leaveClass"
            @after-leave="afterLeave"
    >
        <div class="card is-fullwidth">
            <div class="card-image" v-if="!!this.$slots.image || img">
                <slot name="image">
                    <figure class="image is-4by3">
                        <img :src="img" :alt="alt">
                    </figure>
                </slot>
            </div>
            <header class="card-header" v-if="!!this.$slots.header || title">
                <slot name="header">
                    <p class="card-header-title">{{ title }}</p>
                    <a class="card-header-icon" v-if="!!this.icon">
                        <span class="icon">
                        <i class="fa" :class="[`fa-${icon}`]"></i>
                        </span>
                    </a>
                </slot>
            </header>
            <div class="card-content">
                <slot name="content">
                    {{ content }}
                </slot>
            </div>
            <footer class="card-footer" v-if="!!this.$slots.footer">
                <slot name="footer"></slot>
            </footer>
        </div>
    </transition>
</template>

<script>
    export default {
        props: {
            title: {
                type: String
            },
            img: String,
            alt: String,
            icon: String,
            content: String,
            transition: {
                type: String,
                default: 'fade'
            }
        },

        methods: {
            afterLeave () {
                this.$destroy()
            }
        },

        computed: {
            enterClass () {
                return `${this.transition}In`
            },

            leaveClass () {
                return `${this.transition}Out`
            }
        }
    }
</script>
