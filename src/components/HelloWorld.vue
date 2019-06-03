<template>
  <div class="hello col-4">
    <h1>Hello Vue</h1>
    <h3>Choose Your Target!</h3>
    <button
      v-for="target in targets"
      :key="target.name"
      @click="activeTarget = target"
    >{{target.name}}</button>
    <div v-if="activeTarget.name">
      <h4
        :class="{
        alive: activeTarget.health >= 50, 
        bloodied: activeTarget.health < 50 && activeTarget.health>0, 
        dead: activeTarget.health == 0}"
      >{{ activeTarget.name }}</h4>
      <p>{{ activeTarget.health }}</p>
      <p v-if="activeTarget.health > 50">GET' EM!</p>
      <p v-else-if="activeTarget.health > 0">He's Bloodied</p>
      <p v-else>He Dead</p>
      <button
        v-for="(damage, attackName) in activeTarget.attacks"
        :key="damage"
        @click="attack(attackName)"
      >{{attackName}}</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      activeTarget: {},
      targets: [
        {
          name: "Mark",
          health: 100,
          attacks: {
            slap: 1,
            punch: 5,
            kick: 10
          }
        },
        {
          name: "Jake",
          health: 100,
          attacks: {
            code: 0,
            punch: 6,
            dropKick: 9
          }
        },
        {
          name: "D$",
          health: 100,
          attacks: {
            log: -5,
            hug: 4,
            typo: 1
          }
        }
      ]
    };
  },
  methods: {
    attack(attackType) {
      this.activeTarget.health -= this.activeTarget.attacks[attackType];
      if (this.activeTarget.health < 0) {
        this.activeTarget.health = 0;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.alive {
  color: green;
}
.bloodied {
  color: yellow;
}
.dead {
  color: red;
}
</style>
