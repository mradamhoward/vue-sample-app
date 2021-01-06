<template>

<base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
<template #default>
    <p>One input is required atleast.</p>
    <p>Please check all inputs and make sure you enter a few chars for each input.</p>
</template>
<template #actions>
    <the-button @click="confirmError">Ok</the-button>
</template>
</base-dialog>

    <base-card>
        <form @submit.prevent="submitData">
            <div class="form-control">
                <label for="title">Title</label>
                <input id="title" type="text" name="title" ref="titleInput">
            </div>
            <div class="form-control">
                <label for="desc">Description</label>
                <textarea id="desc" type="text" name="description" rows="3"  ref="descInput"></textarea>
            </div>

             <div class="form-control">
                <label for="link">Link</label>
                <input id="link" type="url" name="url"  ref="linkInput"/>
            </div>
            <div>
                <the-button type="submit">Add Resource</the-button>
            </div>
        </form>
    </base-card>
</template>

<script>
import BaseDialog from './UI/BaseDialog.vue';
import TheButton from './UI/TheButton.vue';
export default {
  components: { BaseDialog, TheButton },
    inject: ['addResources'],
    data() {
        return {
            inputIsInvalid: false,

        };

    },
    methods: {
        submitData(){
            const enteredTitle = this.$refs.titleInput.value;
            const enteredDesc = this.$refs.descInput.value;
            const enteredLink = this.$refs.linkInput.value;

            if(enteredTitle.trim() === '' || enteredDesc.trim() === '' || enteredLink.trim() === ''){
                this.inputIsInvalid = true;
                return;
            }

            this.addResources(enteredTitle, enteredDesc, enteredLink);
        },
        confirmError(){
            this.inputIsInvalid = false;
        }
    }
}
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>