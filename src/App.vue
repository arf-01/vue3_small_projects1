<script setup>

import{ref} from "vue"



const showmodal =ref(false);
const newNote=ref("");
const Notes=ref([]);

function getRandomColor() {
 const  color = "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  return color;
}

const addNote =() =>{


Notes.value.push({

  text:newNote.value,
  date: new Date(),
  backgroundcolor: getRandomColor()

});

showmodal.value=false;
newNote.value="";

}






</script>


<template>
  <main>
    <div v-if="showmodal" class="overlay">
      <div class="modal">
        <h2>Add a Note</h2>
        <textarea v-model="newNote " class="note-input" placeholder="Write your note here..."></textarea>
        <button class="submit-btn " @click="addNote">Save</button>
      </div>
    </div> 
    <div class="container"> 
      <header>

     
        <div><h1>Notes</h1></div>
        <div><button @click="showmodal=true">+</button></div> 
      </header>

      <div class="cards-container">
        <div v-for="note in Notes" class="card" :style="{ backgroundColor: note.backgroundcolor }">

          <p class="main-text">{{note.text}}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>

      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
  width: 100vw;

}

.container {
  max-width: 1000px; /* Use max-width for responsiveness */
  width: 90%; /* Allow it to shrink on smaller screens */
  padding: 20px; /* Increased padding for more space */
  position: relative;
  background-color: rgba(173, 216, 230, 0.8); /* Use a soft aqua color with slight transparency */
  height: 700px;
  border-radius: 10px; /* Rounded corners */
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2); /* Subtle shadow for depth */
  overflow: hidden; /* Hide overflow for a cleaner look */
  margin:0 auto;
}


header {
  display: flex; 
  flex-direction: row; 
  justify-content: space-between; 
  align-items: center;  
}

h1 {
  font-weight: bold;
  font-size: 75px;
  color: black;
}

button {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50px;
  width: 50px;
  border-radius: 100%;
  background-color: black;
  color: white;
  font-size: 30px;
}

.card {
  width: 200px;
  height: 200px;
  background-color: rgb(237, 182, 44);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin: 10px;
}

.date {
  font-size: 12.5px;
  font-weight: bold;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
}

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 10; 
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  width: 300px; /* Adjust width as needed */
}

.note-input {
  width: 100%;
  height: 100px;
  margin: 10px 0;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.submit-btn {
  background-color: black;
  color: white;
  padding: 10px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: small;
}

.submit-btn:hover {
  background-color: darkgray; /* Change color on hover */
}
</style>
