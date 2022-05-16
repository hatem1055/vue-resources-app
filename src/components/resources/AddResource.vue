<template>
    <teleport to = 'body'>
        <error-dialog v-if = 'isInvalid' :title = "inValidField + ' Is Invalid'" @close = "isInvalid = false">
            <template #section>
                <p>{{inValidMessage}}</p>
            </template>
            <template #actions>
                <base-button @click="isInvalid = false">Okay</base-button>
            </template>
        </error-dialog>
    </teleport>
    <base-card>
        <form @submit.prevent = 'sendData'>
            <div class='form-control'>
                <label for='title'>Title</label>
                <input id='title' name='title' type='text' ref = 'title'/>
            </div>
            <div class='form-control'>
                <label for='title'>Description</label>
                <textarea id='desc' name='desc' row='3' ref = 'desc'/>
            </div>
            <div class='form-control'>
                <label for='link'>Link</label>
                <input id='Link' name='link' type='url' ref = 'url'/>
            </div>
            <base-button type='submit'>Submit</base-button>
        </form>
    </base-card>
</template>
<script>
export default {
    data(){
        return {
            isInvalid : false,
            inValidField : '',
            inValidMessage : ''
        }
    },
    methods : {
        validaData(){
            console.log('askjjkac')
            let title = this.$refs.title.value
            let desc = this.$refs.desc.value
            let url  = this.$refs.url.value
            if(title.length == 0){
                this.inValidMessage = 'Title Cant Be empty'
                this.inValidField = 'title'
                this.isInvalid = true
                return false
            }
            if(desc.length == 0){
                this.inValidMessage = 'Description Cant Be empty'
                this.inValidField = 'Description'
                this.isInvalid = true
                return false
            }
            if(url.length == 0){
                this.inValidMessage = 'Url Cant Be empty'
                this.inValidField = 'Url'
                this.isInvalid = true
                return false
            }
            return true
        },
        sendData(){
            if (this.validaData()){
                this.$emit('formSubmited',this.$refs.title.value,this.$refs.desc.value,this.$refs.url.value)
                this.$refs.title.value = this.$refs.desc.value = this.$refs.url.value = ''
            }

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