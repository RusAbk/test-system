<template>
    <div class="question" v-bind:class=" (isAnsRight ? 'right' : 'incorrect') ">
        <p>
            <slot></slot>
        </p>
        <div class="variants">
            <label v-for="(isRight, key) in variants" v-bind:key="key">
                <input type="checkbox" v-model="checkboxes" v-bind:value="key"> {{key}}
            </label>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Question',
    props: ['variants'],
    data(){
        return {
            checkboxes: [],
        }
    },
    computed: {
        isAnsRight(){
            let rightVars = [];
            for(let key in this.variants){
                if(this.variants[key] == true)
                    rightVars.push(key)
            }

            let isAllRightChkd = true;
            for(let el of rightVars){
                if(this.checkboxes.indexOf(el) == -1)
                    isAllRightChkd = false;
            }

            let isNoIncorrect = true;
            for(let el of this.checkboxes){
                if( this.variants[el] == false )
                    isNoIncorrect = false;
            }

            return isAllRightChkd && isNoIncorrect;
        }
    }
}
</script>

<style>
    .question{
        width: 500px;
        border: 1px solid #333;
        border-radius: 5px;
        padding: 20px;
        margin: auto;
    }
    .right{
        background-color: #6bdf6b;
    }
    .incorrect{
        background-color: #df6b6b;
    }
</style>