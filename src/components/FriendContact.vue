<template>
  <li>
    <h2>{{ firstName }} {{ isFavorite === true ? "(Favorite)":""  }}</h2>
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
    <br />
    <button :style="{marginTop:'1rem'}" @click="deleteFriend" >Delete</button>
  </li>
</template>

<script>
export default {
  name: "FriendContact",
  // props: [ "firstName", "phoneNumber", "emailAddress","isFavorite" ],
  props:{
    id:{
      type: String,
      required: true
    },
    firstName:{
      type:String,
      required:true
    },
    phoneNumber:{
      type:String,
      required:true
    },
    emailAddress:{
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
   emits:["toggle-favorite","delete-friend"],
/*   emits:{
    "toggle-favorite":function(id){
      if(id){
        return true;
      }else{
        console.warn("Id is missing!");
        return false;
      }
    }
  } */
  data() {
    return {
      detailsAreVisible: false,
      

    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFavorite(){
      this.$emit("toggle-favorite",this.id)
    },
    deleteFriend(){
      this.$emit("delete-friend",this.id)
    }
  }
};
</script>