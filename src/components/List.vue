<template>
    <div v-for="item in list" :key="item.id" class="card-item" @click="setValue(item)">
        {{ item.name }}
    </div>
</template>

<script>
import { ref } from 'vue'

export default {
    props: {
        list: {
            type: Array,
            default: () => [],
            required: true
        }
    },
    emits:['setValue'],
    setup(props, { emit }) {
        const list = ref(props.list)

        const setValue = (item) => emit('setValue', item)

        return {
            list,
            setValue
        }
    }
}
</script>

<style lang="scss">
.card-item {
    border: 2px solid #f5f5f5;
    border-radius: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #f5f5f5;
    margin-right: .5rem;
    margin-bottom: .5rem;
    width: 80px;
    height: 80px;
    transition: .5 ease-in-out;
    cursor: pointer;

    &:hover {
        background: rgba(0, 0, 0, .6);
    }

    &--large {
        width: 200px;
        height: 200px;
        margin: 1rem;
        margin-bottom: 4rem;
    }
}
</style>