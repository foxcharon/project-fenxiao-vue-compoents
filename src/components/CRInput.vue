<template>
  <div 
    @mouseenter="hovering = true"
    @mouseleave="hovering = false"
    :class="'cr-input ' + (gray ? ' gray' : '')"
  >
    <template v-if="type !== 'textarea'">
      <input
        :tabindex="tabindex"        
        :class="'cr-input__inner ' + (large ? ' large' : '') + (huge ? ' huge' : '') + (center ? ' center' : '') + (gray ? ' gray' : '') + (transparent ? ' transparent' : '') + (leftPadding ? ' left-padding' : '')"
        v-bind="$attrs"
        :type="type"
        :disabled="inputDisabled"
        :autocomplete="autoComplete"
        :value="currentValue"
        ref="input"
        @compositionstart="handleComposition"
        @compositionupdate="handleComposition"
        @compositionend="handleComposition"
        @input="handleInput"
        @focus="handleFocus"
        @blur="handleBlur"
        @change="handleChange"
        :aria-label="label"
      >
      <div :class="'cr-input__after ' + (redSearch ? ' red-serach' : '')" v-if="haveButton === true" @click="search">
       
      </div>
      <div :class="'cr-input__afterword' + (wordGray ? ' word-gray' : '')" v-if="wordButton !== ''" @click="getmcode">
        <p>{{ wordButton }}</p>
      </div>
      <div class="cr-input__afterarrow" v-if="arrow === true">
        
      </div>
      <slot v-if="canInsert === true"></slot>
    </template>
    <textarea
      v-else
      :tabindex="tabindex"
      class="el-textarea__inner"
      :value="currentValue"
      @compositionstart="handleComposition"
      @compositionupdate="handleComposition"
      @compositionend="handleComposition"
      @input="handleInput"
      ref="textarea"
      v-bind="$attrs"
      :disabled="inputDisabled"
      
      @focus="handleFocus"
      @blur="handleBlur"
      @change="handleChange"
      :aria-label="label"
    >
    </textarea>
      
  </div>
</template>
<script>
  

  export default {
    name: 'CRInput',
    componentName: 'CRInput',

    data() {
      return {
        currentValue: this.value === undefined || this.value === null
          ? ''
          : this.value,
        textareaCalcStyle: {},
        prefixOffset: null,
        suffixOffset: null,
        hovering: false,
        focused: false,
        isOnComposition: false
      };
    },

    props: {
      value: [String, Number],
      size: String,
      resize: String,
      form: String,
      disabled: Boolean,
      type: {
        type: String,
        default: 'text'
      },
      wordButton: {
        type: String,
        default: ''
      },
      autosize: {
        type: [Boolean, Object],
        default: false
      },
      autoComplete: {
        type: String,
        default: 'off'
      },
      validateEvent: {
        type: Boolean,
        default: true
      },
      suffixIcon: String,
      prefixIcon: String,
      label: String,
      clearable: {
        type: Boolean,
        default: false
      },
      haveButton: {
        type: Boolean,
        default: false
      },
      center: {
        type: Boolean,
        default: false
      },
      large: {
        type: Boolean,
        default: false
      },
      gray: {
        type: Boolean,
        default: false
      },
      transparent: {
        type: Boolean,
        default: false
      },
      huge: {
        type: Boolean,
        default: false
      },
      arrow: {
        type: Boolean,
        default: false
      },
      wordGray: {
        type: Boolean,
        default: false
      },
      leftPadding: {
        type: Boolean,
        default: false
      },
      canInsert: {
        type: Boolean,
        default: false
      },
      canInsert: {
        type: Boolean,
        default: false
      },
      redSearch: {
        type: Boolean,
        default: false
      },
      tabindex: String
    },

    computed: {
      _elFormItemSize() {
        return (this.elFormItem || {}).elFormItemSize;
      },
      validateState() {
        return this.elFormItem ? this.elFormItem.validateState : '';
      },
      needStatusIcon() {
        return this.elForm ? this.elForm.statusIcon : false;
      },
      validateIcon() {
        return {
          validating: 'el-icon-loading',
          success: 'el-icon-circle-check',
          error: 'el-icon-circle-close'
        }[this.validateState];
      },
      textareaStyle() {
        return merge({}, this.textareaCalcStyle, { resize: this.resize });
      },
      inputSize() {
        return this.size || this._elFormItemSize || (this.$ELEMENT || {}).size;
      },
      inputDisabled() {
        return this.disabled || (this.elForm || {}).disabled;
      },
      isGroup() {
        return this.$slots.prepend || this.$slots.append;
      },
      showClear() {
        return this.clearable &&
          !this.disabled &&
          !this.readonly &&
          this.currentValue !== '' &&
          (this.focused || this.hovering);
      }
    },

    watch: {
      'value'(val, oldValue) {
        this.setCurrentValue(val);
      },
      'wordButton':
        function(){
          // console.log('wordButton')
        }
      
    },

    methods: {
      search(){
        // alert("???")
        this.$emit('search');
      },
      focus() {
        (this.$refs.input || this.$refs.textarea).focus();
      },
      blur() {
        (this.$refs.input || this.$refs.textarea).blur();
      },
      getMigratingConfig() {
        return {
          props: {
            'icon': 'icon is removed, use suffix-icon / prefix-icon instead.',
            'on-icon-click': 'on-icon-click is removed.'
          },
          events: {
            'click': 'click is removed.'
          }
        };
      },
      handleBlur(event) {
        this.focused = false;
        this.$emit('blur', event);
        
      },
      select() {
        (this.$refs.input || this.$refs.textarea).select();
      },
      resizeTextarea() {
        return
        if (this.$isServer) return;
        const { autosize, type } = this;
        if (type !== 'textarea') return;
        if (!autosize) {
          this.textareaCalcStyle = {
            minHeight: calcTextareaHeight(this.$refs.textarea).minHeight
          };
          return;
        }
        const minRows = autosize.minRows;
        const maxRows = autosize.maxRows;

        this.textareaCalcStyle = calcTextareaHeight(this.$refs.textarea, minRows, maxRows);
      },
      handleFocus(event) {
        this.focused = true;
        this.$emit('focus', event);
      },
      handleComposition(event) {
        if (event.type === 'compositionend') {
          this.isOnComposition = false;
          this.handleInput(event);
        } else {
          const text = event.target.value;
          const lastCharacter = text[text.length - 1] || '';
          this.isOnComposition = true
        }
      },
      handleInput(event) {
        if (this.isOnComposition) return;
        const value = event.target.value;
        this.$emit('input', value);
        this.setCurrentValue(value);
      },
      handleChange(event) {
        this.$emit('change', event.target.value);
      },
      setCurrentValue(value) {
        if (value === this.currentValue) return;
        this.$nextTick(_ => {
          this.resizeTextarea();
        });
        this.currentValue = value;
        
      },
      calcIconOffset(place) {
        const pendantMap = {
          'suf': 'append',
          'pre': 'prepend'
        };

        const pendant = pendantMap[place];

        if (this.$slots[pendant]) {
          return { transform: `translateX(${place === 'suf' ? '-' : ''}${this.$el.querySelector(`.el-input-group__${pendant}`).offsetWidth}px)` };
        }
      },
      clear() {
        this.$emit('input', '');
        this.$emit('change', '');
        this.$emit('clear');
        this.setCurrentValue('');
        this.focus();
      },
      getmcode(){
        this.$emit('getmcode', 'a');
      }
    },

    created() {
      this.$on('inputSelect', this.select);
    },

    mounted() {
      this.resizeTextarea();
      if (this.isGroup) {
        this.prefixOffset = this.calcIconOffset('pre');
        this.suffixOffset = this.calcIconOffset('suf');
      }
    }
  };
</script>

<style lang="less" scoped>
  @fs14:3.733vw;
  @fs15:0.9375rem;
  @red:#f80c53;
  @g1:#f0f0f0;
  @g2:#d9d9d9;
  @g3:#cccccc;
  @g4:#999999;

  .cr-input{

    position: relative;
    display: inline-flex;
    width: 100%;
    min-height: 8.667vw;
    &.gray{
      background: #e1e1e6;
      height: 2.8125rem;
    }
  
    .cr-input__inner{
      width: 100%;
      height: 8.667vw;
      line-height: 8.667vw;
      border:0;
      box-sizing: border-box;
      padding: 0 0 0 2.5vw;
      background: @g1;
      font-size: @fs14;
      color: #333;
      &.large{
        height: 2.8125rem;
        line-height: 2.8125rem;
        border-radius: 4px;
      }
      &.huge{
        height: 3.75rem;
        line-height: 3.75rem; 
        font-size: @fs15;
      }
      &.gray{
        background: transparent;
      }
      &.transparent{
        background: transparent;
      }
      &.left-padding{
        padding: 0 0 0 2.8125rem;
      }
      &.center{
        text-align: center;
        padding-left: 0;
      }

    }    
    input::placeholder {
      color: @g4;
    }
    .cr-input__after{
      background-image: url("../../assets/images/new/index_002.png");
      background-repeat: no-repeat;
      background-size: 40%;
      background-color: @g2;
      background-position: center center;
      width: 15%;
      height: 8.667vw;
      vertical-align: top;
      &.red-serach{
        background-color: @red;
      }
    }
    .cr-input__afterword{
      height: 100%;
      width: 30%;
      font-size: @fs14;
      display: inline-flex;
      justify-content: center;
      align-items: center;
      padding: 0 0.625rem 0 0;
      color: @red;      
      &.word-gray{
        color: @g4;
      }
    }
    .cr-input__afterarrow{
      position: absolute;
      width: 0.40625rem;
      height: 0.625rem;          
      top:50%;
      right: 0;
      background-image: url("../../assets/images/new/ordersubmit_001.png");
      background-repeat: no-repeat;
      background-size: 100%;
    }
    .el-textarea__inner{
      display:block;
      resize:none;
      padding:5px 15px;
      line-height:1.5;
      box-sizing:border-box;
      width:100%;
      font-size:@fs15;
      padding: 0.625rem;
      border:0;
      height: 7.5rem;
    }
  }
  
</style>
