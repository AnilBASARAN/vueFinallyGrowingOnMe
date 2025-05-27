<template>
  <li>
    <h2>{{ firstName }} {{ friendIsFavorite === true ? "(Favorite)":""  }}</h2>
    <button :style="{margin:'1rem'}" @click="toggleDetails">{{ detailsAreVisible ? 'Hide' : 'Show' }} Details</button>
    <br />
    <button @click="toggleFavorite"> Toggle Favorite</button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Phone:</strong>
        {{ phoneNumber }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ emailAddress }}
      </li>
    </ul>
  </li>
</template>

<script>
export default {
  name: "FriendContact",
  // props: [ "firstName", "phoneNumber", "emailAddress","isFavorite" ],
  props:{
    firstName:{
      type:String,
      required:true
    },
    phoneNumber:{
      type:String,
      required:true
    },
    isFavorite:{
      type:Boolean,
      required:false,
      default:false,
      validator:function(value){
        return value === true || value === false;
      },

/*      validator(value) {
      // only allow these three strings
      return ["small", "medium", "large"].includes(value);
    } */
    }
  },
  data() {
    return {
      detailsAreVisible: false,
      friendIsFavorite:this.isFavorite

    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFavorite(){
      this.friendIsFavorite = !this.friendIsFavorite;
    }
  }
};
</script>