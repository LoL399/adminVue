<template>
  <div id="movie">
    <!-- detail event -->
    <v-container fluid grid-list-xl>
      <v-layout row wrap>
        <v-flex d-flex lg8 sm6 xs12>
            <div  style=" 
  transition: 0.3s;
  width: 40%">
  <data-table data="hello"/></div>
         </v-flex>
        <v-flex d-flex lg4 sm6 xs12>
          <div
            style="  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  width: 40%; background-color: white; padding: 3%"
          >
            <v-form ref="form" v-model="valid" lazy-validation>
              <img
                src="https://upload.wikimedia.org/wikipedia/commons/5/51/This_Gun_for_Hire_%281942%29_poster.jpg"
                style="
    width: 200px;
    height: auto;
    margin: auto;
    display: block;"
              />
              <h2>Form Wizard</h2>
              <p>Nostrud exercitation commodo consequat.</p>
              <v-text-field
                v-model="name"
                :rules="nameRules"
                :counter="10"
                label="Name"
                required
              ></v-text-field>
              <v-text-field
                v-model="email"
                :rules="emailRules"
                label="E-mail"
                required
              />
              <v-select
                v-model="select"
                :items="items"
                :rules="[v => !!v || 'Item is required']"
                label="Item"
                required
              />
              <v-checkbox
                v-model="checkbox"
                :rules="[v => !!v || 'You must agree to continue!']"
                label="Do you agree?"
                required
              />

              <v-btn :disabled="!valid" @click="submit"> submit </v-btn>
              <v-btn @click.native="clear">clear</v-btn>
            </v-form>
          </div>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    var d = new Date();

    return {
      dialog: false,
      dialogCreateEvent: false,
      newEventTitle: null,
      createEventDate: null,
      selectedEventClass: null,
      selectedEvent: null,
      events: [
        {
          title: "Test",
          start: `${d.getFullYear()}-${d.getMonth() + 1}-01`,
          end: `${d.getFullYear()}-${d.getMonth() + 1}-03`,
          cssClass: "event-item-caution"
        },
        {
          title: "Meeting",
          start: `${d.getFullYear()}-${d.getMonth() + 1}-05`,
          end: `${d.getFullYear()}-${d.getMonth() + 1}-07`,
          cssClass: "event-item-trip"
        },
        {
          title: "Europe Trip",
          start: `${d.getFullYear()}-${d.getMonth() + 1}-03`,
          end: `${d.getFullYear()}-${d.getMonth() + 1}-07`,
          cssClass: "event-item-warning"
        },
        {
          title: "Event",
          start: `${d.getFullYear()}-${d.getMonth() + 1}-12`,
          cssClass: "event-item-meeting"
        },
        {
          title: "Event",
          start: `${d.getFullYear()}-${d.getMonth() + 1}-16`,
          cssClass: "event-item-meeting"
        },
        {
          title: "Europe Trip",
          start: `${d.getFullYear()}-${d.getMonth() + 1}-20`,
          end: `${d.getFullYear()}-${d.getMonth() + 1}-23`,
          cssClass: "event-item-caution"
        },

        {
          title: "Test",
          start: `${d.getFullYear()}-${d.getMonth() + 1}-05`,
          cssClass: "event-item-caution"
        },
        {
          title: "Test",
          start: `${d.getFullYear()}-${d.getMonth() + 1}-27`,
          end: `${d.getFullYear()}-${d.getMonth() + 1}-28`,
          cssClass: "event-item-meeting"
        },
        {
          title: "Test",
          start: `${d.getFullYear()}-${d.getMonth() + 1}-17`,
          end: `${d.getFullYear()}-${d.getMonth() + 1}-19`,
          cssClass: "event-item-trip"
        },
        {
          title: "Event example",
          start: `${d.getFullYear()}-${d.getMonth() + 1}-08`,
          cssClass: "event-item-meeting"
        },
        {
          title: "Event example",
          start: `${d.getFullYear()}-${d.getMonth() + 1}-16`,
          cssClass: "event-item-meeting"
        }
      ]
    };
  },

  methods: {
    eventClick($event) {
      const vm = this;

      vm.dialog = true;

      vm.selectedEvent = $event;
    },

    dayClick($event) {
      const vm = this;

      vm.dialogCreateEvent = true;

      vm.createEventDate = $event;
    },

    createEvent() {
      const vm = this;

      vm.events.push({
        title: vm.newEventTitle ? vm.newEventTitle : "Sample Event",
        start: vm.createEventDate,
        cssClass: vm.selectedEventClass ? vm.selectedEventClass : null
      });

      vm.createEventDate = null;
      vm.newEventTitle = "";
      vm.dialogCreateEvent = false;
    }
  }
};
</script>

<style>
#calendar {
  height: 100%;
}

.prev-month {
  font-size: 20px !important;
  font-weight: bold;
}

.next-month {
  font-size: 20px !important;
  font-weight: bold;
}

.event-item {
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif !important;
  font-size: 14px !important;
}

.event-item-caution {
  background-color: #e89a9a !important;
}

.event-item-warning {
  background-color: #ffffa5 !important;
}

.event-item-meeting {
  background-color: #71d48e !important;
}

.event-item-trip {
  background-color: #8d78e6 !important;
}
</style>
