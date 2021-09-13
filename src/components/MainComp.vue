<template>
  <div class="container">
    <div class="country-container">
      
      <select class="form-select form-select-lg" id="country" v-model="selected_country_id">
            <option selected value="42"></option>
            <option v-for="i in countries.length" :key="i-1" :value="i-1">
                {{countries[i-1].name}}
            </option>
        </select>


        <div class="country-info" v-if="this.countries.length > 0">


          <table class="table table-bordered table-light">
            <thead class="table-active">
              <tr >
                <th colspan="2">
                  <img v-bind:src="countries[selected_country_id].flag" v-bind:alt="countries[selected_country_id].name" class="country-img">
                </th>
              </tr>

            </thead>
             <tbody>
                <tr>
                  <th scope="row">Name</th>
                  <td>{{countries[selected_country_id].name}}</td>
                </tr>
                <tr>
                  <th scope="row">Other Names</th>
                  <td>
                    <span class="span-list" v-for="nam in countries[selected_country_id].altSpellings" :key="nam">
                        {{nam}}
                    </span>
                  </td>
                </tr>

                <tr>
                  <th scope="row">ISO 3166-2 Code</th>
                  <td>{{countries[selected_country_id].alpha2Code}}</td>
                </tr>

                <tr>
                  <th scope="row">Capital</th>
                  <td>{{countries[selected_country_id].capital}}</td>
                </tr>

                <tr>
                  <th scope="row">Dialing Code</th>
                  <td> +{{countries[selected_country_id].callingCodes[0]}}</td>
                </tr>

                <tr>
                  <th scope="row">Top Level Domains</th>
                  <td>
                    <span class="span-list" v-for="dom in countries[selected_country_id].topLevelDomain" :key="dom">
                        {{dom}}
                    </span>
                  </td>
                </tr>

                <tr>
                  <th scope="row">Population</th>
                  <td v-if="countries[selected_country_id].population">{{countries[selected_country_id].population.toLocaleString("en-US")}}</td>
                  <td v-else>N/A</td>
                </tr>

                <tr>
                  <th scope="row">Area</th>
                  <td v-if="countries[selected_country_id].area">{{countries[selected_country_id].area.toLocaleString("en-US")}} km²</td>
                  <td v-else> N/A</td>
                </tr>

                <tr>
                  <th scope="row">Currencies</th>
                  <td>
                    <span class="span-list" v-for="curr in countries[selected_country_id].currencies" :key="curr">
                        {{curr.symbol}} {{curr.name}}
                    </span>
                  </td>
                </tr>

                <tr>
                  <th scope="row">Languages</th>
                  <td>
                    <span class="span-list" v-for="lang in countries[selected_country_id].languages" :key="lang.name">
                        {{lang.name}}
                    </span>
                  </td>
                </tr>

                <tr>
                  <th scope="row">Region</th>
                  <td>{{countries[selected_country_id].region}}</td>
                </tr>

                <tr>
                  <th scope="row">Subregion</th>
                  <td>{{countries[selected_country_id].subregion}}</td>
                </tr>

                <tr>
                  <th scope="row">Timezone(s)</th>
                  <td>
                    <span class="span-list" v-for="tz in countries[selected_country_id].timezones" :key="tz">
                        {{tz}}
                    </span>
                    </td>
                  
                </tr>

             </tbody>



          </table>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'main',
   data(){
        return{
          API_URL: "https://restcountries.eu/rest/v2/all",
          countries: [],
          selected_country_id: 42 //Defaults as 42 which is Canada
        }
    },

  methods:{
    countriesINIT(){
      try {
          fetch(this.API_URL)
          .then(res => {
            //console.log(res);
            if (res.status == 200){
                let data =res.json();
                //console.log(data)
                return data;
              }
              else{
                console.log("error")
                alert("Error "+res.status+": "+res.statusText);
                return;
              }
          })
          .then(this.setData);
        } catch (error) {
          alert(error.message);
        }
      }, //init
      setData(data){
        if(data){
          this.countries=[...data]
          //console.log(this.countries)
        }
        else{
          alert("Data is Empty")
        }
      }
    },
    beforeMount(){
    if(this.countries.length === 0){
      this.countriesINIT();
    }
  }

  
}

</script>


<style>
.country-container{
  align-content: center;
}
.country-img{
  max-height: 30vh;
  max-width:90%;
  border: 1px solid black;
}
.country-info{
  text-align: center;
}
td .span-list:not(:first-child)::before{
  content: ", ";
}
</style>
