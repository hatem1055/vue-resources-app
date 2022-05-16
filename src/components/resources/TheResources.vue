<template>
    <base-card>
        <base-button @click = 'activeComponent = "stored-resources-list" '
        :mode = 'activeComponent == "stored-resources-list" ? null : "flat"'
        >Stored Resources</base-button>
        <base-button @click='activeComponent = "add-resource"'
        :mode = 'activeComponent == "add-resource" ? null : "flat"'
        >Add Resource</base-button>
    </base-card>
    <keep-alive>
        <component :is = "activeComponent" @formSubmited = 'addResource' ></component>
    </keep-alive>
</template>

<script>
import StoredResourcesList from './StoredResourcesList.vue'
import AddResource from './AddResource.vue'


export default {
components: {
        'stored-resources-list':StoredResourcesList,
        'add-resource' : AddResource
    },
provide() {
    return {
        'storedResources' : this.storedResources,
        'removeResource' : this.removeResource
    }
},
methods : {
    addResource(title,desc,link){
        this.storedResources.unshift({
            title,desc,link,id : Date.now().toString()
        })
        this.activeComponent = 'stored-resources-list'
    },
    removeResource(id){
        const resIndex = this.storedResources.findIndex(res => res.id == id)
        this.storedResources.splice(resIndex,1)
    }
},
data() {
    return {
        activeComponent : 'stored-resources-list',
        storedResources: [
            {
                'id': 'official-guide',
                'title': 'official guide',
                'desc': 'The official Vue.js docs',
                'link': 'https://vuejs.org'
            },
            {
                'id': 'Google',
                'title': 'Google',
                'desc': 'To Search',
                'link': 'https://google.com'
            },
        ]
    }
}
}
</script>

<style>

</style>