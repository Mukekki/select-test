<template>
    <div class="drop-down-list" :class="listClasses">
        <slot></slot>
        <div class="head" @click="listToggle()" :class="{'-active': listIsOpen}">
            <slot name="selected"></slot>
            <svg width="11" height="6" viewBox="0 0 11 6" fill="none" xmlns="http://www.w3.org/2000/svg"
            :class="{'-active': listIsOpen}">
                <path d="M1 5L5.5 1L10 5" stroke="#001A54"/>
            </svg>
        </div>
        <div class="list" @click="listClose();">
            <div class="option" v-for="(name, code) of array" :key="code"
            @click="changeValue(code)">
                <slot :name="code"></slot>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'w-select',
    data() {
        return {
            listIsOpen: false,
            current: '',
        }
    },
    props: {
        array: [Array,Object],
        value: {
            type: String,
        }
    },
    model: {
        prop: 'value',
        event: 'change'
    },
    computed: {
        listClasses() {
            return {
                '-active': this.listIsOpen
            }
        }
    },
    methods: {
        listToggle() {
            this.listIsOpen = !this.listIsOpen
        },
        listClose() {
            this.listIsOpen = false
        },
        changeValue(code) {
            this.$emit('change', code)
        }
    }
}
</script>

<style lang="less" scoped>
.drop-down-list {
    font-weight: 400;
    font-size: 14px;
    line-height: 144%;
    position: relative;

    > .head {
        margin-top: 6px;
        height: 50px;
        border: 1px solid rgb(10, 10, 80);
        box-sizing: border-box;
        border-radius: 10px;
        position: relative;
        padding: 15px 16px;
        font-weight: 500;
        background-color: #fff;
        transition: all 0.4s;

        svg {
            position: absolute;
            right: 17px;
            bottom: 22px;
            transform: scale(-1);
            transition: all 0.4s;

            
        }
        svg.-active {
            transform: scale(1);
            position: absolute;
            right: 17px;
            bottom: 22px;
        }

        &.-active {
            border: 1px solid rgb(63, 19, 83);
        }
    }

    > .list {
        position: absolute;
        left: 0px;
        top: 76px;
        width: 100%;
        background-color: #fff;
        border-radius: 8px;
        max-height: 315px;
        overflow: auto;
        filter: drop-shadow(0px 20px 40px #000);
        opacity: 0;
        transform: translateY(-50%) rotate3d(1, 0, 0, 90deg);
        transition: all 0.4s;
        z-index: 1;

        .option {
            padding: 10px 16px;
            transition: all 0.2s;
            cursor: pointer;

            &:hover {
                background-color: #F2F5F9;
            }
        }
    }

    &.-active {

        > .list {
            opacity: 1;
            transform: translateY(0px) rotate3d(0, 0, 0, 0deg);
        }
    }
}

.list::-webkit-scrollbar {
    width: 10px;
}

.list::-webkit-scrollbar-track {
    border-radius: 10px;
    margin: 5px 3px 5px 3px;
}

.list::-webkit-scrollbar-thumb {
    border-radius: 10px;
    background: var(--blue-link);
    border: 3px solid rgba(255, 255, 255, 1);
}


</style>
