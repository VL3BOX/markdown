<template>
    <div :style="{ fontSize: fontSize, lineHeight: lineHeight, height: fullHeight ? '100%' : 'auto' }" class="auto-textarea-wrapper">
        <pre :style="{ fontSize: fontSize, lineHeight: lineHeight, minHeight: fullHeight ? '100%' : 'auto' }" class="auto-textarea-block"><br/>{{temp_value}} </pre>
        <textarea
            ref="vTextarea"
            :autofocus="s_autofocus"
            @keyup="change"
            spellcheck="false"
            :placeholder="placeholder"
            v-model="temp_value"
            :style="{ fontSize: fontSize, lineHeight: lineHeight }"
            :class="{ 'no-border': !border, 'no-resize': !resize }"
            class="auto-textarea-input"
        >
        </textarea>
    </div>
</template>

<script type="text/ecmascript-6">
export default {
    data() {
        return {
            temp_value: (() => {
                return this.value;
            })(),
            s_autofocus: (() => {
                if (this.autofocus) {
                    return 'autofocus'
                } else {
                    null
                }
            })()
        };
    },
    created() {
    },
    props: {
        fullHeight: {
            type: Boolean,
            default: false
        },
        autofocus: {
            type: Boolean,
            default: false
        },
        value: {
            type: String,
            default: ''
        },
        placeholder: {
            type: String,
            default: ''
        },
        border: {
            type: Boolean,
            default: false
        },
        resize: {
            type: Boolean,
            default: false
        },
        onchange: {
            type: Function,
            default: null
        },
        fontSize: {
            type: String,
            default: '14px'
        },
        lineHeight: {
            type: String,
            default: '18px'
        }
    },
    methods: {
        change($event) {
            if (this.onchange) {
                this.onchange(this.temp_value , $event)
            }
        }
    },
    watch: {
        value: function (val, oldVal) {
            this.temp_value = val
        },
        temp_value: function (val, oldVal) {
            this.$emit('input' , val)
        }
    }
};
</script>
<style>
.auto-textarea-wrapper {
    position: relative;
    width: 100%;
    margin: 0;
    padding: 0;
    line-height: normal;
}
.auto-textarea-wrapper .auto-textarea-block {
    display: block;
    white-space: pre-wrap;
    word-wrap: break-word !important;
    visibility: hidden;
    overflow: hidden;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-size: 100%;
}
.auto-textarea-wrapper .auto-textarea-input {
    font-family: Menlo, "Ubuntu Mono", Consolas, "Courier New", "Microsoft Yahei", "Hiragino Sans GB", "WenQuanYi Micro Hei", sans-serif;
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    margin: 0;
    padding: 0;
    overflow-y: hidden;
    color: #2c3e50;
}
.auto-textarea-wrapper .auto-textarea-input.no-border {
    outline: 0 none;
    border: none !important;
}
.auto-textarea-wrapper .auto-textarea-input.no-resize {
    resize: none;
}
</style>
