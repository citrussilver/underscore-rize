<template>
  <section class="hero is-fullheight is-info is-bold">
      <div class="hero-body">
          <div class="container has-text-centered">
              <h2 class="subtitle">Underscore-rize</h2>
              <div class="content-container">
                  <div class="content-container-item">
                      <textarea id="inputBox" cols="30" rows="10" spellcheck="false" v-model="stringInput" @keyup="checkText" />
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
                        <button @click.prevent="resetText" class="button is-danger is-rounded override">Reset</button>
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
                        message: 'Underscores applied!',
                        type: 'is-danger',
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
    .content-container {
        display: flex;
        flex-direction: column;
        
        margin: 2rem 0rem;
    }
    .content-container-item {
        margin: 0.5rem 2rem;
    }
    
    .counter-theme {
        font-size: 90px;
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
        border: 1.5px solid #fff;
    }

    .override:hover {
        background: orange;
        border: 1.5px solid #fff;
    }

    .text-counter {
        background: #66615e;
        padding: 1rem;
        border-radius: 50px;
    }

    #inputBox {
        font-size: 1.5rem;
        resize: none;
    }

    @media screen and (max-width: 600px) {
        /* smaller screens */
        .buttons-container.content {
            flex-direction: column;   /* by simply swap direction it work on smaller screen */
            align-items: center;
            justify-content: center;
        }
    }
</style>