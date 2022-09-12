<template>
  <div class="heading">
    <p
      style="
        margin: 0px;
        margin-bottom: 50px;
        padding-top: 20px;
        font-size: 40px;
      "
    >
      CALENDER EVENTS BY DATE
    </p>
    <input
      v-model="selectedDate"
      @change="fetchEvent"
      class="dateInput"
      type="date"
    />
    <table>
      <thead>
        <tr>
          <th>Country</th>
          <th>Calender ID</th>
          <th>Date</th>
          <th>Event</th>
          <th>Ticker</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="event in events" :key="event">
          <td>{{ event.Country }}</td>
          <td>{{ event.CalendarId }}</td>
          <td>{{ event.Date }}</td>
          <td>{{ event.Event }}</td>
          <td>{{ event.Ticker }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      selectedDate: null,
      events: [],
    };
  },
  methods:{
    fetchEvent() {
      axios
        .get(
          `https://api.tradingeconomics.com/calendar/country/All/${this.selectedDate}/${this.selectedDate}?c=guest:guest&f=json`
        )
        .then((response) => {
          this.events = response.data;
        });
    },
  },
};
</script>
<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto+Condensed&display=swap");
.heading {
  height: 600px;
  text-align: center;
  background-color: bisque;
  background-image: linear-gradient(bisque, white);
  font-family: "Roboto Condensed", sans-serif;
  color:#8D918D;
}
.dateInput {
  padding: 10px 30px 10px 30px;
  border-radius: 5px;
  border: 1px solid white;
}
.dateInput:focus {
  outline: none !important;
}
table {
  margin: auto;
  margin-top: 50px;
  border-collapse: collapse;
  width: 50%;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #f8e6e6;
}
</style>
