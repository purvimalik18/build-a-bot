<!-- eslint-disable linebreak-style -->
<template>
<div class="content">
  <button class="add-to-cart" @click="addToCart()">Add to Cart</button>
    <div class="top-row">
      <!-- binding inline class -->
        <div class="top part" :style="headBorderStyle">
          <div class="robot-name">
            {{selectedRobot.head.title}}
            <span class="sale" v-if="selectedRobot.head.onSale">Sale!</span>
          </div>
        <img :src="selectedRobot.head.src" alt=""  title="head"/>
        <button class="prev-selector" @click="selectPreviousHead()">&#9668;</button>
        <button class="next-selector" @click="selectNextHead()">&#9658;</button>
        </div>
    </div>
    <div class="middle-row">
        <div class="left part">
        <img :src="selectedRobot.leftArm.src" alt="" title="left arm"/>
        <button class="prev-selector"  @click="selectPreviousLeftArm()">&#9650;</button>
        <button class="next-selector" @click="selectNextLeftArm()">&#9660;</button>
        </div>
        <div class="center part">
        <img :src="selectedRobot.torsos.src" alt="" title="torsos"/>
        <button class="prev-selector" @click="selectPreviousTorsos()">&#9668;</button>
        <button class="next-selector" @click="selectNextTorsos()">&#9658;</button>
        </div>
        <div class="right part">
        <img :src="selectedRobot.rightArm.src" alt=""
        title="right arm"/>
        <button class="prev-selector" @click="selectPreviousRightArm()">&#9650;</button>
        <button class="next-selector" @click="selectNextRightArm()">&#9660;</button>
        </div>
    </div>
    <div class="bottom-row">
        <div class="bottom part">
        <img :src="selectedRobot.bases.src" alt="" title="base"/>
        <button class="prev-selector" @click="selectPreviousBases()">&#9668;</button>
        <button class="next-selector" @click="selectNextBases()">&#9658;</button>
        </div>
    </div>
    <div>
      <h1>Cart</h1>
      <table>
        <thead>
          <tr>
            <th>Robot</th>
            <th class="cost">Cast</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(robot, index) in cart" :key = "index">
            <td>{{robot.head.title}}</td>
            <td class="cost">{{robot.cost}}</td>
          </tr>
        </tbody>
      </table>
    </div>
</div>
</template>
<!-- eslint-disable linebreak-style -->

<script>
import availableParts from '../data/parts';

function getPreviousValidIndex(index, length) {
  const depracatedIndex = index - 1;
  return depracatedIndex < 0 ? length - 1 : depracatedIndex;
}

function getNextValidIndex(index, length) {
  const incrementedIndex = index - 1;
  return incrementedIndex < 0 ? length - 1 : incrementedIndex;
}

export default {
  name: 'RobotBuilder',
  data() {
    return {
      availableParts,
      cart: [],
      selectNextHeadIndex: 0,
      selectNextLeftArmIndex: 0,
      selectNextTorsosIndex: 0,
      selectNextRightArmIndex: 0,
      selectNextBaseIndex: 0,
    };
  },

  computed: {
    headBorderStyle() {
      return { border: this.selectedRobot.head.onSale ? '3px solid red' : '3px solid #aaa' };
    },
    selectedRobot() {
      return {
        head: availableParts.heads[this.selectNextHeadIndex],
        leftArm: availableParts.arms[this.selectNextLeftArmIndex],
        torsos: availableParts.torsos[this.selectNextTorsosIndex],
        rightArm: availableParts.arms[this.selectNextRightArmIndex],
        bases: availableParts.bases[this.selectNextBaseIndex],
      };
    },
  },

  methods: {
    addToCart() {
      const robot = this.selectedRobot;
      const cost = robot.head.cost + robot.leftArm.cost
      + robot.rightArm.cost + robot.bases.cost + robot.torsos.cost;
      this.cart.push({ ...robot, cost });
    },

    selectNextHead() {
      this.selectNextHeadIndex = getNextValidIndex(
        this.selectNextHeadIndex,
        availableParts.heads.length,
      );
    },
    selectPreviousHead() {
      this.selectNextHeadIndex = getPreviousValidIndex(
        this.selectNextHeadIndex,
        availableParts.heads.length,
      );
    },

    selectNextLeftArm() {
      this.selectNextLeftArmIndex = getNextValidIndex(
        this.selectNextLeftArmIndex,
        availableParts.arms.length,
      );
    },
    selectPreviousLeftArm() {
      this.selectNextLeftArmIndex = getPreviousValidIndex(
        this.selectNextLeftArmIndex,
        availableParts.arms.length,
      );
    },

    selectNextTorsos() {
      this.selectNextTorsosIndex = getNextValidIndex(
        this.selectNextTorsosIndex,
        availableParts.torsos.length,
      );
    },
    selectPreviousTorsos() {
      this.selectNextTorsosIndex = getPreviousValidIndex(
        this.selectNextTorsosIndex,
        availableParts.torsos.length,
      );
    },

    selectNextRightArm() {
      this.selectNextRightArmIndex = getNextValidIndex(
        this.selectNextRightArmIndex,
        availableParts.arms.length,
      );
    },
    selectPreviousRightArm() {
      this.selectNextRightArmIndex = getPreviousValidIndex(
        this.selectNextRightArmIndex,
        availableParts.arms.length,
      );
    },

    selectNextBases() {
      this.selectNextBaseIndex = getNextValidIndex(
        this.selectNextBaseIndex,
        availableParts.bases.length,
      );
    },
    selectPreviousBases() {
      this.selectNextBaseIndex = getPreviousValidIndex(
        this.selectNextBaseIndex,
        availableParts.bases.length,
      );
    },
  },

};
</script>
<!-- eslint-disable linebreak-style -->

<style scoped>
    .part {
        position: relative;
        width:165px;
        height:165px;
        border: 3px solid #aaa;
      }
      .part img {
        width:165px;
      }
      .top-row {
        display:flex;
        justify-content: space-around;
      }
      .middle-row {
        display:flex;
        justify-content: center;
      }
      .bottom-row {
        display:flex;
        justify-content: space-around;
        border-top: none;
      }
      .head {
        border-bottom: none;
      }
      .left {
        border-right: none;
      }
      .right {
        border-left: none;
      }
      .left img {
        transform: rotate(-90deg);
      }
      .right img {
        transform: rotate(90deg);
      }
      .bottom {
        border-top: none;
      }
      .prev-selector {
        position: absolute;
        z-index:1;
        top: -3px;
        left: -28px;
        width: 25px;
        height: 171px;
      }
      .next-selector {
        position: absolute;
        z-index:1;
        top: -3px;
        right: -28px;
        width: 25px;
        height: 171px;
      }
      .center .prev-selector, .center .next-selector {
        opacity:0.8;
      }
      .left .prev-selector {
        top: -28px;
        left: -3px;
        width: 144px;
        height: 25px;
      }
      .left .next-selector {
        top: auto;
        bottom: -28px;
        left: -3px;
        width: 144px;
        height: 25px;
      }
      .right .prev-selector {
        top: -28px;
        left: 24px;
        width: 144px;
        height: 25px;
      }
      .right .next-selector {
        top: auto;
        bottom: -28px;
        left: 24px;
        width: 144px;
        height: 25px;
      }
      .right .next-selector {
        right: -3px;
      }

      .robot-name{
        position: absolute;
        top: -25px;
        text-align: center;
        width: 100% ;
      }

      .sale{
        color: red;
      }

      .content{
        position: relative;
      }

      .add-to-cart{
        position: absolute;
        right: 30px;
        width: 220px;
        padding: 3px;
        font-size: 16px;
      }

      td,th{
        text-align: left;
        padding: 5px;
        padding-right: 20px;
      }

      .cost{
        text-align: right;
      }
</style>
