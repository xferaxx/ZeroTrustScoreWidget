<template>
  <v-app>
    <v-container>
      <!-- Zero-Trust Score Widget Header -->
      <v-row class="text-center mb-4">
        <v-col>
          <h1>Zero-Trust Score for {{ companyName }}</h1>
          <h2>Overall Score: {{ zeroTrustScore }}</h2>
        </v-col>
      </v-row>

      <!-- Risk Category Indicator -->
      <v-row class="text-center mb-4">
        <v-col>
          <v-chip :color="riskCategoryColor" dark>{{ riskCategory }}</v-chip>
        </v-col>
      </v-row>

      <!-- Metrics Section with Progress Bars -->
      <v-row>
        <v-col v-for="(score, metric) in metrics" :key="metric" cols="12" md="6">
          <v-card class="mb-4">
            <v-card-title>{{ metric }}</v-card-title>
            <v-card-subtitle>{{ metricDescriptions[metric] }}</v-card-subtitle>
            <v-card-text>
              <v-progress-linear :value="score" color="primary" height="20">
                <template v-slot:default>{{ score }}%</template>
              </v-progress-linear>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      companyName: "FinTechSecure Ltd.",
      zeroTrustScore: 58.5,
      metrics: {
        "Network Security": 75,
        "Application Security": 45,
        "User Authentication": 65,
        "Data Encryption": 80,
      },
      metricDescriptions: {
        "Network Security": "Measures the security of the network infrastructure.",
        "Application Security": "Evaluates the security of applications in use.",
        "User Authentication": "Assesses the strength of user authentication mechanisms.",
        "Data Encryption": "Indicates the level of encryption applied to data.",
      },
      riskCategory: "Moderate Risk",
    };
  },
  computed: {
    riskCategoryColor() {
      return this.riskCategory === "High Risk" ? "red" : this.riskCategory === "Moderate Risk" ? "orange" : "green";
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
