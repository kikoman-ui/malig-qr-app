<template>
    <v-container>
      <v-card class="pa-4">
        <v-card-title>QR Code Scanner</v-card-title>
        <v-card-text>
          <div
            id="reader"
            style="width: 300px; height: 300px; margin: auto;"
          ></div>
  
          <div v-if="result" class="mt-4">
            <v-alert type="success">
              ✅ Scanned QR Code: <strong>{{ result }}</strong>
            </v-alert>
  
            <v-btn color="primary" class="mt-2" @click="restartScanner">
              🔄 Scan Again
            </v-btn>
          </div>
        </v-card-text>
      </v-card>
    </v-container>
  </template>
  
  <script>
  // 👇 Import from the installed npm package
  import { Html5Qrcode } from 'html5-qrcode'
  
  export default {
    data () {
      return {
        result: null,
        html5QrCode: null
      }
    },
    mounted () {
      this.startScanner()
    },
    methods: {
      startScanner () {
        const html5QrCode = new Html5Qrcode("reader")
        this.html5QrCode = html5QrCode
  
        html5QrCode.start(
          { facingMode: "environment" }, // back camera
          {
            fps: 10,
            qrbox: { width: 250, height: 250 }
          },
          decodedText => {
            this.result = decodedText
            html5QrCode.stop().then(() => {
              console.log('Scanner stopped after scan.')
            })
          },
          errorMessage => {
            // optional: handle errors here
            // console.warn(`Scan error: ${errorMessage}`)
          }
        ).catch(err => {
          console.error("Unable to start scanning:", err)
        })
      },
      restartScanner () {
        this.result = null
        this.startScanner()
      }
    },
    beforeDestroy () {
      if (this.html5QrCode) {
        this.html5QrCode.stop().catch(() => {})
      }
    }
  }
  </script>
  