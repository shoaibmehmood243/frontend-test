<template>
  <div class="page-selector">
    <div class="select-all">
      <label>
        <span>Select All</span>
        <input type="checkbox" v-model="selectAll" @change="toggleAll" />
      </label>
    </div>
    <div class="divider"></div>
    <div class="page-list">
      <div v-for="page in pages" :key="page.id" class="page-item">
        <label>
          <span>{{ page.name }}</span>
          <input
            type="checkbox"
            :id="page.id"
            v-model="page.selected"
            @change="updateSelectAll"
          />
        </label>
      </div>
    </div>
    <div class="divider"></div>
    <div>
      <button @click="showSelectedPages">Done</button>
    </div>
  </div>
</template>

<script>
import { ref, reactive, computed } from "vue";

export default {
  name: "PageSelector",
  setup() {
    const pages = reactive([
      { id: 1, name: "Page 1", selected: false },
      { id: 2, name: "Page 2", selected: false },
      { id: 3, name: "Page 3", selected: false },
      { id: 4, name: "Page 4", selected: false },
    ]);

    const selectAll = ref(false);

    const toggleAll = () => {
      pages.forEach((page) => (page.selected = selectAll.value));
    };

    const updateSelectAll = () => {
      selectAll.value = pages.every((page) => page.selected);
    };

    const selectedPages = computed(() => {
      return pages.filter((page) => page.selected);
    });

    const showSelectedPages = () => {
      const selected = selectedPages.value;
      if (selected.length === 0) {
        alert("No pages selected");
      } else {
        const pageNames = selected.map((page) => page.name).join(", ");
        alert(`Selected pages: ${pageNames}`);
      }
    };

    return {
      pages,
      selectAll,
      toggleAll,
      updateSelectAll,
      selectedPages,
      showSelectedPages,
    };
  },
};
</script>

<style scoped>
.page-selector {
  max-width: 370px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #eeeeee;
  box-shadow: 0px 8px 15px 0px #1414141f;
  border-radius: 6px;
}

.select-all {
  margin-bottom: 10px;
}

.divider {
  margin: 20px 0;
  height: 0.7px;
  background: #cdcdcd;
}

.page-list {
  display: flex;
  flex-direction: column;
}

.page-item {
  margin-bottom: 15px;
}

label {
  display: flex;
  align-items: center;
  justify-content: space-between;
  cursor: pointer;
}

span {
  font-size: 14px;
  font-weight: 400;
  line-height: 18.2px;
  text-align: left;
  color: #1f2128;
}

input[type="checkbox"] {
  width: 20px;
  height: 20px;
  border: 1px solid #bdbdbd;
  border-radius: 6px;
  outline: none;
  cursor: pointer;
}

input[type="checkbox"]:checked {
  accent-color: #2469f6;
}

button {
  width: 100%;
  background: #ffce22;
  padding: 10px 20px;
  border-radius: 4px;
  border: none;
  outline: none;
  cursor: pointer;
  font-size: 14px;
  font-weight: 600;
  color: #1f2128;
}

button:hover {
  background: #ffd74a;
}
</style>
