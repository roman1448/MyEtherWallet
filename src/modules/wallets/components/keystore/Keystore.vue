<template>
  <v-sheet color="transparent" max-width="800px" class="mx-auto">
    <mew-stepper :items="items" :on-step="currentStep"></mew-stepper>
    <div v-if="currentStep === 1">
      <v-sheet color="white" class="border-radius--10px pa-12">
        <div class="subtitle-1 font-weight-bold grey--text">STEP 1.</div>
        <div class="headline font-weight-bold mb-5">Create password</div>
        <div class="d-flex align-start">
          <mew-input
            hint="Password must be 8 or more charactors"
            label="Password"
            placeholder=" "
            class="mr-3 flex-grow-1"
          />
          <mew-button
            title="Create"
            button-size="xlarge"
            :has-full-width="false"
            @click.native="currentStep = 2"
          />
        </div>
      </v-sheet>
      <warning-sheet
        title="NOT RECOMMENDED"
        description='This information is sensitive, and these options should only be used in offline settings by experienced crypto users. And MEW "CAN NOT" change your password. Please "DO NOT FORGET" to save your password, and it is your private key. You will need this "Password + Keystore file" to access your wallet.'
      />
    </div>

    <div v-if="currentStep === 2">
      <v-sheet color="white" class="border-radius--10px pa-12">
        <div class="subtitle-1 font-weight-bold grey--text">STEP 2.</div>
        <div class="headline font-weight-bold mb-5">
          Download keystore file
        </div>
        <v-row class="align-stretch">
          <v-col v-for="(d, key) in warningData" :key="key">
            <mew-super-button
              :title="d.title"
              :subtitle="d.description"
              is-column
              icon-type="img"
              :right-icon="d.img"
            />
          </v-col>
        </v-row>
        <div class="d-flex justify-center mt-6">
          <mew-button
            title="Acknowledge & Download"
            button-size="xlarge"
            :has-full-width="false"
            @click.native="currentStep = 3"
          />
        </div>
      </v-sheet>
      <warning-sheet
        title="NOT RECOMMENDED"
        description='This information is sensitive, and these options should only be used in offline settings by experienced crypto users. And MEW "CAN NOT" change your password. Please "DO NOT FORGET" to save your password, and it is your private key. You will need this "Password + Keystore file" to access your wallet.'
      />
    </div>

    <v-sheet
      v-if="currentStep === 3"
      color="white"
      class="border-radius--10px pa-12"
    >
      <div class="d-flex align-center">
        <div class="mr-8">
          <div class="subtitle-1 font-weight-bold grey--text">
            STEP 3.
          </div>
          <div class="headline font-weight-bold mb-3">You are done!</div>
          <p class="mb-6">
            Congratulation! Please use the MEWconnect App to scan this QR code
            in order to access your new wallet. And you are done!
          </p>
          <mew-button
            title="Access my wallet"
            button-size="xlarge"
            :has-full-width="false"
            class="mb-5"
            @click.native="currentStep = 1"
          />
          <p class="mt-4 mb-0">
            Need help?
            <router-link
              class="primary--text text-decoration--none font-weight-bold"
              to="/"
              >Get helps from MEWconnect</router-link
            >
          </p>
        </div>
        <v-img
          max-width="250px"
          src="@/assets/images/icons/icon-keystore-mew.png"
        />
      </div>
    </v-sheet>
  </v-sheet>
</template>

<script>
export default {
  name: 'MewConnect',
  props: {},
  data: () => ({
    currentStep: 1,
    items: [
      {
        step: 1,
        name: 'STEP 1. Create password'
      },
      {
        step: 2,
        name: 'STEP 2. Download keystore file'
      },
      {
        step: 3,
        name: 'STEP 3. Well done'
      }
    ],
    warningData: [
      {
        img: require('@/assets/images/icons/icon-paper-plane-mew.svg'),
        title: "Don't lose it",
        description: 'Be careful, it can not be recovered if you lose it.'
      },
      {
        img: require('@/assets/images/icons/icon-money-bag-mew.svg'),
        title: "Don't share it",
        description:
          'Your funds will be stolen if you use this file on a malicious phishing site.'
      },
      {
        img: require('@/assets/images/icons/icon-copy-mew.svg'),
        title: 'Make a backup',
        description:
          'Secure it like the millions of dollars it may one day be worth.'
      }
    ]
  })
};
</script>
