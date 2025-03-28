<template>
  <section>
    <input type="text" v-model="data.filter" placeholder="Type something to filter the list" />
  </section>
  <section>
    <input type="text" v-model="data.newIngredient" placeholder="Title" />
    <button @click="add" @disabled="!data.newIngredient">Add</button>
  </section>
  <section>
    <template v-if="!data.ingredients.length">
      <h1>No ingredients found</h1>
    </template>
    <template v-else>
      <table>
        <thead>
          <tr>
            <th>Ingredient</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="ingredient in filteredIngredients" :key="ingredient">
            <td>{{ingredient}}</td>
            <td>
              <button @click="update(ingredient)">Update</button>
              <button @click="remove(ingredient)">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </template>
  </section>
</template>

<script>
import { reactive, computed } from "vue";
export default {
  setup() {
    const data = reactive({
      ingredients: [],
      filter: "",
      newIngredient: ""
    });
    const filteredIngredients = computed(() =>
      data.ingredients
        .filter(ingredient => !data.filter || ingredient.includes(data.filter))
        .sort((a, b) => (a > b ? 1 : a < b ? -1 : 0))
    );
    const add = ingredient => {
      if (
        !data.newIngredient ||
        data.ingredients.some(ingredient => ingredient === data.newIngredient)
      )
        return;
      data.ingredients = [...data.ingredients, data.newIngredient];
      data.newIngredient = "";
    };
    const update = ingredient => {
      data.newIngredient = ingredient;
      remove(ingredient);
    };
    const remove = ingredient =>
      (data.ingredients = data.ingredients.filter(
        filterIngredient => ingredient !== filterIngredient
      ));
    return {
      filteredIngredients,
      data,
      add,
      update,
      remove
    };
  }
};
</script>