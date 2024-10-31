<template>
  <v-container class="pa-4">
    <!-- Company Name and Overall Zero-Trust Score -->
    <v-card class="mb-4" color="primary" dark>
      <v-card-title>{{ zeroTrustData.companyName }}</v-card-title>
      <v-card-subtitle>Overall Zero-Trust Score: {{ zeroTrustData.ZeroTrustScore }}</v-card-subtitle>
    </v-card>

    <!-- Individual Metric Scores -->
    <v-card class="mb-4" outlined>
      <v-card-title>Metrics</v-card-title>
      <v-card-text>
        <div v-for="(value, key) in zeroTrustData.metrics" :key="key">
          <v-row align="center">
            <v-col cols="4">
              <strong>{{ key }}</strong>
            </v-col>
            <v-col cols="6">
              <v-progress-linear :value="value" color="blue" height="10"></v-progress-linear>
            </v-col>
            <v-col cols="2" class="text-right">
              {{ value }}%
            </v-col>
          </v-row>
        </div>
      </v-card-text>
    </v-card>

    <!-- Observable Data -->
    <v-card class="mb-4" outlined>
      <v-card-title>Observable Data</v-card-title>
      <v-card-text>
        <v-row>
          <v-col cols="6">
            Average Shannon Entropy Score: {{ zeroTrustData.observableData.averageShannonEntropyScore }}
          </v-col>
          <v-col cols="6">
            Firewall Detected: <strong>{{ zeroTrustData.observableData.firewallDetected ? 'Yes' : 'No' }}</strong>
          </v-col>
          <v-col cols="6">
            DNSsec Enabled: <strong>{{ zeroTrustData.observableData.DNSsecEnabled ? 'Yes' : 'No' }}</strong>
          </v-col>
          <v-col cols="6">
            TLS Version: {{ zeroTrustData.observableData.tlsVersion }}
          </v-col>
          <v-col cols="6">
            Certificate Bit Strength: {{ zeroTrustData.observableData.certificateBitStrength }}
          </v-col>
          <v-col cols="6">
            Open Ports Detected: {{ zeroTrustData.observableData.openPortsDetected }}
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>

    <!-- Risk Category Indicator -->
    <v-alert :type="riskCategoryType" border="left" prominent>
      Risk Category: {{ zeroTrustData.riskCategory }}
    </v-alert>
  </v-container>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';

const zeroTrustData = ref({
  companyName: "FinTechSecure Ltd.",
  ZeroTrustScore: 58.5,
  metrics: {
    "Network Security": 70,
    "Application Security": 60,
    "Data Protection": 50,
    "User Authentication": 80,
    "Monitoring & Auditing": 55
  },
  observableData: {
    averageShannonEntropyScore: 7.8,
    firewallDetected: true,
    DNSsecEnabled: true,
    tlsVersion: "1.2",
    certificateBitStrength: 2048,
    securityHeadersImplemented: ["X-XSS-Protection", "X-Frame-Options"],
    openPortsDetected: 12
  },
  riskCategory: "Moderate Risk"
});

// Computed property to determine risk category color
const riskCategoryType = computed(() => {
  switch (zeroTrustData.value.riskCategory) {
    case 'Low Risk':
      return 'success';
    case 'Moderate Risk':
      return 'warning';
    case 'High Risk':
      return 'error';
    default:
      return 'info';
  }
});
</script>

<style scoped>
.v-card-title {
  font-weight: bold;
}
</style>
