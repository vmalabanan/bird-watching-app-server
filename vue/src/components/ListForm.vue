<template>
  <main id="list-form">
    <span>Create a List</span>
    <form v-on:submit.prevent="createList">
      <input
        id="create-list"
        type="text"
        size="50"
        placeholder="Add a list name"
        required
        v-model="list.listName"
      />
      <input type="submit" />
    </form>
  </main>
</template>

<script>
import listService from "../services/ListService";
export default {
  data() {
    return {
      list: {
        // userId is handled in the backend -- we are passing in zero for now
        userId: 0,
        error:''
      },
    };
  },
  methods: {
    createList() {
      listService
        .createList(this.list)
        .then((response) => {
          if (response.status == 201) {
            this.$store.commit("ADD_LIST", response.data);
          }
          this.list = {}; // this clears out the form field
        })
        .catch((err) => {
          this.error=err + " problem creating list!";
        });
    },
  },
};
</script>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  align-items: center;
}
form {
  display: flex;
  padding-bottom: 10px;
}
 input {
  padding: 8px;
  border-radius: 8px;
  font-size: 1.2rem;
  border: 1px solid #011627;
  border-left: 5px solid #FF9F1C;
  border-right: 5px solid #FF9F1C;
} 
 input[type="submit"] {
  margin-left: 7px;
  border: 1px solid #011627;
  background-color: #E71D36;
  font-size: 1rem;
  font-weight: bold;
  border-radius: 8px;
  border-left: 5px solid #FF9F1C;
  border-right: 5px solid #FF9F1C;
} 
span {
  margin-top: 35px;
  margin-bottom: 35px;
  font-size: 1.8rem;
  font-weight: bold;
}
</style>