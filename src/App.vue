<template>
  <div class="viewport" :class="mode">
    <header>
      <div class="avatar">
        <img src="@/assets/img/avatar.png">
      </div>
      <div class="right">
        <SwitchTheme :mode="mode" @change="changeTheme" />
      </div>
    </header>
    <main>
      <h1>Hola, Oscar</h1>
      <div class="grid">
        <div class="box half">
          <h5>Hora<br>actual</h5>
          <h1 class="spacing big center">{{time}}</h1>
        </div>
        <div class="box half enfasis">
          <h5>Control<br>de luz</h5>
          <Switch class="spacing" :mode="mode" />
        </div>
        <div class="box side-by-side">
          <h5>Modo automático</h5>
          <Switch class="borders" :mode="mode" />
        </div>
        <div class="box">
          <a href="#" class="edit-icon" @click="toggleModal"><PenIcon :fill="mode == 'dark' ? 'white' : undefined" /></a>
          <h5 class="margin-bottom">Horario programado</h5>
          <div class="flex">
            <h5>Desde</h5>
            <h3>{{ programmedFrom }}</h3>
          </div>
          <div class="flex">
            <h5>Hasta</h5>
            <h3>{{ programmedTo }}</h3>
          </div>
        </div>
      </div>
    </main>

    <div class="modal" :class="{hidden: !modal}">
      <div class="window">
        <div class="flex">
          <h5>Desde</h5>
          <input type="text" v-model="programmedFrom">
        </div>
        <div class="flex">
          <h5>Hasta</h5>
          <input type="text" v-model="programmedTo">
        </div>
        <button @click="toggleModal">Guardar</button>
      </div>
    </div>
  </div>
</template>

<script>
import SwitchTheme from '@/components/SwitchTheme.vue'
import Switch from '@/components/Switch.vue'
import PenIcon from '@/components/PenIcon.vue'

export default {
  data() {
    return {
      mode: 'light',
      time: "",
      modal: false,
      programmedFrom: "17:00",
      programmedTo: "22:00"
    }
  },
  mounted() {
    this.getTime()
    setInterval(() => {
      this.getTime()
    }, 1000);
  },
  components: {
    SwitchTheme, Switch, PenIcon
  },
  methods: {
    changeTheme(switched) {
      this.mode = switched ? 'dark' : 'light'
    },
    getTime() {
      let timeStr = new Date().toLocaleTimeString('en-US', {hour12: false})
      this.time = timeStr.substring(0, timeStr.length - 3)
    },
    toggleModal() {
      this.modal = !this.modal
    }
  }
}
</script>