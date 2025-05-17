 
<script setup>
import { ref } from "vue";
import NameCard from "../components/NameCard.vue";

const popularCities = [
  "New York",
  "Los Angeles",
  "Nyc",
  "Ny",
  "Chicago",
  "London",
  "Paris",
  "Tokyo",
  "Shanghai",
  "Beijing",
  "Sydney",
  "Dubai",
  "Singapore",
  "Hong Kong",
  "Barcelona",
  "Rome",
  "Istanbul",
  "Mumbai",
  "São Paulo",
  "Mexico City",
  "Moscow",
  "Toronto",
  "Berlin",
  "Bangkok",
  "Delhi",
  "Cairo",
  "Buenos Aires",
  "Kuala Lumpur",
  "Jakarta",
  "Lima",
  "Seoul",
  "Rio de Janeiro",
  "San Francisco",
  "Miami",
  "Madrid",
  "Amsterdam",
  "Dublin",
  "Vienna",
  "Zurich",
  "Lisbon",
  "Prague",
  "Budapest",
  "Warsaw",
  "Brussels",
  "Stockholm",
  "Helsinki",
  "Copenhagen",
  "Oslo",
  "Athens",
  "Edinburgh",
  "Munich",
  "Milan",
  "Venice",
  "Florence",
  "Nice",
  "Lyon",
  "Marseille",
  "Geneva",
  "Montreal",
  "Vancouver",
  "Melbourne",
  "Brisbane",
  "Perth",
  "Adelaide",
  "Auckland",
  "Wellington",
  "Cape Town",
  "Johannesburg",
  "Nairobi",
  "Lagos",
  "Casablanca",
  "Rabat",
  "Tunis",
  "Algiers",
  "Tehran",
  "Baghdad",
  "Riyadh",
  "Jeddah",
  "Mecca",
  "Medina",
  "Doha",
  "Abu Dhabi",
  "Manama",
  "Kuwait City",
  "Beirut",
  "Amman",
  "Damascus",
  "Jerusalem",
  "Tel Aviv",
  "Ankara",
  "Kyiv",
  "Bucharest",
  "Sofia",
  "Belgrade",
  "Sarajevo",
  "Zagreb",
  "Ljubljana",
  "Bratislava",
  "Vilnius",
  "Riga",
  "Tallinn",
  "Havana",
  "Santo Domingo",
  "San Juan",
  "Kingston",
  "Panama City",
  "San Salvador",
  "Guatemala City",
  "Managua",
  "San Jose",
  "Lima",
  "Santiago",
  "Quito",
  "La Paz",
  "Caracas",
  "Bogotá",
  "Lima",
  "Asunción",
  "Montevideo",
  "Buenos Aires",
  "Brasília",
  "Sao Paulo",
  "Rio de Janeiro",
  "Recife",
  "Salvador",
  "Fortaleza",
  "Porto Alegre",
  "Curitiba",
  "Manaus",
  "Belém",
  "Lagos",
  "Kinshasa",
  "Johannesburg",
  "Cape Town",
  "Durban",
  "Nairobi",
  "Cairo",
  "Alexandria",
  "Giza",
  "Casablanca",
  "Rabat",
  "Algiers",
  "Tunis",
  "Tripoli",
  "Addis Ababa",
  "Khartoum",
  "Accra",
  "Dakar",
  "Luanda",
  "Dar es Salaam",
  "Maputo",
  "Kampala",
  "Lusaka",
  "Harare",
  "Windhoek",
  "Pretoria",
  "Gaborone",
  "Antananarivo",
  "Port Louis",
  "Victoria",
  "Djibouti",
  "Nouakchott",
  "Bamako",
  "Ouagadougou",
  "Niamey",
  "N'Djamena",
  "Juba",
  "Yaoundé",
  "Libreville",
  "Brazzaville",
  "Kinshasa",
  "Bangui",
  "Kigali",
  "Bujumbura",
  "Mbabane",
  "Lobamba",
];

const topTouristCities = [
  "Bangkok",
  "Paris",
  "London",
  "Dubai",
  "Singapore",
  "New York",
  "Kuala Lumpur",
  "Istanbul",
  "Tokyo",
  "Seoul",
  "Hong Kong",
  "Barcelona",
  "Los Angeles",
  "Rome",
  "Osaka",
  "Las Vegas",
  "Amsterdam",
  "Milan",
  "Miami",
  "Vienna",
];

let keyword = ref("");
let names = ref([]);
let tld = ref("com");
let atTheEnd = ref(false);

function generateNames() {
  names.value = [];
  console.log(tld.value);
  for (let i = 0; i < topTouristCities.length; i++) {
    let domainName = "";
    ///upper the first letter of the keyword
    let upperFirstLetter =
      keyword.value[0].toUpperCase() + keyword.value.slice(1);
    ///add the keyword at the end of the generated domain name
    if (atTheEnd.value) {
      domainName += topTouristCities[i] + upperFirstLetter;
    } else domainName += upperFirstLetter + topTouristCities[i];

    names.value.push(domainName.replaceAll(" ", ""));
  }
  getWhois(names[0])
}

async function getWhois(name) {
  await fetch("https://api.api-ninjas.com/v1/whois?domain=" + name)
    .then((res) => res.json())
    .then((data) => console.log(data));
}
</script>


<template>
  <header>
    <div class="form">
      <input type="text" v-model="keyword" name="" id="" />
      <select v-model="tld">
        <option value="com" selected>com</option>
        <option value="net">net</option>
        <option value="org">org</option>
        <option value="ai">ai</option>
        <option value="io">io</option>
      </select>
      <label for="atTheEnd">
        <input type="checkbox" id="atTheEnd" v-model="atTheEnd" /> atTheEnd
      </label>

      <button @click="generateNames">Submit</button>
    </div>
  </header>

  <ul v-if="names.length > 1">
    <NameCard
      v-for="(name, index) in names"
      :key="index"
      :domain="name"
      :tld="tld"
    />
  </ul>
  <ul v-else>
    <li>Loading...</li>
  </ul>
</template>
  
<style scoped>
header {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 2rem;
  border-radius: 14px;
}
label {
  line-height: normal;
}
header input[type="text"],
header select,
header label,
header button,
span {
  background: #fff;
  color: var(--color-background);
  border-color: var(--color-background);
  border: 1px solid var(--vt-c-indigo);
}
ul {
  padding: 0;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
}
.form {
  display: flex;
  justify-content: center;
  padding: 10px;
  align-items: center;
  background: #fff;
  height: 150px;
  box-shadow: 0 0 5px #fff;
  border-radius: 10px;
}
label,
input[type="text"],
select,
button {
  padding: 5px 10px;
  background: transparent;
  color: var(--vt-c-indigo);
  font-size: 1rem;
  border: 1px solid var(--vt-c-indigo);
  margin: 0 5px;
  border-radius: 5px;
  outline: none;
}

label,
select,
button {
  cursor: pointer;
}
</style>
