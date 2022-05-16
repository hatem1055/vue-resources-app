<template>
    <ul>
        <resource-item v-for='res in storedResources' :key='res.id' :link='res.link' :title='res.title' :id='res.id'
            :desc='res.desc'></resource-item>
    </ul>
</template>


<script>
import ResourceItem from './ResourceItem.vue'
export default {
    components: {
        'resource-item': ResourceItem,
    },
    inject: ['storedResources','removeResource']

}
</script>
<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>