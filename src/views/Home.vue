<template>
  <div class="home">
    <h1>Vue State Counter</h1>

    <!-- <p class="count">{{ store.state.count }}</p> -->
    <p class="count">{{ count }}</p>

    <!-- <p>Count Tripled {{ store.getters.tripleCount() }}</p> -->
    <p>Count Tripled {{ tripleCount }}</p>

    <div class="change-count">
      <i @click="increase" class="fal fa-plus"></i>
      <i @click="decrease" class="fal fa-minus"></i>
    </div>

    <div class="cod">
      <h1>Color of the day:</h1>

      <!-- <p>{{store.state.color}}</p>

      <input type="text" name="color" v-model="store.state.color" /> -->

      <p>{{ color }}</p>

      <input type="text" name="color" v-model="color"/>
    </div>
  </div>
</template>

<script>
import { computed } from "vue";
import store from "../store/index";
export default {
  name: "Home",
  components: {},
  setup() {
    //const count = ref(0);
    const count = computed(() => store.state.count);
    
    const tripleCount = computed(() => store.getters.tripleCount());

    const increase = () => {
      // count.value++;
      store.mutations.increase();
    };

    const decrease = () => {
      // count.value--;
      store.mutations.decrease();
    };

    const color = computed({
      get() {
        return store.state.color;
      },
      set(value) {
        store.mutations.setColor(value);
      }
    });

    return { count, increase, decrease, color, tripleCount, store };
  },
};
</script>

<style lang="scss" scoped>
h1 {
  margin-top: 16px;
  text-align: center;
}

.count {
  margin-top: 32px;
  font-size: 60px;
  text-align: center;
}

.change-count {
  margin: 32px 0;
  display: flex;
  justify-content: center;
  gap: 32px;

  i {
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background-color: #f1f1f1;
    font-size: 40px;
  }
}

.cod {
  display: flex;
  flex-direction: column;

  p {
    font-size: 32px;
    text-align: center;
  }

  input {
    margin: 16px 0;
    padding: 6px;

    &:focus {
      outline: none;
    }
  }
}
</style>
