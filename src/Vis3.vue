<template>
    <div :id="containerID"></div>
  </template>
  
<script>
  export default {
    name: 'Vis3',
    props: {
      onLoad: Function,
      domainName: String,
      ID: String
    },
    data() {
      return {
        containerID: ''
      }
    },
    created() {
      // Generate a unique ID for the container
      this.containerID = Math.random().toString(36).substring(2)
  
      // If a callback function is provided, set it on the window object
      if (typeof this.onLoad === 'function') {
        window[`vis_callback_${this.containerID}`] = this.onLoad
      }
  
      // Create a script element and set its attributes
      const script = document.createElement('script')
      script.async = true
      script.src = `https://${this.domainName || ''}/${this.ID || ''}/embed?container=${this.containerID}&callback=vis_callback_${this.containerID}`
  
      // Append the script to the document body
      document.body.appendChild(script)
  
      // Cleanup function to remove the script element when the component unmounts or props change
      this.cleanup = () => {
        document.body.removeChild(script)
        // Remove the callback function from the window object
        if (typeof this.onLoad === 'function') {
          delete window[`vis_callback_${this.containerID}`]
        }
      }
    },
    beforeUnmount() {
      this.cleanup()
    }
  }
</script>