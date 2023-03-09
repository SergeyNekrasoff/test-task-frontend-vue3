
<template>
  <main class="container">
    <div class="user-items">
        <div class="user-items__selected">
          <template v-if="getLengthSelectedList > 0">
            <div class="user-items__list">
              <list :list="selectedItems" @setValue="removeItem"></list>
            </div>
            <div class="user-items__value">
              <span>selected: {{ getLengthSelectedList }}/{{ getLengthUserItemsList }}</span>
            </div>
          </template>
          <template v-else>
            <div class="empty-list">
              <span class="small-text">Список выбранных вещей пуст</span>
            </div>
          </template>
        </div>

      <template v-if="getLengthUserItemsList > 0">
        <div class="user-items__list user-items__list--bordered">
          <list :list="userItems" @setValue="addItem"></list>
        </div>
      </template>
    </div>

    <div class="set-items">
      <div class="set-items__current-item">
        <div v-if="currentItem?.name" class="card-item card-item--large" @click="removeCurrentItem">
          {{ currentItem.name }}
        </div>
        <div v-else class="card-item card-item--large">
          <span class="small-text">Выберите элемент ниже</span>
        </div>
      </div>

      <template v-if="getLengthSetItemsList > 0">
        <div class="set-items__list set-items__list--bordered">
          <list :list="setItems" @setValue="selectItem"></list>
        </div>
      </template>
    </div>
  </main>
</template>

<script>
import { ref, computed } from 'vue'
import List from '@/components/List.vue'

const LIMIT_ITEMS_LENGTH = 6

export default {
  components: {
    List
  },
  setup() {
    const userItems = ref([
        {
            "id": 1,
            "name": "Shoes 1"
        },
        {
            "id": 2,
            "name": "Shoes 2"
        },
        {
            "id": 3,
            "name": "Shoes 3"
        },
        {
            "id": 4,
            "name": "Shoes 4"
        },
        {
            "id": 5,
            "name": "T-shirt 1"
        },
        {
            "id": 6,
            "name": "T-shirt 2"
        },
        {
            "id": 7,
            "name": "T-shirt 3"
        },
        {
            "id": 8,
            "name": "T-shirt 4"
        }
    ])

    const setItems = ref([
      {
          "id": 11,
          "name": "Jacket 1"
      },
      {
          "id": 12,
          "name": "Jacket 2"
      },
      {
          "id": 13,
          "name": "Jacket 3"
      },
      {
          "id": 14,
          "name": "Jacket 4"
      },
      {
          "id": 15,
          "name": "Hoodie 1"
      },
      {
          "id": 16,
          "name": "Hoodie 2"
      },
      {
          "id": 17,
          "name": "Hoodie 3"
      },
      {
          "id": 18,
          "name": "Hoodie 4"
      }
    ])

    const selectedItems = ref([])

    const currentItem = ref(null)

    const addItem = (item) => {
      if (selectedItems.value.length === 0 
          || (selectedItems.value.find(el => el.id !== item.id) 
          && selectedItems.value.length < LIMIT_ITEMS_LENGTH))
      {
        selectedItems.value.push(item)
      }
    }

    const removeItem = (item) => {
      const index = selectedItems.value.findIndex(el => el.id === item.id)
      selectedItems.value.splice(index, 1)
    }

    const selectItem = (item) => currentItem.value = item

    const removeCurrentItem = () => currentItem.value = null

    const getLengthSelectedList = computed(() => selectedItems.value.length)
    const getLengthUserItemsList = computed(() => userItems.value.length)
    const getLengthSetItemsList = computed(() => setItems.value.length)

    return {
      userItems,
      setItems,
      selectedItems,
      addItem,
      removeItem,
      selectItem,
      currentItem,
      removeCurrentItem,
      getLengthSelectedList,
      getLengthUserItemsList,
      getLengthSetItemsList
    }
  }
}
</script>

<style lang="scss">
.container {
  height: 100vh;
}

.user-items,
.set-items {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  flex-wrap: nowrap;
  width: calc(50% - 2rem);
  height: 100%;
  margin: 1rem;

  &__list {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
    flex-wrap: wrap;
    width: 100%;
    margin-bottom: 2rem;

    &--bordered {
      border: 2px solid #f5f5f5;
      border-radius: 5px;
      padding: 1rem;
    }
  }
  
  .small-text {
    color: #828282;
  }
}

.set-items {
  &__current-item {
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    align-items: center;
    flex-wrap: nowrap;
    width: 100%;
  }

  .card-item {
    &--large {
      margin-right: 0;
    }
  }
}

.user-items {
  &__selected {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    flex-wrap: nowrap;
    border: 2px solid #f5f5f5;
    border-radius: 5px;
    padding: 1rem;
    margin: 1rem;
    margin-bottom: 4rem;
    width: 100%;
    min-height: 60px;
  }

  .empty-list {
    height: 165px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  &__value {
    font-size: 1.5rem;
    color: #fff;
    text-transform: uppercase;
  }
}
</style>
