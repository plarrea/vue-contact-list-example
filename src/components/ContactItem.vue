<template>
  <li>
    <h2>{{ name }} {{ isFavorite === "1" ? "(Favorite)" : "" }}</h2>
    <button @click="togleFavorite">Toggle Favorite</button>
    <button @click="togleDetails">
      {{ detailsAreVisible ? "Hide" : "Show" }} Details
    </button>
    <ul v-if="detailsAreVisible">
      <li><strong>Phone:</strong>{{ phoneNumber }}</li>
      <li><strong>Email:</strong>{{ emailAddress }}</li>
    </ul>
  </li>
</template>

<script>
export default {
  name: "ContactItem",
  props: {
    id: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    phoneNumber: {
      type: String,
      required: true,
    },
    emailAddress: {
      type: String,
      required: true,
    },
    isFavorite: {
      type: String,
      required: false,
      default: "0",
      validator: (value) => {
        return value === "1" || value === "0";
      },
    },
  },
  emits: {
    "toggle-favorite": (id) => {
      if (id) {
        return true;
      } else {
        console.warn("Id is missing");
        return false;
      }
    },
  },
  data() {
    return {
      detailsAreVisible: false,
    };
  },
  methods: {
    togleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    togleFavorite() {
      this.$emit("toggle-favorite", this.id);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
