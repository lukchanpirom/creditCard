<template>
  <v-app style="background: gray">
    <v-container>
      <v-card
        v-if="!flip"
        dark
        width="450"
        class="mx-auto mt-10 rounded-xl"
        elevation="12"
      >
        <v-img
          src="https://raw.githubusercontent.com/muhammederdem/credit-card-form/master/src/assets/images/23.jpeg"
          gradient="to top right, rgba(100,115,201,.33), rgba(25,32,72,.7)"
          height="300px"
        >
          <v-card-title class="ml-2 mt-2">
            <v-img
              src="https://raw.githubusercontent.com/muhammederdem/credit-card-form/master/src/assets/images/chip.png"
              max-width="60"
              max-height="60"
            ></v-img>
            <v-spacer></v-spacer>
            <v-img
              class="mr-3"
              src="https://raw.githubusercontent.com/muhammederdem/credit-card-form/master/src/assets/images/visa.png"
              max-width="85"
              max-height="60"
            ></v-img>
          </v-card-title>
          <v-card-text
            class="d-flex mt-9 py-2 px-2 text-center align-center justify-space-around"
            style="fontSize: 28px"
          >
            <div>
              <span class="font-weight-black">{{ cardNumber[0] || "#" }}</span>
              <span class="font-weight-black">{{ cardNumber[1] || "#" }}</span>
              <span class="font-weight-black">{{ cardNumber[2] || "#" }}</span>
              <span class="font-weight-black">{{ cardNumber[3] || "#" }}</span>
            </div>
            <div>
              <span class="font-weight-black">{{ cardNumber[4] || "#" }}</span>
              <span class="font-weight-black">{{ cardNumber[5] || "#" }}</span>
              <span class="font-weight-black">{{ cardNumber[6] || "#" }}</span>
              <span class="font-weight-black">{{ cardNumber[7] || "#" }}</span>
            </div>
            <div>
              <span class="font-weight-black">{{ cardNumber[8] || "#" }}</span>
              <span class="font-weight-black">{{ cardNumber[9] || "#" }}</span>
              <span class="font-weight-black">{{ cardNumber[10] || "#" }}</span>
              <span class="font-weight-black">{{ cardNumber[11] || "#" }}</span>
            </div>
            <div>
              <span class="font-weight-black">{{ cardNumber[12] || "#" }}</span>
              <span class="font-weight-black">{{ cardNumber[13] || "#" }}</span>
              <span class="font-weight-black">{{ cardNumber[14] || "#" }}</span>
              <span class="font-weight-black">{{ cardNumber[15] || "#" }}</span>
            </div>
          </v-card-text>
          <v-card-text class="d-flex mt-11 px-8">
            <div>
              <div style="fontSize: 14px">Card Holder</div>
              <div class="font-weight-black" style="fontSize: 16px">
                {{ cardName || "FULL NAME" }}
              </div>
            </div>
            <v-spacer></v-spacer>
            <div>
              <div style="fontSize: 14px">Expires</div>
              <div class="font-weight-black" style="fontSize: 16px">
                <span>{{ cardMonth }}</span>
                <span>/</span>
                <span>{{ cardYear }}</span>
              </div>
            </div>
          </v-card-text>
        </v-img>
      </v-card>
      <v-card
        v-else
        dark
        width="450"
        class="mx-auto mt-10 rounded-xl"
        elevation="12"
      >
        <v-img
          src="https://raw.githubusercontent.com/muhammederdem/credit-card-form/master/src/assets/images/23.jpeg"
          gradient="to top right, rgba(100,115,201,.33), rgba(25,32,72,.7)"
          height="300px"
        >
          <v-card-title
            class="mt-10 py-7"
            style="background: black"
            width="100%"
          >
          </v-card-title>
          <v-card-text class="d-flex align-end flex-column mt-3 text-center">
            <div class="mr-4 text-h8">CVV</div>
            <v-card
              class="mr-4 py-2 px-3 text-h7 text-end"
              width="400"
              height="40"
              style="background: white; color: black"
            >
              {{ cvv }}
            </v-card>
          </v-card-text>
          <v-card-text class="d-flex justify-end mt-4 px-8">
            <v-img
              class=""
              src="https://raw.githubusercontent.com/muhammederdem/credit-card-form/master/src/assets/images/visa.png"
              max-width="85"
              max-height="60"
            ></v-img>
          </v-card-text>
        </v-img>
      </v-card>
      <v-card width="600" height="600" mx-auto class="mt-10 mx-auto rounded-xl">
        <v-container class="pa-10">
          <v-row class="">
            <v-col>
              <v-text-field
                v-model="cardNumber"
                @focus="offFlip"
                label="Card Number"
                oninput="javascript: if (this.value.length > this.maxLength) this.value = this.value.slice(0, this.maxLength);"
                type="number"
                maxlength="16"
                outlined
              ></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col>
              <v-text-field
                v-model="cardName"
                @focus="offFlip"
                label="Card Holders"
                outlined
              ></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col>
              <v-select
                v-model="cardMonth"
                @focus="offFlip"
                :items="months"
                label="Month"
                outlined
              ></v-select>
            </v-col>
            <v-col>
              <v-select
                v-model="cardYear"
                @focus="offFlip"
                :items="years"
                label="Year"
                outlined
              ></v-select>
            </v-col>
            <v-col>
              <v-text-field v-model="cvv" label="CVV" @focus="onFlip" outlined></v-text-field>
            </v-col>
          </v-row>
        </v-container>
      </v-card>
    </v-container>
  </v-app>
</template>

<style>
</style>

<script>
export default {
  data() {
    return {
      cardName: "",
      cardNumber: "",
      cardMonth: "MM",
      cardYear: "YY",
      cvv: "",
      months: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],
      years: [2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023, 2024, 2025],
      flip: false,
    };
  },
  watch: {
    // cvv: function (value) {
    //   if (value) {
    //     this.flip = true;
    //   } else this.flip = false;
    // },
  },
  methods: {
    onlyNumberKey: function (evt) {
      // Only ASCII charactar in that range allowed
      var ASCIICode = evt.which ? evt.which : evt.keyCode;
      if (ASCIICode > 31 && (ASCIICode < 48 || ASCIICode > 57)) return false;
      return true;
    },
    onFlip: function() {
      this.flip = true;
    },
    offFlip: function() {
      this.flip = false;
    }
  },
};
</script>

