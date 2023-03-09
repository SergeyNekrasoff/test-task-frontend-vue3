<template>
    <div v-for="item in list" :key="item.id" class="card-item" @click="setValue(item)">
        <span class="card-name">{{ item.name }}</span>
        <img class="card-img" :src="getImage(item.src)" />
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

        const getImage = (path) => {
            return new URL(`../assets/${path}`, import.meta.url).href
        }

        return {
            list,
            setValue,
            getImage
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
    overflow: hidden;

    &:hover {
        background: rgba(0, 0, 0, .6);

        .card-name {
            display: flex;
        }
    }

    &--large {
        width: 200px;
        height: 200px;
        margin: 1rem;
        margin-bottom: 4rem;
    }
}

.card-img {
    max-width: 100%;
    width: 100%;
    height: auto;
}

.card-name {
    display: none;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, .8);
    flex-direction: column;
    align-items: center;
    justify-content: center;
    z-index: 1;
}
</style>