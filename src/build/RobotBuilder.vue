<template>
  <div class="content">
    <div class="preview">
      <div class="preview-content">
        <div class="top-row">
          <img :src="selectedRobot.head.src" alt=""/>
        </div>
        <div class="middle-row">
          <img :src="selectedRobot.leftArm.src" class="rotate-left" alt=""/>
          <img :src="selectedRobot.torso.src" alt=""/>
          <img :src="selectedRobot.rightArm.src" class="rotate-right" alt=""/>
        </div>
        <div class="bottom-row">
          <img :src="selectedRobot.base.src" alt=""/>
        </div>
      </div>
      <button class="add-to-cart" @click="addToCart()">Add to cart</button>
    </div>
    <div class="top-row">
      <div
        class="top part"
        :style="headBorderStyle"
        :class="{ 'sale-boarder': selectedRobot.head.onSale }"
      >
        <!-- <div class="robot-name">
          {{ selectedRobot.head.title }}
          <span class="sale" v-if="selectedRobot.head.onSale">Sale!</span>
        </div> -->
        <PartSelector
          :parts="availableParts.heads"
          position="top"
          @partSelected="part => (selectedRobot.head = part)"
        />
      </div>
    </div>
    <div class="middle-row">
      <PartSelector
        :parts="availableParts.arms"
        position="left"
        @partSelected="part => (selectedRobot.leftArm = part)"
      />
      <PartSelector
        :parts="availableParts.torsos"
        position="center"
        @partSelected="part => (selectedRobot.torso = part)"
      />
      <PartSelector
        :parts="availableParts.arms"
        position="right"
        @partSelected="part => (selectedRobot.rightArm = part)"
      />
    </div>
    <div class="bottom-row">
      <PartSelector
        :parts="availableParts.bases"
        position="bottom"
        @partSelected="part => (selectedRobot.base = part)"
      />
    </div>

    <div>
      <h1>Cart</h1>
      <table>
        <thead>
          <tr>
            <th>Robot</th>
            <th class="cost">cost</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(robot, index) in cart" :key="index">
            <td>{{ robot.head.title }}</td>
            <td>{{ robot.cost }}</td>
          </tr>
          <tr>
            <td>Total</td>
            <td>{{ totalCost }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
/* eslint linebreak-style: ["error", "windows"] */
import availableParts from '../data/parts';
import PartSelector from './PartSelector.vue';

export default {
  name: 'RobotBuilder',
  components: { PartSelector },
  data() {
    return {
      availableParts,
      cart: [],
      selectedRobot: {
        head: {},
        leftArm: {},
        torso: {},
        rightArm: {},
        base: {},
      },
    };
  },
  computed: {
    totalCost() {
      return this.cart.length > 0
        ? this.cart.reduce((total, robot) => total + robot.cost, 0)
        : 0;
    },
    headBorderStyle() {
      return {
        border: this.selectedRobot.head.onSale
          ? '3px solid red'
          : '3px solid grey',
      };
    },
  },
  methods: {
    addToCart() {
      const robot = this.selectedRobot;
      const cost = robot.head.cost
        + robot.leftArm.cost
        + robot.rightArm.cost
        + robot.torso.cost
        + robot.base.cost;
      this.cart.push({ ...this.selectedRobot, cost });
    },
  },
};
</script>

<style scoped>
.top-row {
  display: flex;
  justify-content: space-around;
}
.middle-row {
  display: flex;
  justify-content: center;
}
.bottom-row {
  display: flex;
  justify-content: space-around;
  border-top: none;
}

.robot-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}

.content {
  position: relative;
}
.add-to-cart {
  position: absolute;
  width: 210px;
  padding: 3px;
  font-size: 16px;
}

td,
th {
  text-align: left;
  padding: 5px;
  padding-right: 20px;
}

tr {
  text-align: right;
}

.sale-boarder {
  border: 3px solid red;
}

.preview {
  position: absolute;
  top: -20px;
  right: 0;
  width: 210px;
  height: 210px;
  padding: 5px;
}
.preview-content {
  border: 1px solid #999;
}
.preview img {
  width: 50px;
  height: 50px;
}
.rotate-right {
  transform: rotate(90deg);
}
.rotate-left {
  transform: rotate(-90deg);
}
</style>
