<template>
    <v-container>
      <v-card class="pa-4">
        <v-card-title>QR Code Scanner</v-card-title>
        <v-card-text>
          <div
            id="reader"
            style="width: 300px; height: 300px; margin: auto; border: 1px solid #ccc;"
          >
            <p v-if="!scanning" class="text-center mt-12">
              Camera will appear here when you click "Start Scanning"
            </p>
          </div>
  
          <div class="mt-4">
            <v-btn
              v-if="!scanning"
              color="primary"
              @click="startScanner"
            >
              📷 Start Scanning
            </v-btn>
  
            <v-btn
              v-if="scanning"
              color="red"
              @click="stopScanner"
            >
              🛑 Stop Scanning
            </v-btn>
          </div>
  
          <div v-if="result" class="mt-4">
            <v-alert type="success">
              ✅ Scanned QR Code: <strong>{{ result }}</strong>
            </v-alert>
          </div>
        </v-card-text>
      </v-card>
    </v-container>
  </template>
  
  <script>
  import { Html5Qrcode } from 'html5-qrcode'
  
  export default {
    data () {
      return {
        result: null,
        html5QrCode: null,
        scanning: false
      }
    },
    methods: {
      startScanner () {
        this.scanning = true
        console.log("Starting QR scanner…")
  
        this.html5QrCode = new Html5Qrcode("reader")
        this.html5QrCode.start(
          { facingMode: "environment" },
          {
            fps: 10,
            qrbox: { width: 250, height: 250 }
          },
          decodedText => {
            this.result = decodedText
            this.stopScanner()
          },
          errorMessage => {
            // optional: console.warn(errorMessage)
          }
        ).catch(err => {
          console.error("Unable to start scanning:", err)
          this.scanning = false
        })
      },
  
      stopScanner () {
        if (this.html5QrCode) {
          this.html5QrCode.stop().then(() => {
            console.log("Scanner stopped.")
            this.html5QrCode.clear()
            this.scanning = false
          }).catch(err => {
            console.error("Failed to stop scanner:", err)
          })
        }
      }
    },
    beforeDestroy () {
      this.stopScanner()
    }
  }
  </script>
  