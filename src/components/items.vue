<template>
  <div>
    <b-container class="" style="width=60vw" v-show="flight">
      <div>
        <b-row style="width=60vw">
          <b-col class="common_div">
            <div>
              <b-card
                title="Leaving From"
                @click="LeavemodalShow = !LeavemodalShow"
              >
                <b-card-text>
                  <h1>{{ departureIata }}</h1>
                  <h6>{{ departureName }}</h6>
                </b-card-text>
              </b-card>
            </div>
          </b-col>
          <b-col class="common_div">
            <div>
              <b-card title="Going To" @click="gomodalShow = !gomodalShow">
                <b-card-text>
                  <h1>{{ returnIata }}</h1>
                  <h6>{{ returnName }}</h6>
                </b-card-text>
              </b-card>
            </div>
          </b-col>
          <b-col class="common_div">
            <b-card-text>
              <div>
                <div>
                  <label for="example-datepicker">Departing On</label>
                  <b-form-datepicker
                    id="example-datepicker"
                    v-model="departingDatevalue"
                    class="mb-2"
                  ></b-form-datepicker>
                </div>
              </div>

              <div>
                <label for="example-datepicker">Returning On</label>
                <b-form-datepicker
                  id="example-datepickerw"
                  v-model="returningDatevalue"
                  class="mb-2"
                ></b-form-datepicker>
              </div>
            </b-card-text>
          </b-col>
          <b-col class="common_div">
            <div>
              <b-card>
                <b-card-text class="btn-grad" @click="sarchflight">
                  <h1>Search</h1>
                  <div class="flightbutton">
                    <i class="fas fa-plane "></i>
                  </div>
                  <h1>Flight</h1>
                </b-card-text>
              </b-card>
            </div>
          </b-col>
          <b-col class="common_div">
            <img src="../assets/image.jpg" alt="" width="100%" height="100%" />
          </b-col>
        </b-row>
        <b-modal
          v-model="LeavemodalShow"
          id="modal-scrollable"
          scrollable
          hide-footer
          title="Airports"
        >
          <b-form-input
            @keyup="desSearch"
            v-model="searchDes"
            placeholder="Destination Name"
          >
          </b-form-input>
          <b-list-group>
            <b-list-group-item
              v-for="(data, idx) in desData"
              :key="idx"
              @click="
                setDestinationiatacode(data.iata, data.name),
                  (LeavemodalShow = !LeavemodalShow)
              "
              >{{ data.iata }},{{ data.name }}</b-list-group-item
            >
          </b-list-group>
        </b-modal>
        <b-modal
          v-model="gomodalShow"
          id="modal-scrollable"
          scrollable
          hide-footer
          title="Airports"
        >
          <b-form-input
            @keyup="desSearch"
            v-model="searchDes"
            placeholder="Destination Name"
          >
          </b-form-input>
          <b-list-group>
            <b-list-group-item
              v-for="(data, idx) in desData"
              :key="idx"
              @click="
                setReturningiatacode(data.iata, data.name),
                  (gomodalShow = !gomodalShow)
              "
              >{{ data.iata }},{{ data.name }}</b-list-group-item
            >
          </b-list-group>
        </b-modal>
      </div>
    </b-container>
    <b-container v-show="flighttable" style="color:black"
      ><div>
        <b-table striped hover :items="items" :fields="fields"></b-table>
        <b-button @click="homeshow">HomePage</b-button>
      </div>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "items",
  data() {
    return {
      searchDes: "",
      flight: true,
      flighttable: false,
      departureIata: "City",
      departureName: "Country",
      returnIata: "City",
      returnName: "Country",
      LeavemodalShow: false,
      gomodalShow: false,
      departingDatevalue: "",
      returningDatevalue: "",
      desData: [],
      destinationIataCode: "",
      fields: [
        {
          key: "From",
          sortable: false
        },
        {
          key: "To",
          sortable: false
        },
        {
          key: "Time",
          sortable: true
        },
        {
          key: "Price",
          sortable: true
          // Variant applies to the whole column, including the header and footer
        }
      ],
      items: [
        {
          isActive: true,
          age: 40,
          first_name: "Dickerson",
          last_name: "Macdonald"
        },
        { isActive: false, age: 21, first_name: "Larsen", last_name: "Shaw" },
        { isActive: false, age: 89, first_name: "Geneva", last_name: "Wilson" },
        { isActive: true, age: 38, first_name: "Jami", last_name: "Carney" }
      ]
    };
  },
  methods: {
    desSearch() {
      fetch(
        "https://api.sharetrip.net/api/v1/flight/search/airport?name=" +
          this.searchDes
      )
        .then(res => res.json())
        .then(
          data => (this.desData = data.response)
          // console.log(this.desData.response[0].iata),
        );
    },
    setDestinationiatacode(iata, name) {
      (this.departureIata = iata), (this.departureName = name);
    },
    setReturningiatacode(iata, name) {
      (this.returnIata = iata), (this.returnName = name);
    },
    sarchflight() {
      this.flight = false;
      this.flighttable = true;
      // fetching data
      fetch(
        "https://api.sharetrip.net/api/v1/flight/search?tripType=Return&adult=1&child=0&infant=0&class=Economy&origin=" +
          this.departureIata +
          "&destination=" +
          this.returnIata +
          "&depart=" +
          this.departingDatevalue +
          "&depart=" +
          this.returningDatevalue
      )
        .then(res => res.json())
        .then(data => console.log(data));

      // fectching data
    },
    homeshow() {
      this.flight = true;
      this.flighttable = false;
    }
  }
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.common_div {
  margin: 0;
  padding: 0;
  background-color: white;
}
.flightbutton {
  transform: translateX(-5rem);
  width: 100%;
}
.flightbutton:hover {
  -webkit-transition: transform 1s ease-in-out;
  transform: translateX(3.25rem);
  transform: scaleY(3rem);
}

.btn-grad {
  background-image: linear-gradient(
    to right,
    #1a2980 0%,
    #26d0ce 51%,
    #1a2980 100%
  );
}
.btn-grad {
  text-align: center;
  text-transform: uppercase;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
  box-shadow: 0 0 20px #eee;
  border-radius: 10px;
  display: block;
}

.btn-grad:hover {
  background-position: right center; /* change the direction of the change here */
  color: #fff;
  text-decoration: none;
}
</style>
