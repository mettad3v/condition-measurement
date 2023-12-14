<template>
  <v-container class="fill-height">
    <v-responsive class=" fill-height">


      <v-row class="d-flex justify-center mt-10">


        <v-col>
          <v-select label="Select Year" :items="yearList" v-model="selectedYear"></v-select>
        </v-col>
        <v-col>
          <v-select label="Disease Condition" :items="diseaseCodes" v-model="selectedDisease"></v-select>
        </v-col>
        <v-col cols="auto">
          <v-btn @click="submit" :loading="isLoading" color="#5865f2" class="d-inline" size="x-large">
            Submit
          </v-btn>
        </v-col>




      </v-row>


      <v-row>
        <v-col class="mt-15 d-flex justify-center align-center">
          <div class="output">
            <h3 class="mb-2">OUTCOME </h3>
            <div>
              333333
            </div>
          </div>
        </v-col>
      </v-row>

    </v-responsive>
  </v-container>
</template>

<script setup>
import { ref } from 'vue'

const yearList = [
  1990, 1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998, 1999,
  2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009,
  2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019,
  2020, 2021, 2022, 2023
];

const diseaseCodes = [
  10509002,
  65363002,
  43878008,
  65966004,
  232353008,
  10509002,
  65363002,
  43878008,
  65966004,
  232353008,
  446096008,
  284551006,
  44465007,
]

const selectedDisease = ref()
const selectedYear = ref()
const isLoading = ref(false)


const submit = async () => {

  isLoading.value = true
  try {
    const res = await fetch(`https://gosh-synth-fhir.azurehealthcareapis.com/Condition?onset-date=${selectedYear.value}&code=${selectedDisease.value}&_summary=count`, {
      method: 'GET',
      headers: {
        'Authorization': `Bearer ${import.meta.env.VITE_TOKEN}`
      }
    })

    isLoading.value = false
    console.log(res);
  } catch (error) {
    console.log(error);
  }
}



</script>


<style lang="scss">
.output {

  h3 {
    text-align: center;
    letter-spacing: 0.167rem;
  }

  div {
    padding: 0.25em 1.5em;
    aspect-ratio: 1;
    background-color: #ddd;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2.5rem;
    font-weight: bold;
  }


}
</style>