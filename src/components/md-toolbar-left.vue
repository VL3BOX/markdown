<template>
    <div class="v-left-item">
        <slot name="left-toolbar-before" />
        <!-- 标题 -->
        <div
            :class="{ selected: s_header_dropdown_open }"
            :disabled="!editable"
            type="button"
            v-if="toolbars.header"
            @mouseleave="$mouseleave_header_dropdown"
            @mouseenter="$mouseenter_header_dropdown"
            class="op-icon fa fa-mavon-header dropdown dropdown-wrapper"
            aria-hidden="true"
            :title="`${d_words.tl_header} (ctrl+h)`"
        >
            <transition name="fade">
                <div
                    class="op-header popup-dropdown"
                    :class="{ transition: transition }"
                    v-show="s_header_dropdown_open"
                    @mouseenter="$mouseenter_header_dropdown"
                    @mouseleave="$mouseleave_header_dropdown"
                >
                    <div title="#" class="dropdown-item" @click.stop="$click_header('header1')">
                        <span>{{ d_words.tl_header_one }}</span>
                    </div>
                    <div title="## " class="dropdown-item" @click.stop="$click_header('header2')">
                        <span>{{ d_words.tl_header_two }}</span>
                    </div>
                    <div title="### " class="dropdown-item" @click.stop="$click_header('header3')">
                        <span>{{ d_words.tl_header_three }}</span>
                    </div>
                    <div title="#### " class="dropdown-item" @click.stop="$click_header('header4')">
                        <span>{{ d_words.tl_header_four }}</span>
                    </div>
                    <div title="##### " class="dropdown-item" @click.stop="$click_header('header5')">
                        <span>{{ d_words.tl_header_five }}</span>
                    </div>
                    <div title="###### " class="dropdown-item" @click.stop="$click_header('header6')">
                        <span>{{ d_words.tl_header_six }}</span>
                    </div>
                </div>
            </transition>
        </div>
        <!-- 链接 -->
        <button
            :disabled="!editable"
            type="button"
            v-if="toolbars.link"
            @click.stop="$toggle_imgLinkAdd('link')"
            class="op-icon fa fa-mavon-link"
            aria-hidden="true"
            :title="`${d_words.tl_link} (ctrl+l)`"
        ></button>

        <span class="op-icon-divider"></span>

        <!-- 粗体 -->
        <button :disabled="!editable" type="button" v-if="toolbars.bold" @click="$clicks('bold')" class="op-icon fa fa-mavon-bold" aria-hidden="true" :title="`${d_words.tl_bold} (ctrl+b)`"></button>
        <!-- 斜体 -->
        <button
            :disabled="!editable"
            type="button"
            v-if="toolbars.italic"
            @click="$clicks('italic')"
            class="op-icon fa fa-mavon-italic"
            aria-hidden="true"
            :title="`${d_words.tl_italic} (ctrl+i)`"
        ></button>
        <!-- 下划线 -->
        <button
            :disabled="!editable"
            type="button"
            v-if="toolbars.underline"
            @click="$clicks('underline')"
            class="op-icon fa fa-mavon-underline"
            :title="`${d_words.tl_underline} (ctrl+u)`"
            aria-hidden="true"
        ></button>
        <!-- 删除线 -->
        <button
            :disabled="!editable"
            type="button"
            v-if="toolbars.strikethrough"
            @click="$clicks('strikethrough')"
            class="op-icon fa fa-mavon-strikethrough"
            :title="`${d_words.tl_strikethrough} (ctrl+shift+d)`"
            aria-hidden="true"
        ></button>
        <!-- 标记色 -->
        <button
            :disabled="!editable"
            type="button"
            v-if="toolbars.mark"
            @click="$clicks('mark')"
            class="op-icon fa fa-mavon-thumb-tack"
            :title="`${d_words.tl_mark} (ctrl+m)`"
            aria-hidden="true"
        ></button>
        <!-- 上标 -->
        <button
            :disabled="!editable"
            type="button"
            v-if="toolbars.superscript"
            @click="$clicks('superscript')"
            class="op-icon fa fa-mavon-superscript"
            aria-hidden="true"
            :title="`${d_words.tl_superscript} (ctrl+alt+s)`"
        ></button>
        <!-- 下标 -->
        <button
            :disabled="!editable"
            type="button"
            v-if="toolbars.subscript"
            @click="$clicks('subscript')"
            class="op-icon fa fa-mavon-subscript"
            aria-hidden="true"
            :title="`${d_words.tl_subscript} (ctrl+shift+s)`"
        ></button>

        <span class="op-icon-divider"></span>

        <!-- 左对齐 -->
        <button
            :disabled="!editable"
            type="button"
            v-if="toolbars.alignleft"
            @click="$clicks('alignleft')"
            class="op-icon fa fa-mavon-align-left"
            aria-hidden="true"
            :title="`${d_words.tl_alignleft} (ctrl+l)`"
        ></button>
        <!-- 居中对齐 -->
        <button
            :disabled="!editable"
            type="button"
            v-if="toolbars.aligncenter"
            @click="$clicks('aligncenter')"
            class="op-icon fa fa-mavon-align-center"
            aria-hidden="true"
            :title="`${d_words.tl_aligncenter} (ctrl+e)`"
        ></button>
        <!-- 右对齐 -->
        <button
            :disabled="!editable"
            type="button"
            v-if="toolbars.alignright"
            @click="$clicks('alignright')"
            class="op-icon fa fa-mavon-align-right"
            aria-hidden="true"
            :title="`${d_words.tl_alignright} (ctrl+r)`"
        ></button>
        <!-- 无序列表 -->
        <button :disabled="!editable" type="button" v-if="toolbars.ul" @click="$clicks('ul')" class="op-icon fa fa-mavon-list-ul" aria-hidden="true" :title="`${d_words.tl_ul} (ctrl+alt+u)`"></button>
        <!-- 有序列表 -->
        <button :disabled="!editable" type="button" v-if="toolbars.ol" @click="$clicks('ol')" class="op-icon fa fa-mavon-list-ol" aria-hidden="true" :title="`${d_words.tl_ol} (ctrl+o)`"></button>
        <!-- 表格 -->
        <button
            :disabled="!editable"
            type="button"
            v-if="toolbars.table"
            @click="$clicks('table')"
            class="op-icon fa fa-mavon-table"
            aria-hidden="true"
            :title="`${d_words.tl_table} (ctrl+alt+t)`"
        ></button>
        <!-- 引用 -->
        <button
            :disabled="!editable"
            type="button"
            v-if="toolbars.quote"
            @click="$clicks('quote')"
            class="op-icon fa fa-mavon-quote-left"
            aria-hidden="true"
            :title="`${d_words.tl_quote} (ctrl+q)`"
        ></button>
        <!-- 代码 -->
        <button
            :disabled="!editable"
            type="button"
            v-if="toolbars.code"
            @click="$clicks('code')"
            class="op-icon fa fa-mavon-code"
            aria-hidden="true"
            :title="`${d_words.tl_code} (ctrl+alt+c)`"
        ></button>

        <span class="op-icon-divider"></span>

        <!-- 上传图片 -->
        <div
            :disabled="!editable"
            :class="{ selected: s_img_dropdown_open }"
            type="button"
            v-if="toolbars.imagelink"
            @mouseleave="$mouseleave_img_dropdown"
            @mouseenter="$mouseenter_img_dropdown"
            class="op-icon fa fa-mavon-picture-o dropdown dropdown-wrapper"
            aria-hidden="true"
        >
            <transition name="fade">
                <div class="op-image popup-dropdown" :class="{ transition: transition }" v-show="s_img_dropdown_open" @mouseleave="$mouseleave_img_dropdown" @mouseenter="$mouseenter_img_dropdown">
                    <div class="dropdown-item" @click.stop="$toggle_imgLinkAdd('imagelink')">
                        <span>{{ d_words.tl_image }}</span>
                    </div>
                    <div class="dropdown-item" style="overflow: hidden">
                        <input type="file" accept="image/gif,image/jpeg,image/jpg,image/png,image/svg" @change="$imgAdd($event)" multiple="multiple" />{{ d_words.tl_upload }}
                    </div>

                    <div v-for="(item, index) in img_file" v-if="item && item[1]" class="dropdown-item dropdown-images" :title="item[1].name" :key="index" @click.stop="$imgFileListClick(index)">
                        <span>{{ item[1].name }}</span>
                        <button slot="right" type="button" @click.stop="$imgDel(index)" class="op-icon fa fa-mavon-times" aria-hidden="true" :title="d_words.tl_upload_remove"></button>
                        <!-- 缩略图展示 -->
                        <img class="image-show" :class="{ transition: transition }" :src="item[1].miniurl" alt="none" />
                    </div>
                </div>
            </transition>
        </div>
        <!-- 添加image链接 -->
        <transition name="fade">
            <div class="add-image-link-wrapper" v-if="s_img_link_open">
                <div class="add-image-link">
                    <i @click.stop.prevent="s_img_link_open = false" class="fa fa-mavon-times" aria-hidden="true"></i>
                    <h3 class="title">
                        {{ link_type == "link" ? d_words.tl_popup_link_title : d_words.tl_popup_img_link_title }}
                    </h3>
                    <div class="link-text input-wrapper">
                        <input ref="linkTextInput" type="text" v-model="link_text" :placeholder="link_type == 'link' ? d_words.tl_popup_link_text : d_words.tl_popup_img_link_text" />
                    </div>
                    <div class="link-addr input-wrapper">
                        <input type="text" v-model="link_addr" :placeholder="link_type == 'link' ? d_words.tl_popup_link_addr : d_words.tl_popup_img_link_addr" />
                    </div>
                    <div class="add-image-buttons">
                        <div class="u-op-btn cancel" @click.stop="s_img_link_open = false">
                            {{ d_words.tl_popup_link_cancel }}
                        </div>
                        <div class="u-op-btn sure" @click.stop="$imgLinkAdd()">
                            {{ d_words.tl_popup_link_sure }}
                        </div>
                    </div>
                </div>
            </div>
        </transition>
        <!-- 上传文件 -->
        <slot name="left-toolbar-after" />

        <!-- 撤销 -->
        <button type="button" v-if="toolbars.undo" @click="$clicks('undo')" class="op-icon fa fa-mavon-undo" aria-hidden="true" :title="`${d_words.tl_undo} (ctrl+z)`"></button>
        <!-- 重做 -->
        <button type="button" v-if="toolbars.redo" @click="$clicks('redo')" class="op-icon fa fa-mavon-repeat" aria-hidden="true" :title="`${d_words.tl_redo} (ctrl+y)`"></button>
        <!-- 清空 -->
        <button type="button" v-if="toolbars.trash" @click="$clicks('trash')" class="op-icon fa fa-mavon-trash-o" aria-hidden="true" :title="`${d_words.tl_trash} (ctrl+breakspace)`"></button>
        <!-- 保存 -->
        <button type="button" v-if="toolbars.save" @click="$clicks('save')" class="op-icon fa fa-mavon-floppy-o" aria-hidden="true" :title="`${d_words.tl_save} (ctrl+s)`"></button>

    </div>
</template>
<script type="text/ecmascript-6">
export default {
    name: "s-md-toolbar-left",
    props: {
        editable: {
            // 是否开启编辑
            type: Boolean,
            default: true,
        },
        transition: {
            type: Boolean,
            default: true,
        },
        toolbars: {
            // 工具栏
            type: Object,
            required: true,
        },
        d_words: {
            type: Object,
            required: true,
        },
        image_filter: {
            type: Function,
            default: null,
        },
    },
    data() {
        return {
            // [index, file]
            img_file: [[0, null]],
            img_timer: null,
            header_timer: null,
            s_img_dropdown_open: false,
            s_header_dropdown_open: false,
            s_img_link_open: false,
            trigger: null,
            num: 0,
            link_text: "",
            link_addr: "",
            link_type: "link",
        };
    },
    methods: {
        $imgLinkAdd() {
            this.$emit(
                "toolbar_left_addlink",
                this.link_type,
                this.link_text,
                this.link_addr
            );
            this.s_img_link_open = false;
        },
        $toggle_imgLinkAdd(type) {
            this.link_type = type;
            this.link_text = this.link_addr = "";
            this.s_img_link_open = true;
            this.$nextTick(() => {
                this.$refs.linkTextInput.focus();
            });
            this.s_img_dropdown_open = false;
        },
        $imgFileListClick(pos) {
            this.$emit("imgTouch", this.img_file[pos]);
        },
        $changeUrl(index, url) {
            this.img_file[index][0] = url;
        },
        $imgFileAdd($file) {
            // this.img_file[0][0] = this.num;
            // this.img_file[0][1] = $file;
            // this.img_file.unshift([(this.num + 1), null]);
            // this.num = this.num + 1;
            this.img_file.push([++this.num, $file]);
            this.$emit("imgAdd", this.num, $file);
            this.s_img_dropdown_open = false;
        },
        $imgFilesAdd($files) {
            // valid means if the image_filter exist.
            let valid = typeof this.image_filter === "function";
            for (let i = 0; i < $files.length; i++) {
                if (valid && this.image_filter($files[i]) === true) {
                    this.$imgFileAdd($files[i]);
                } else if (!valid && $files[i].type.match(/^image\//i)) {
                    this.$imgFileAdd($files[i]);
                }
            }
        },
        $imgAdd($e) {
            this.$imgFilesAdd($e.target.files);
            $e.target.value = ""; // 初始化
        },
        $imgDel(pos) {
            this.$emit("imgDel", this.img_file[pos]);
            this.img_file.splice(pos, 1);
            this.num--;

            this.s_img_dropdown_open = false;
        },
        isEqualName(filename, pos) {
            if (this.img_file[pos][1]) {
                if (
                    this.img_file[pos][1].name === filename ||
                    this.img_file[pos][1]._name === filename
                ) {
                    return true;
                }
            }
            return false;
        },
        $imgDelByFilename(filename) {
            var pos = 0;
            while (this.img_file.length > pos) {
                if (
                    this.img_file[pos][1] === filename ||
                    this.isEqualName(filename, pos)
                ) {
                    this.$imgDel(pos);
                    return true;
                }
                pos += 1;
            }
            return false;
        },
        $imgAddByFilename(filename, $file) {
            for (var i = 0; i < this.img_file.length; i++) {
                if (this.img_file[i][0] === filename) return false;
            }
            this.img_file[0][0] = filename;
            this.img_file[0][1] = $file;
            this.img_file[0][2] = filename;
            this.img_file.unshift(["./" + this.num, null]);
            this.$emit("imgAdd", this.img_file[1][0], $file, false);
            return true;
        },
        $imgAddByUrl(filename, $url) {
            for (var i = 0; i < this.img_file.length; i++) {
                if (this.img_file[i][0] === filename) return false;
            }
            this.img_file[0][0] = filename;
            this.img_file[0][1] = $url;
            this.img_file.unshift(["./" + this.num, null]);
            return true;
        },
        $imgUpdateByFilename(filename, $file) {
            for (var i = 0; i < this.img_file.length; i++) {
                if (
                    this.img_file[i][0] === filename ||
                    this.isEqualName(filename, i)
                ) {
                    this.img_file[i][1] = $file;
                    this.$emit("imgAdd", filename, $file, false);
                    return true;
                }
            }
            return false;
        },
        // 工具栏功能图标click-----------------
        $mouseenter_img_dropdown() {
            if (this.editable) {
                clearTimeout(this.img_timer);
                this.s_img_dropdown_open = true;
            }
        },
        $mouseleave_img_dropdown() {
            let vm = this;
            this.img_timer = setTimeout(function () {
                vm.s_img_dropdown_open = false;
            }, 200);
        },
        $mouseenter_header_dropdown() {
            if (this.editable) {
                clearTimeout(this.header_timer);
                this.s_header_dropdown_open = true;
            }
        },
        $mouseleave_header_dropdown() {
            let vm = this;
            this.header_timer = setTimeout(function () {
                vm.s_header_dropdown_open = false;
            }, 200);
        },
        $clicks(_type) {
            // 让父节点来绑定事件并
            if (this.editable) {
                this.$emit("toolbar_left_click", _type);
            }
        },
        $click_header(_type) {
            // 让父节点来绑定事件并
            this.$emit("toolbar_left_click", _type);
            this.s_header_dropdown_open = false;
        },
        handleClose(e) {
            this.s_img_dropdown_open = false;
        },
    },
    watch: {
        s_img_link_open(newVlaue) {
            // fix issue #644
            this.$parent.$el.style.zIndex = newVlaue ? 1501 : 1500;
        },
    },
};
</script>
