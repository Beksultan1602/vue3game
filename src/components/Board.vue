<template>
  <div class="board-wrapper">
    <div class="board">
      <BoardItem :game-status="gameStatus" v-for="field in fields" :field="field" :key="'item-' + field.id"
        @selectField="selectField($event)"/>
    </div>
    
    <p class="difficult">Сложность: <strong>{{ difficult }}</strong></p>
    <p class="win" v-if="isWin">Поздравляем! Продолжаем играть!</p>
    <p class="fail" v-if="isFail">Вы проиграли. Попробуйте еще раз!</p>
  
    <button class="btn" @click="start" :disabled="!canStartGame">Старт</button>
  </div>
</template>

<script>
import BoardItem from './BoardItem';
import useGameInit from "@/components/composables/useGameInit";
import useGameStart from "@/components/composables/useGameStart";
import useGameProcess from "@/components/composables/useGameProcess";
import { GAME_STATUS } from "@/constants";
import { ref } from 'vue';
export default {
  name: 'Board',
  props: {},
  components: {
    BoardItem,
  },
  setup() {
    const number = 25;
    const gameStatus = ref(GAME_STATUS.NONE);
    
    const { difficult, fields, init } = useGameInit(number);
    
    const { start, canStartGame } = useGameStart(init, fields, difficult, number, gameStatus);
    const { selectField, isWin, isFail } = useGameProcess(fields, gameStatus, difficult, start);
    
    return {
      number,
      difficult,
      fields,
      init,
      start,
      gameStatus,
      canStartGame,
      selectField,
      isWin,
      isFail
    }
  },
}
</script>

<style scoped>
    .board {
        width: 300px;
        background: rgb(0, 0, 0);
        margin: 0 auto;
    }

    .btn {
        background: #f74e00;
        color: #000;
        border: none;
        border-radius: 2px;
        padding: 10px 30px;
        margin: 10px 0;
        cursor: pointer;
        outline: none;
    }
    
    button:hover {
        background: #f74e00cc;
    }
    
    button:disabled {
        opacity: .5;
    }
    .win {
        color: #f74e00;
    }
  
    .fail {
        color: #f74e00;
    }
</style>   