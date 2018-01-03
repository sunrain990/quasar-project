<template>
  <div>
    <q-btn :infinite="myInfiniteVariable">Do something</q-btn>
    <q-icon name="alarm" />
    <q-icon name="cloud"></q-icon>
    <q-icon name="thumb_up" />

    <q-icon name="ion-heart" />
    <!-- Fontawesome icons have "fa-" prefix -->
    <q-icon name="fa-id-card" />
    <!-- IcoMoon icons have "icon-" prefix -->
    <q-icon name="icon-chrome" />

    <q-icon name="thumb_up" style="font-size: 5rem" />



    <!-- Token (as CSS class) -->
    <span class="token">blue</span>
    <!-- Small and Big text -->
    <small>Text</small>
    <big>Text</big>
    <!-- sub and sup -->
    <sub>Subtext</sub>
    <sup>Supertext</sup>
    <!-- Paragraphs -->
    <p>Default Paragraph</p>
    <p class="caption">Caption Paragraph</p>
    <p class="light-paragraph">Light Paragraph</p>
    <p class="thin-paragraph">Thin Paragraph</p>
    <!-- Bold or italic -->
    <p class="text-bold">Bold text</p>
    <!-- or: --><strong>Bold text</strong>
    <p class="text-italic">Italic text</p>
    <!-- or: --><em>Italic text</em>
    <!-- Quotes -->
    <div class="quote">
      Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante.
    </div>
    <div class="quote text-right">
      Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante.
    </div>
    <!-- Blockquotes -->
    <blockquote>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante.</p>
      <small>Someone famous for <cite title="Quasar Framework">Quasar Framework</cite></small>
    </blockquote>
    <blockquote class="text-right">
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante.</p>
      <small>Someone famous for <cite title="Quasar Framework">Quasar Framework</cite></small>
    </blockquote>
    <!-- Definition Lists -->
    <dl>
      <dt>Description lists</dt>
      <dd>A description list is perfect for defining terms.</dd>
      <dt>Euismod</dt>
      <dd>Vestibulum id ligula porta felis euismod semper eget lacinia odio sem nec elit.</dd>
    </dl>
    <dl class="horizontal">
      <dt>Description lists</dt>
      <dd>A description list is perfect for defining terms.</dd>
      <dt>Euismod</dt>
      <dd>Vestibulum id ligula porta felis euismod semper eget lacinia odio sem nec elit.</dd>
    </dl>
    <!-- Tokens; alternative: Chips -->
    <span class="token">Some token</span>


    <div v-if="$q.platform.is.ios">
      Gets rendered only on iOS platform.
    </div>


    <p class="text-primary">....</p>
    <span class="bg-primary">....</span>


    <div
            v-ripple="rippleEnabled"
            class="relative-position"
    >
      <q-checkbox
              v-model="rippleEnabled"
              label="Enable Ripples"
      />
      .....
    </div>

    <q-checkbox
            v-model="rippleEnabled"
            checked-icon="sentiment very satisfied"
            unchecked-icon="sentiment very dissatisfied"
    />

    <q-checkbox
            v-model="rippleEnabled"
            checked-icon="visibility"
            unchecked-icon="visibility_off"
    />

    <q-checkbox v-model="rippleEnabled" color="teal" />
    <q-checkbox v-model="rippleEnabled" color="orange" />
    <q-checkbox v-model="rippleEnabled" color="dark" />



    <div class="row">
      <div class="col-8">two thirds</div>
      <div class="col-2">one sixth</div>
      <div class="col-auto">auto size based on content and available space</div>
      <div class="col">fills remaining available space</div>
    </div>

  </div>
</template>
<script>
    import { QBtn, QIcon, Platform, Toast, QCheckbox } from 'quasar'
    import { Events } from 'quasar'
    import {
        Loading,
        // optional!, for example below
        // with custom spinner
        QSpinnerGears
    } from 'quasar'

    import { Ripple } from 'quasar'


    Events.$on('app:loading', state => {
        console.log(`Loading has become ${state ? 'visible' : 'hidden'}`)
    })

//    Loading.show({
//        spinner: QSpinnerGears,
//        message: 'Some message',
//        messageColor: 'blue',
//        spinnerSize: 250, // in pixels
//        spinnerColor: 'white',
//        customClass : 'bg-primary'
//    })
//
//    setTimeout(function () {
//        Loading.hide()
//    }, 3000)

//
//    Toast.create.positive({
//        html: 'Message to display',
//        icon: 'alarm_add',
//        timeout: 1000,
//        color: '#f8c1c1',
//        bgColor: 'white',
//        button: {
//            label: 'Undo',
//            handler () {
//                // Specify what to do when button is clicked/tapped
//            },
//            color: '#000'
//        }
//    })

    export default {
        directives: {
            Ripple
        },
        data() {
            return {
                myInfiniteVariable: false,
                rippleEnabled: true
            }
        },
        components: {
            QBtn,
            QIcon,
            QCheckbox
        },
        created () {
            this.handler = state => {
                console.log('App became', state)
            }
            this.$q.events.$on('app:visibility', this.handler)

        },
        beforeDestroy () {
            this.$q.events.$off('app:visibility', this.handler)
            Loading.hidden()
        },
        mounted() {
            console.log(Platform.is);
        },
        methods: {
            show () {
                // prints out Quasar version
                console.log(this.$q.version)
            }
        }
    }
</script>