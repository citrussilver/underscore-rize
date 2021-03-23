<template>
  <section class="hero is-fullheight is-bold hero-override">
      <div class="hero-body">
          <div class="container has-text-centered">
              <p class="title">
                Underscore-rize
                </p>
                 <p class="subtitle">
                    Replace spaces with underscores
                </p>
              <div class="content-container">
                  <div class="content-container-item">
                      <textarea id="inputBox" placeholder="Paste or type your text here" cols="30" rows="10" spellcheck="false" v-model="stringInput" @keyup="checkText" />
                    </div>
                    <div class="content-container-item">
                        <label class="text-counter">{{stringInput.length}}</label>
                    </div>
                </div>
                <div class="buttons-container content">
                    <div class="one-third column">
                        <button @click.prevent="process" class="button is-success is-rounded override">underscore-rize!</button>
                    </div>
                    <div class="one-third column">
                        <button :disabled="isDisabled" @click.prevent="copyText" class="button is-primary is-rounded override">Copy to Clipboard</button>
                    </div>
                    <div class="one-third column">
                        <button @click.prevent="resetText" class="button is-danger is-rounded override reset">Reset</button>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import { toast } from 'bulma-toast'


export default {
    data() {
        return {
            stringInput: '',
            isDisabled: true
        }
    },
    components: {
        
    },
    methods: {
        process: function() {
            try {
                if(this.stringInput.length > 0) {
                    this.isDisabled = false
                    console.log(this.stringInput.replace(/ /g,"_"));
                    this.stringInput = this.stringInput.replace(/ /g,"_");
                    toast({
                        message: 'Text Underscore-rized!',
                        type: 'is-success',
                        position: "top-center",
                        dismissible: true,
                        pauseOnHover: true,
                        closeOnClick: true
                    });
                }
                else {
                    this.isDisabled = true
                    toast({
                        message: 'Please type something!',
                        type: 'is-danger',
                        position: "top-center",
                        dismissible: true,
                        pauseOnHover: true,
                        closeOnClick: true
                    });
                }
            } catch (error) {
                toast({
                    message: error + ' occured!',
                    type: 'is-danger',
                    position: "top-center",
                    dismissible: true,
                    pauseOnHover: true,
                    closeOnClick: true
                });   
            }
        },
        copyText: async function() {
            await navigator.clipboard.writeText(this.stringInput)
                .then(function() {
                    toast({
                        message: 'Copied to clipboard!',
                        type: 'is-danger',
                        position: "top-center",
                        dismissible: true,
                        pauseOnHover: true,
                        closeOnClick: true
                    });
                }, function() {
                    toast({
                        message: 'Copy to clipboard failed!',
                        type: 'is-danger',
                        position: "top-center",
                        dismissible: true,
                        pauseOnHover: true,
                        closeOnClick: true
                    });
                });
            this.isDisabled = !this.isDisabled;
        },
        checkText: function() {
            if(this.stringInput.length > 0) {
                this.isDisabled = true
            }
            else {
                this.isDisabled = false
            }
        },
        resetText: function() {
            this.stringInput = ''
        }
    },
}
</script>

<style scoped>
    body {
        --transition-delay: 1s;
        margin: 0;
    }

    .content-container {
        display: flex;
        flex-direction: column;
        margin: 2rem 0rem;
    }
    .content-container-item {
        margin: 0.5rem 2rem;
    }
    
    .hero-override {
        background-color: #2B2624;
    }

    .hero-override p, label {
        color: #fff;
    }

    .buttons-container.content, .one-third.column {
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .one-third.column {
        margin: 0rem 1rem;
    }

    .override {
        font-weight: bold;
        
        transition: transform 0.5s ease-in-out;
        /* transition: transform 1s cubic-bezier(0.98, 0.32, 0.3, 1.04); */
        transform: scale(1);
    }

    .override:hover {
        transform: scale(1.1);
        background: #e69138;
        border: 1.5px solid #fff;
    }

    .override.reset:hover {
        background: white;
        color: #f14668;
        border: 1.5px solid #f14668;
    }

    .text-counter {
        background: #66615e;
        padding: 0.8rem;
        border-radius: 5rem;
    }

    #inputBox {
        outline: none;
        font-size: 1.5rem;
        resize: none;
        background-color: #2B2624;
        color: white;
        border: 0.1px solid #fff;
        border-radius: 0.5rem;
    }

    @media screen and (max-width: 600px) {
        /* smaller screens */

        .buttons-container.content {
            flex-direction: column;   /* by simply swap direction it work on smaller screen */
            align-items: center;
            justify-content: center;
        }

        #inputBox {
            width: 70vw;
        }
    }
</style>