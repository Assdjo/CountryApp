<script setup>



import { ref } from 'vue'
let id = ref(0)
let loading = ref(false)

// const allcountry = ref([
//     {id: id++, Nom : 'Bénin'},
//     {id: id++, Nom : 'Bénin'},
//     {id: id++, Nom : 'Bénin'},
//     {id: id++, Nom : 'Bénin'},
//     {id: id++, Nom : 'Bénin'},
//     {id: id++, Nom : 'Bénin'},
//     {id: id++, Nom : 'Bénin'},
//     {id: id++, Nom : 'Bénin'},
//     {id: id++, Nom : 'Bénin'},
//     {id: id++, Nom : 'Bénin'},
//     {id: id++, Nom : 'Bénin'},
//     {id: id++, Nom : 'Bénin'},
//     {id: id++, Nom : 'Bénin'},
//     {id: id++, Nom : 'Bénin'},
//     {id: id++, Nom : 'Bénin'}
// ]);

let country = ref([])
const url = 'https://restcountries.com/v3.1/all'

async function fetchCountry() {
  const response = await fetch(url)
  country.value = await response.json()
  if (country.value.length>0) {
    loading.value = true
  }
  console.log(country.value)
}


// function fecthCountry() {
//     try {
//         country.value = fetch(url).then(
//     (response)=> console.log(response.json())
// )
//     } catch (error) {
//         console.log(error)
//     }
// }

fetchCountry()
// onMounted (() => {
//     fetchCountry()
// })


</script>
<template>
  <div v-if = "!loading">
    <p>Chargement en cours</p>
  </div>
 <div v-else>
  <img class="drapeau" :src="country[id]?.flags.png" :alt="country[id]?.flags.alt" />
  <header>
    <h1>{{ country[id]?.name.official }}</h1>
  </header>

  <main>
    <article class="list">
      <ul>
        <h2>liste des pays</h2>
        <li v-for="(all, index) in country" :key="index">
          <a href="#" @click="(() => id = index)">{{ all.name.common }}</a>
        </li>
      </ul>
    </article>
    <article class="description">
      <p><b>capitale :</b> {{ country[id]?.capital.join('') }}</p>
      <!-- <p><b>Langue :</b> {{ Object.values(country[id]?.languages)[id] }}</p>-->
      <!-- <p><b>Monnaie :</b><br> {{  Object.values(allContries[id]?.currencies)[0]?.name }}  {{Object.values(allContries[id]?.currencies)[0]?.symbol}} </p>   -->
    <p><b> Continent:</b> {{ country[id]?.continents.join('')}}</p>
    <p><b> Sous-région:</b> {{ country[id]?.subregion}}</p>
    <p><b> Emblème:</b> </p>
    <img class="embleme" :src="country[id]?.coatOfArms.png" :alt="country[id]?.flags.alt" />
    
      
     
      {{ console.log( country[id]) }}
    </article>
    <article class="other">
        <h2>Autres informations</h2>
      
      <p><b>Population :</b> {{ country[id]?.population }}</p>
      
    </article>
    <article class="apropos">
      <p>
        à propos
      </p>
      <p>
        ...
      </p>
    </article>
    <article class="Infogenerale">
      <p>
        Information générale
      </p>
      <p>
        ...
      </p>
    </article>
  </main>
  <footer></footer>
 </div>
</template>
<style>
body {
  margin: 0;
  padding: 0;
  background-color: rgb(231, 229, 229);
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial,
    sans-serif;
}

header {
background: rgb(91, 255, 0);
background: linear-gradient(
90deg,
rgba(91, 255, 0, 1) 0%,
rgba(36, 105, 1, 1) 41%,
rgba(36, 105, 1, 1) 100%
);
text-align: center;
/_ position: absolute; _/
width: 100%;
height: 200px;
}

h1 {
position: relative;
top: 70px;
color: white;
}

.drapeau {
position: absolute;
left: 200px;
top: 130px;
border-radius: 20px;
}

ul {
padding: 0;
}

.list {
margin-top: 150px;
height: 400px;
width: 500px;
overflow: scroll;
background-color: white;
grid-area: list;
margin-inline: 20px;
padding: 10px;
}

li {
list-style: none;
padding: 5px;
font-weight: bold;
}

main {
display: grid;
grid-template-areas:
'list descrip other'
'list apropos apropos'
'list Infogenerale Infogenerale';
gap: 20px;
}

.description {
grid-area: descrip;
background-color: white;
margin-left: 30px;
margin-top: 20px;
width: 80%;
height: 500px;
padding: 10px;
}

.embleme {
width: 200px;
}

.other {
grid-area: other;
background-color: white;
padding: 10px;
margin-top: 20px;
height: 500px;
width: 80%;
}

.apropos {
grid-area: apropos;
background-color: white;
padding: 10px;
margin-left: 30px;
width: 88%;
}
.Infogenerale {
grid-area: Infogenerale;
background-color: white;
padding: 10px;
margin-left: 30px;
width: 88%;
}

a {
text-decoration: none;
color: rgb(82, 82, 82);
}
</style>
