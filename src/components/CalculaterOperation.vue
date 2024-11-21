<template>
  <v-container class="d-flex justify-center align-center" style="height: 100vh">
    <v-card
      class="pa-3"
      style="max-width: 400px; background-color: #234"
      elevation="8"
    >
      <!-- Calculator Result -->
      <v-card-text
        class="text-h6 text-right font-weight-bold text-white mb-4 py-3"
        style="background-color: #31475e; border-radius: 8px"
      >
        {{ calculatorValue || 0 }}
      </v-card-text>

      <!-- Calculator Buttons -->
      <v-container class="pa-0">
        <v-row dense>
          <v-col
            cols="3"
            v-for="(n, index) in calculatorElements"
            :key="index"
            class="py-1 d-flex justify-center align-center"
          >
            <v-btn
              class="text-white"
              :color="['C','*','/','-','+','%','='].includes(n) ? 'green darken-2' : 'blue-grey darken-3'"
              elevation="2"
              block
              :style="{ fontWeight: 'bold', borderRadius: '8px' }"
              @click="action(n)"
            >
              {{ n }}
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: "CalculatorOP",
  props: {
    msg: String,
  },

  data() {
    return {
      calculatorValue: "",
      calculatorElements: [
        "C",
        "*",
        "/",
        "-",
        7,
        8,
        9,
        "+",
        4,
        5,
        6,
        "%",
        1,
        2,
        3,
        "=",
        0,
        ".",
      ],
      operator: null,
      previousCalculatorValue: "",
    };
  },

  methods: {
    action(n) {
      /* Append value */
      if (!isNaN(n) || n === ".") {
        this.calculatorValue += n + "";
      }

      /* Clear value */
      if (n === "C") {
        this.calculatorValue = "";
      }

      /* Percentage */
      if (n === "%") {
        this.calculatorValue = this.calculatorValue / 100 + "";
      }

      /* Operators */
      try {
        if (["/", "*", "-", "+"].includes(n)) {
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = "";
      }
      } catch (error) {
        console.log(error)
      }
      
      if (n === "=") {
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );
        this.previousCalculatorValue = "";
        this.operator = null;
      }
    },
  },
};
</script>

<style scoped>
.text-white {
  color: #ffffff !important;
}
</style>
