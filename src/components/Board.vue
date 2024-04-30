<template>
  <div class="game">
    {{ count }}/{{allowed}}
    <div class="game-board">
      <card
        @click="onCardClick(index)"
        v-for="(food, index) in emojis"
        :food="food"
        :key="index"
      />
    </div>
    <button class="reset-btn" @click="shuffleEmojis()">Reset game</button>
  </div>
</template>
<script>
import Card from "./Card.vue";

export default {
  components: { Card },
  data() {
    return {
      emojis: [
        {
          icon: "🥕",
          fliped: false,
        },
        {
          icon: "🥕",
          fliped: false,
        },
        {
          icon: "🍍",
          fliped: false,
        },
        {
          icon: "🍍",
          fliped: false,
        },
        {
          icon: "🥥",
          fliped: false,
        },
        {
          icon: "🥥",
          fliped: false,
        },
        {
          icon: "🍅",
          fliped: false,
        },
        {
          icon: "🍅",
          fliped: false,
        },
        {
          icon: "🍒",
          fliped: false,
        },
        {
          icon: "🍒",
          fliped: false,
        },
        {
          icon: "🥦",
          fliped: false,
        },
        {
          icon: "🥦",
          fliped: false,
        },
        {
          icon: "🧀",
          fliped: false,
        },
        {
          icon: "🧀",
          fliped: false,
        },
        {
          icon: "🍕",
          fliped: false,
        },
        {
          icon: "🍕",
          fliped: false,
        },
      ],
      selectedCards: [],
      count: 0,
      allowed: 4
    };
  },
  computed: {
    isGameOver() {
        return this.count >= this.allowed
    },
  },
  mounted() {
    this.shuffleEmojis();
  },
  methods: {
    shuffleEmojis() {
      let emojis = this.emojis;
      for (let i = emojis.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [emojis[i], emojis[j]] = [emojis[j], emojis[i]];
      }
      this.emojis = emojis.map((item) => ({
        ...item,
        fliped: false,
      }));
    },
    onCardClick(index) {
      if (this.selectedCards.length === 2) {
        this.selectedCards = [];
      }
      this.emojis[index].fliped = !this.emojis[index].fliped;
      this.selectedCards.push(index);

      this.checkCards();
    },
    checkCards() {
      const firstCard = this.emojis[this.selectedCards[0]];
      const secondCard = this.emojis[this.selectedCards[1]];
      if (
        this.selectedCards.length === 2 &&
        firstCard?.icon !== secondCard?.icon
      ) {
        setTimeout(() => {
          firstCard.fliped = false;
          secondCard.fliped = false;
          this.count += 1;
        }, 500);
      }
    },
  },
  watch: {
    isGameOver(val) {
        if (val) {
            this.count = 0;
            this.shuffleEmojis();
            alert("Game Over!");
        }
    }
  }
};
</script>
<style>
.game {
  display: flex;
  flex-direction: column;
}
.game-board {
  width: 600px;
  height: 600px;
  background-color: #888;
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  align-items: center;
  justify-content: center;
  padding: 20px 10px;
}

.reset-btn {
  margin-top: 20px;
}
</style>