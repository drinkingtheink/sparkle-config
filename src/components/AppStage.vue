<template>
  <div class="app-stage" :class="{ 'hide-controls': !showControls }">
    <button class="controls-toggle" @click="toggleControls">{{ this.showControls ? 'Hide Controls' : 'Show Controls'  }}</button>
    
    <h2>Configure Your Sparkle</h2>

    <section class="sparkle-container">
      <Sparkle 
        :lrgStarDelay="lrgStarDelay"
        :medStarDelay="medStarDelay"
        :smlStarDelay="smlStarDelay"
      />

      <div class="med-star-input input-container" >
        <label for="med-star-input-delay">Bottom Star Animation Delay:</label>
        <input 
          id="med-star-input-delay"
          type="range" 
          min="0"
          max="20"
          step="0.25"
          v-model="medStarDelay"
        />
        <span class="value-display"> {{  medStarDelay }}s</span>
      </div>

      <div class="sml-star-input input-container" >
        <label for="sml-star-input-delay">Top Star Animation Delay:</label>
        <input 
          id="sml-star-input-delay"
          type="range" 
          min="0"
          max="20"
          step="0.25"
          v-model="smlStarDelay"
        />
        <span class="value-display"> {{  smlStarDelay }}s</span>
      </div>

      <div class="lrg-star-input input-container" >
        <label for="lrg-star-input-delay">Large Star Animation Delay:</label>
        <input 
          id="lrg-star-input-delay"
          type="range" 
          min="0"
          max="20"
          step="0.25"
          v-model="lrgStarDelay"
        />
        <span class="value-display"> {{ lrgStarDelay }}s</span>
      </div>
    </section>

    <section class="controls" >
      <div>
        <h3>SVG Image Download</h3>
        
        <button @click="downloadImage" class="download-img">Download Sparkle Image</button>
      </div>
      <div>
      <h3>CSS Output</h3>
        <section class="code-output">
          <code>
            #lrg-star,
            #med-star,
            #sml-star {
                animation-name: twinkle;
                animation-duration: 4s;
                animation-delay: 0s;
                animation-iteration-count: infinite;
                transform-origin: center;
            }

            #lrg-star {
              animation-delay: {{ lrgStarDelay }}s;
            }

            #med-star {
              animation-delay: {{ medStarDelay }}s;
            }

            #sml-star {
              animation-delay: {{ smlStarDelay }}s;
            }
          </code>
        </section>

        <button 
          @click="copyCSS" 
          class="download-css"
          :class="{ 'success': copied }"  
        >{{ copyButtonText }}</button>
      </div>
    </section>
  </div>
</template>

<script>
import Sparkle from './Sparkle.vue'
const initialCopyText = 'Copy CSS'

export default {
  name: 'AppStage',
  data() {
    return {
        lrgStarDelay: 0,
        medStarDelay: 0.25,
        smlStarDelay: 0.5,
        imagePath: require('@/assets/sparkle-img.svg'),
        showControls: true,
        copyButtonText: initialCopyText,
    }
  },
  components: {
    Sparkle
  },
  props: {
    msg: String
  },
  methods: {
    downloadImage() {
      // Create an anchor element
      const link = document.createElement('a')
      
      // Set the download attribute with desired filename
      link.download = 'sparkle-img.svg'
      
      // Point the link to the image URL
      link.href = this.imagePath
      
      // Append to the document temporarily
      document.body.appendChild(link)
      
      // Trigger the download
      link.click()
      
      // Clean up
      document.body.removeChild(link)
    },
    copyCSS() {
      // Find the code element
      const codeElement = document.querySelector('.code-output code');
      const keyframes = `
@keyframes twinkle {
  0% {
      fill: var(--bluefill);
  }
  10% {
      fill: gray;
      transform: scale(0.95);
  }
  30% {
      fill: gray;
      transform: scale(1.05);
  }
  50% {
      fill: var(--bluefill);
      transform: scale(1);
  }
  100% {
      fill: var(--bluefill);
  }
}

      `
      
      if (!codeElement) {
        console.error('No code element found with selector ".code-output code"');
        return;
      }
      
      // Get the text content
      const codeText = keyframes + codeElement.textContent.trim();
      console.log(`COPIED TO CLIPBOARD >>>>>`);
      console.log(`${codeText}`);
      // Use the Clipboard API to copy the text
      navigator.clipboard.writeText(codeText)
        .then(() => {
          // Change button state to indicate success
          this.copied = true;
          this.copyButtonText = 'Copied!';
          
          // Reset button state after 2 seconds
          setTimeout(() => {
            this.copied = false;
            this.copyButtonText = initialCopyText;
          }, 2000);
        })
        .catch(err => {
          console.error('Failed to copy text: ', err);
          this.copyButtonText = 'Failed to copy';
          
          setTimeout(() => {
            this.copyButtonText = initialCopyText;
          }, 2000);
        });
    },
    toggleControls() {
      this.showControls = !this.showControls;
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
:root {
    --blue: #17a5ff;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.app-stage {
  position: relative;
  margin-top: 4rem;
}

.app-stage * {
  transition: all 0.2s;
}

.sparkle-container {
  margin: 0 auto;
  width: 500px;
  position: relative;
  background-color: white;
  padding: 1rem;
}

label,
.value-display {
  display: block;
}

.sml-star-input {
  position: absolute;
  right: -220px;
  top: 0;
}

.lrg-star-input {
  position: absolute;
  left: -200px;
  top: 20px;
}

.med-star-input {
  position: absolute;
  right: -200px;
  bottom: 20px;
}

.code-output {
  width: 400px;
  margin: 0 auto 1rem auto;
  border: 2px solid rgba(0,0,0,0.5);
  padding: 10px;
  border-radius: 5px;
  background-color: white;
  text-align: left;
}

.input-container {
  background-color: rgba(0,0,0,0.8);
  color: white;
  padding: 10px 20px;
  border-radius: 10px;
}

button {
  color: white;
  padding: 10px 15px;
  background-color: var(--blue);
  text-transform: uppercase;
  border-radius: 10px;
  transition: all 0.3s;
  font-size: 1rem;
}

button:hover {
  background-color: white;
  color: var(--blue);
  cursor: pointer;
}

.controls-toggle {
  font-size: 0.8rem;
  padding: 10px 20px;
  position: absolute;
  left: 0;
  right: 0;
  top: -3rem;
  margin: auto;
  width: 200px;
}

.controls {
  display: flex;
  justify-content: center;
}

.controls div {
  margin-right: 1rem;
}

.hide-controls .input-container,
.hide-controls .controls {
  opacity: 0;
  transform: translateY(-10px);
  pointer-events: none;
}

.download-css {
  width: 150px;
}

.download-css.success {
  background-color: rgb(7, 165, 7);
}

.download-css.success:hover {
  color: white;
}
</style>
