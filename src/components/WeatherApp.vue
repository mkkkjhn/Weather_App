<template>
  <div class="container">
    <h1 class="title">Today's weather</h1>
    <table>
      <tr>
        <th>
          <button class="sortButton" @click="sortByColumn('name'); isColumnSorted = !isColumnSorted">
            City
            <svg clip-rule="evenodd" fill-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2" viewBox="0 0 24 24">
              <path d="m15.344 17.778c0-.414-.336-.75-.75-.75h-5.16c-.414 0-.75.336-.75.75s.336.75.75.75h5.16c.414 0 .75-.336.75-.75zm2.206-4c0-.414-.336-.75-.75-.75h-9.596c-.414 0-.75.336-.75.75s.336.75.75.75h9.596c.414 0 .75-.336.75-.75zm2.45-4c0-.414-.336-.75-.75-.75h-14.5c-.414 0-.75.336-.75.75s.336.75.75.75h14.5c.414 0 .75-.336.75-.75zm2-4c0-.414-.336-.75-.75-.75h-18.5c-.414 0-.75.336-.75.75s.336.75.75.75h18.5c.414 0 .75-.336.75-.75z" fill-rule="nonzero"/>
            </svg>
          </button>
        </th>
        <th>
          <button class="sortButton" @click="sortByColumn('minTemp'); isColumnSorted = !isColumnSorted">
            Min Temp
            <svg clip-rule="evenodd" fill-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2" viewBox="0 0 24 24">
              <path d="m15.344 17.778c0-.414-.336-.75-.75-.75h-5.16c-.414 0-.75.336-.75.75s.336.75.75.75h5.16c.414 0 .75-.336.75-.75zm2.206-4c0-.414-.336-.75-.75-.75h-9.596c-.414 0-.75.336-.75.75s.336.75.75.75h9.596c.414 0 .75-.336.75-.75zm2.45-4c0-.414-.336-.75-.75-.75h-14.5c-.414 0-.75.336-.75.75s.336.75.75.75h14.5c.414 0 .75-.336.75-.75zm2-4c0-.414-.336-.75-.75-.75h-18.5c-.414 0-.75.336-.75.75s.336.75.75.75h18.5c.414 0 .75-.336.75-.75z" fill-rule="nonzero"/>
            </svg>
          </button>
        </th>
        <th>
          <button class="sortButton" @click="sortByColumn('maxTemp'); isColumnSorted = !isColumnSorted">
            Max Temp
            <svg clip-rule="evenodd" fill-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2" viewBox="0 0 24 24">
              <path d="m15.344 17.778c0-.414-.336-.75-.75-.75h-5.16c-.414 0-.75.336-.75.75s.336.75.75.75h5.16c.414 0 .75-.336.75-.75zm2.206-4c0-.414-.336-.75-.75-.75h-9.596c-.414 0-.75.336-.75.75s.336.75.75.75h9.596c.414 0 .75-.336.75-.75zm2.45-4c0-.414-.336-.75-.75-.75h-14.5c-.414 0-.75.336-.75.75s.336.75.75.75h14.5c.414 0 .75-.336.75-.75zm2-4c0-.414-.336-.75-.75-.75h-18.5c-.414 0-.75.336-.75.75s.336.75.75.75h18.5c.414 0 .75-.336.75-.75z" fill-rule="nonzero"/>
            </svg>
          </button>
        </th>
        <th></th>
      </tr>
      <tr :key="city.id" v-for="city in selectedCities">
        <td>{{city.name}}</td>
        <td>{{city.minTemp}}</td>
        <td>{{city.maxTemp}}</td>
        <td>
          <button class="deleteCityButton" @click="deleteTheCity(city.id)">
            <svg clip-rule="evenodd" fill-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2" viewBox="0 0 24 24">
              <path d="m21 4c0-.478-.379-1-1-1h-16c-.62 0-1 .519-1 1v16c0 .621.52 1 1 1h16c.478 0 1-.379 1-1zm-16.5.5h15v15h-15zm11.75 6.752h-8.5c-.414 0-.75.336-.75.75s.336.75.75.75h8.5c.414 0 .75-.336.75-.75s-.336-.75-.75-.75z" fill-rule="nonzero"/>
            </svg>
          </button>
        </td>
      </tr>
    </table>
    <div>
      <button class="addCityButton" @click="isListActive = !isListActive">
        <svg clip-rule="evenodd" fill-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2" viewBox="0 0 24 24">
          <path d="m21 3.998c0-.478-.379-1-1-1h-16c-.62 0-1 .519-1 1v16c0 .621.52 1 1 1h16c.478 0 1-.379 1-1zm-16.5.5h15v15h-15zm6.75 6.752h-3.5c-.414 0-.75.336-.75.75s.336.75.75.75h3.5v3.5c0 .414.336.75.75.75s.75-.336.75-.75v-3.5h3.5c.414 0 .75-.336.75-.75s-.336-.75-.75-.75h-3.5v-3.5c0-.414-.336-.75-.75-.75s-.75.336-.75.75z" fill-rule="nonzero"/>
        </svg>
      </button>
      <ul class="addCitiesList" v-if="isListActive">
        <li :key="city.id" v-for="city in predefinedCities">
          <button @click="addNewCity(city.name)">{{city.name}}</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      selectedCities: [
        {
          name: 'London',
          minTemp: '',
          maxTemp: '',
          id: 1,
          cords: 'latitude=51.51&longitude=-0.13'
        },
        {
          name: 'Berlin',
          minTemp: '',
          maxTemp: '',
          id: 2,
          cords: 'latitude=52.52&longitude=13.41'
        },
        {
          name: 'Lisbon',
          minTemp: '',
          maxTemp: '',
          id: 3,
          cords: 'latitude=38.72&longitude=-9.13'
        }
      ],
      predefinedCities: [
        {
          name: 'Melbourne',
          minTemp: '',
          maxTemp: '',
          id: 4,
          cords: 'latitude=-37.81&longitude=144.96'
        },
        {
          name: 'Rome',
          minTemp: '',
          maxTemp: '',
          id: 5,
          cords: 'latitude=41.89&longitude=12.51'
        },
        {
          name: 'Paris',
          minTemp: '',
          maxTemp: '',
          id: 6,
          cords: 'latitude=48.85&longitude=2.35'
        },
        {
          name: 'Ottawa',
          minTemp: '',
          maxTemp: '',
          id: 7,
          cords: 'latitude=45.41&longitude=-75.70'
        },
        {
          name: 'Manchester',
          minTemp: '',
          maxTemp: '',
          id: 8,
          cords: 'latitude=53.48&longitude=-2.24'
        },
        {
          name: 'Bruges',
          minTemp: '',
          maxTemp: '',
          id: 9,
          cords: 'latitude=51.21&longitude=3.22'
        }
      ],
      isListActive: false,
      isColumnSorted: false
    }
  },
  methods: {
    async fetchTemperature (city) {
      try {
        const response = await axios.get(`https://api.open-meteo.com/v1/forecast?${city.cords}&daily=temperature_2m_max,temperature_2m_min&current_weather=true&timezone=auto`)
        city.minTemp = response.data.daily.temperature_2m_min[0]
        city.maxTemp = response.data.daily.temperature_2m_max[0]
      } catch (e) {
        alert('Owibqa' + city.name)
      }
    },
    async fetchForDefaultCities () {
      for (const e of this.selectedCities) {
        await this.fetchTemperature(e)
      }
    },
    async addNewCity (value) {
      const newCity = this.predefinedCities.find(city => city.name === value)
      this.selectedCities.push(newCity)
      await this.fetchTemperature(newCity)
      this.predefinedCities.splice(this.predefinedCities.indexOf(newCity), 1)
    },
    deleteTheCity (id) {
      const selectedCity = this.selectedCities.find(c => c.id === id)
      this.selectedCities = this.selectedCities.filter(c => c.id !== id)
      this.predefinedCities.unshift(selectedCity)
    },
    ascendingSort (column) {
      return (a, b) => a[column] > b[column] ? 1 : -1
    },
    descendingSort (column) {
      return (a, b) => a[column] > b[column] ? -1 : 1
    },
    sortByColumn (columnName) {
      this.selectedCities.sort(this.isColumnSorted ? this.ascendingSort(columnName) : this.descendingSort(columnName))
    }
  },
  mounted () {
    this.fetchForDefaultCities()
  }
}
</script>

<style lang="scss" scoped>
*{
  padding: 0;
  margin: 0;
  border: 0;
}
*,*:before,*:after{
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
:focus,:active{outline: none;}
a:focus,a:active{outline: none;}

nav,footer,header,aside{display: block;}

html,body{
  height: 100%;
  width: 100%;
  line-height: 1;
  font-size: 14px;
  -ms-text-size-adjust: 100%;
  -moz-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}
input,button,textarea{font-family:inherit;}

input::-ms-clear{display: none;}
button{
  cursor: pointer;
  background-color: inherit;
}
button::-moz-focus-inner {padding:0;border:0;}
a, a:visited{text-decoration: none;}
a:hover{text-decoration: none;}
ul li{list-style: none;}
img{vertical-align: top;}

h1,h2,h3,h4,h5,h6{font-weight: 400;}

/* Обнудение */

.title {
  font-family: 'Roboto',serif;
  margin-bottom: 30px;
}
.container {
  display: flex;
  align-items: center;
  flex-direction: column;
}
.addCityButton {
  margin: 20px;
  svg {
    height: 24px;
  }
  svg:hover {
    opacity: .6;
  }
}
.deleteCityButton {
  svg {
    height: 16px;
    transition: opacity .2s linear;
  }
  svg:hover {
    opacity: .6;
  }
}
th {
  padding: 12px;
  text-transform: uppercase;
}
td {
  padding: 4px 0;
}
.addCitiesList {
  background-color: honeydew;
  display: flex;
  flex-direction: column;
  li {
    text-align: left;
  }
}
.sortButton {
  text-transform: uppercase;
  font-weight: bold;
  font-size: 16px;
  svg {
    height: 14px;
  }
}
</style>
