<template>
  <div class="infusion-manual flex-col flex-j-center flex-a-center">
    <p class="text-700 text-b2 text-center">INFUSION</p>
    <hr class="hr-25 hr-mg" />
    <div class="wrapper flex-row flex-a-center flex-j-evenly pd-1">
      <div class="fixed-width">
        <Button
          v-bind:title="!manualState ? 'Process' : 'Processing'"
          v-on:handler="handleClick"
          v-bind:disabledStatus="manualState"
        />
      </div>
      <div class="fixed-width flex-col flex-a-center flex-j-center">
        <p class="text-500 text-s1">COST</p>
        <p class="text-700 text-b1">No costs</p>
      </div>
      <div class="fixed-width flex-col flex-a-center flex-j-center">
        <p class="text-500 text-s1">PROGRESS</p>
        <p class="text-700 text-b1">{{ progress }}/100%</p>
      </div>
      <div class="fixed-width flex-col flex-a-center flex-j-center">
        <p class="text-500 text-s1">COAL AMOUNT</p>
        <p class="text-700 text-b1">
          <CoalFormat>+{{ infusion.rawValue }}</CoalFormat>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import utils from "~/scripts/utils"
import Player from "~/scripts/playerData"
import Button from "../Button"
import CoalFormat from "../CoalFormat"

export default {
  name: "InfusionManual",

  components: {
    Button,
    CoalFormat
  },

  data() {
    return {
      player: Player
    }
  },

  computed: {
    infusion: function() {
      return this.player.modules.alchemy.getAlchemyData("infusion")
    },

    progress: function() {
      return utils.format(
        this.player.modules.alchemy.getManualTick("infusion") * 100
      )
    },

    manualState: function() {
      return this.player.modules.alchemy.getManualState("infusion")
    }
  },

  methods: {
    handleClick: function() {
      this.player.modules.alchemy.setManualState("infusion", true)
    }
  }
}
</script>

<style scoped>
.infusion-manual {
  width: 100%;
}

.wrapper {
  width: 100%;
}

.fixed-width {
  width: 20%;
}
</style>
