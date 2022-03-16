<template>
    <form class="create-twoot" 
    @submit.prevent = "createNewTwoot" 
    :class="{ '--exceeded': newTwootCharacterCount > 180 }">
          <label for="newTwoot"><strong>New Twoot</strong>
                ({{ newTwootCharacterCount }}/180)</label>
          <textarea id ="newTwoot" rows="4" v-model="newTwootContent"/>
          <div class=" create-twoot_submit">
          <div class = "create-twoot_type">
              <label for="newTwootType"><strong>Type: </strong></label>
              <select id="newTwootType" v-model="selectedTwootType">
                  <option :value="option.value" v-for="(option,index) in twootTypes" :key="index">
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

export default{
    name: "CreateTwootPanel",
    data() {
        return {
            newTwootContent: '',
            selectedTwootType: 'instant',
            twootTypes: [
                {value: 'draft', name: 'Draft'},
                {value: 'instant', name:'Instant Twoot'}
             ],
        }
    },
    computed: {
        newTwootCharacterCount() {
            return this.newTwootContent.length;
        }
    },
    methods: {
        createNewTwoot() {
        if (this.newTwootContent && this.selectedTwootType !== 'draft' && this.newTwootCharacterCount < 180) {
           this.$emit('add-twoot', this.newTwootContent);
        }
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
    }

    &.--exceeded {
        color: red;
        border-color: red;  

        .create-twoot_submit {
            button{
            background-color: red;
            color: white;
            }
        }
      }
    }
</style>