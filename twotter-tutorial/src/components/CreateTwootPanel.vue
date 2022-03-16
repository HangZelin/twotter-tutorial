<template>
    <form class="create-twoot" 
    @submit.prevent = "createNewTwoot" 
    :class="{ '--exceeded': newTwootCharacterCount > 180 }">
          <label for="newTwoot"><strong>New Twoot</strong>
                ({{ newTwootCharacterCount }}/180)</label>
          <textarea id ="newTwoot" rows="4" v-model="state.newTwootContent"/>
          <div class=" create-twoot_submit">
          <div class = "create-twoot_type">
              <label for="newTwootType"><strong>Type: </strong></label>
              <select id="newTwootType" v-model="state.selectedTwootType">
                  <option :value="option.value" v-for="(option,index) in state.twootTypes" :key="index">
                  {{ option.name }}
                  </option>
              </select>
          </div>
          <button>
              Twoot it!
          </button>
          </div>
      </form>
</template>

<script>
import { reactive, computed } from 'vue'; 

export default{
    name: "CreateTwootPanel",
    setup(props, ctx) {
      const state = reactive({
            newTwootContent: '',
            selectedTwootType: 'instant',
            twootTypes: [
                {value: 'draft', name: 'Draft'},
                {value: 'instant', name:'Instant Twoot'}
             ]
      })

      const newTwootCharacterCount = computed(() => state.newTwootContent.length)

      function createNewTwoot() {
        if (state.newTwootContent && state.selectedTwootType !== 'draft') {
            ctx.emit('add-twoot', state.newTwootContent);
            state.newTwootContent = '';
        }
      }

      return {
          state,
          newTwootCharacterCount,
          createNewTwoot
      }
    }
}
</script>


<style lang="scss" scoped>
    .create-twoot {
        margin-top: 20px;
        padding: 20px 0;
        display: flex;
        flex-direction: column;
    
    textarea {
        border: 1px solid #DFE3E8;
        border-radius: 5px;
    }
    
    .create-twoot_submit {
        display: flex;
        justify-content: space-between;

        .create-twoot_type {
            padding: 10px 0;
        }
    }

    button {
        padding: 5px 20px;
        margin: auto 0;
        border-radius: 5px;
        border: none;
        background-color: deeppink;
        font-weight: bold;
        color: white;
        transition: all 0.25s ease;
        &:hover {
            background-color: pink ;
            color: white;
        }
    }

    &.--exceeded {
        color: red;
        border-color: red;  

        .create-twoot_submit {
            button{
              background-color: red;
              color: white;        
              &:hover {
                background-color: #FF5D7D;
                color: white;
              }
            }
        }
      }
    }
</style>